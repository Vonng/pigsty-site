---
title: "Parameter Reference"
linkTitle: "Parameter Reference"
date: 2017-01-05
weight: 1
description: >
  Example configuration for vagrant sandbox environment 
---


```yaml
---
######################################################################
# File      :   dev.yml
# Path      :   conf/dev.yml
# Desc      :   Configuration file for development (demo) environment
# Note      :   follow ansible inventory file format
# Ctime     :   2020-05-22
# Mtime     :   2020-12-22
# Copyright (C) 2019-2021 Ruohang Feng
######################################################################


######################################################################
#               Development Environment Inventory                    #
######################################################################
all: # top-level namespace, match all hosts


  #==================================================================#
  #                           Clusters                               #
  #==================================================================#
  children: # top-level groups, one group per database cluster (and special group 'meta')

    #-----------------------------
    # meta controller
    #-----------------------------
    meta: # special group 'meta' defines the main controller machine
      vars:
        meta_node: true                     # mark node as meta controller
        ansible_group_priority: 99          # meta group is top priority

      # nodes in meta group
      hosts: {10.10.10.10: {ansible_host: meta}}

    #-----------------------------
    # cluster: pg-meta
    #-----------------------------
    pg-meta:

      # - cluster members - #
      hosts:
        10.10.10.10: {pg_seq: 1, pg_role: primary, ansible_host: meta}

      # - cluster configs - #
      vars:
        pg_cluster: pg-meta                 # define actual cluster name
        pg_version: 13                      # define installed pgsql version
        node_tune: oltp                     # tune node into oltp|olap|crit|tiny mode
        pg_conf: oltp.yml                   # tune pgsql into oltp/olap/crit/tiny mode
        patroni_mode: pause                 # enter maintenance mode, {default|pause|remove}
        patroni_watchdog_mode: off          # disable watchdog (require|automatic|off)
        pg_users:                           # create a business user named 'dbuser_meta'
          - {username: dbuser_meta, password: DBUser.Meta, groups: [dbrole_readwrite]}
        pg_databases:                       # create a business database 'meta'
          - name: meta
            schemas: [meta]                 # create extra schema named 'meta'
            extensions: [{name: postgis}]   # create extra extension postgis
            parameters:                     # overwrite database meta's default search_path
              search_path: public, monitor
        pg_default_database: meta           # default database will be used as primary monitor target

        # proxy settings
        vip_enabled: true                   # enable/disable vip (require members in same LAN)
        vip_address: 10.10.10.2             # virtual ip address
        vip_cidrmask: 8                     # cidr network mask length
        vip_interface: eth1                 # interface to add virtual ip


    #-----------------------------
    # cluster: pg-test
    #-----------------------------
    pg-test: # define cluster named 'pg-test'
      # - cluster members - #
      hosts:
        10.10.10.11: {pg_seq: 1, pg_role: primary, ansible_host: node-1}
        10.10.10.12: {pg_seq: 1, pg_role: replica, ansible_host: node-2}
        10.10.10.13: {pg_seq: 1, pg_role: replica, ansible_host: node-3}
      # - cluster configs - #
      vars:
        # basic settings
        pg_cluster: pg-test                 # define actual cluster name
        pg_version: 13                      # define installed pgsql version
        node_tune: tiny                     # tune node into oltp|olap|crit|tiny mode
        pg_conf: tiny.yml                   # tune pgsql into oltp/olap/crit/tiny mode

        pg_users:
          - username: test
            password: test
            comment: default test user
            groups: [ dbrole_readwrite ]
        pg_databases:                       # create a business database 'test'
          - name: test
            extensions: [{name: postgis}]   # create extra extension postgis
            parameters:                     # overwrite database meta's default search_path
              search_path: public,monitor
        pg_default_database: test           # default database will be used as primary monitor target

        # proxy settings
        vip_enabled: true                   # enable/disable vip (require members in same LAN)
        vip_address: 10.10.10.3             # virtual ip address
        vip_cidrmask: 8                     # cidr network mask length
        vip_interface: eth1                 # interface to add virtual ip



  #==================================================================#
  #                           Globals                                #
  #==================================================================#
  vars:

    #------------------------------------------------------------------------------
    # CONNECTION PARAMETERS
    #------------------------------------------------------------------------------
    # this section defines connection parameters

    # ansible_user: vagrant             # admin user with ssh access and sudo privilege

    proxy_env: # global proxy env when downloading packages
      # http_proxy: 'http://xxxxxx'
      # https_proxy: 'http://xxxxxx'
      # all_proxy: 'http://xxxxxx'
      no_proxy: "localhost,127.0.0.1,10.0.0.0/8,192.168.0.0/16,*.pigsty,*.aliyun.com"

    #------------------------------------------------------------------------------
    # REPO PROVISION
    #------------------------------------------------------------------------------
    # this section defines how to build a local repo

    repo_enabled: true                            # build local yum repo on meta nodes?
    repo_name: pigsty                             # local repo name
    repo_address: yum.pigsty                      # repo external address (ip:port or url)
    repo_port: 80                                 # listen address, must same as repo_address
    repo_home: /www                               # default repo dir location
    repo_rebuild: false                           # force re-download packages
    repo_remove: true                             # remove existing repos

    # - where to download - #
    repo_upstreams:
      - name: base
        description: CentOS-$releasever - Base - Aliyun Mirror
        baseurl:
          - http://mirrors.aliyun.com/centos/$releasever/os/$basearch/
          - http://mirrors.aliyuncs.com/centos/$releasever/os/$basearch/
          - http://mirrors.cloud.aliyuncs.com/centos/$releasever/os/$basearch/
        gpgcheck: no
        failovermethod: priority

      - name: updates
        description: CentOS-$releasever - Updates - Aliyun Mirror
        baseurl:
          - http://mirrors.aliyun.com/centos/$releasever/updates/$basearch/
          - http://mirrors.aliyuncs.com/centos/$releasever/updates/$basearch/
          - http://mirrors.cloud.aliyuncs.com/centos/$releasever/updates/$basearch/
        gpgcheck: no
        failovermethod: priority

      - name: extras
        description: CentOS-$releasever - Extras - Aliyun Mirror
        baseurl:
          - http://mirrors.aliyun.com/centos/$releasever/extras/$basearch/
          - http://mirrors.aliyuncs.com/centos/$releasever/extras/$basearch/
          - http://mirrors.cloud.aliyuncs.com/centos/$releasever/extras/$basearch/
        gpgcheck: no
        failovermethod: priority

      - name: epel
        description: CentOS $releasever - EPEL - Aliyun Mirror
        baseurl: http://mirrors.aliyun.com/epel/$releasever/$basearch
        gpgcheck: no
        failovermethod: priority

      - name: grafana
        description: Grafana - TsingHua Mirror
        gpgcheck: no
        baseurl: https://mirrors.tuna.tsinghua.edu.cn/grafana/yum/rpm

      - name: prometheus
        description: Prometheus and exporters
        gpgcheck: no
        baseurl: https://packagecloud.io/prometheus-rpm/release/el/$releasever/$basearch

      - name: pgdg-common
        description: PostgreSQL common RPMs for RHEL/CentOS $releasever - $basearch
        gpgcheck: no
        baseurl: https://download.postgresql.org/pub/repos/yum/common/redhat/rhel-$releasever-$basearch

      - name: pgdg13
        description: PostgreSQL 13 for RHEL/CentOS $releasever - $basearch - Updates testing
        gpgcheck: no
        baseurl: https://download.postgresql.org/pub/repos/yum/13/redhat/rhel-$releasever-$basearch

      - name: centos-sclo
        description: CentOS-$releasever - SCLo
        gpgcheck: no
        mirrorlist: http://mirrorlist.centos.org?arch=$basearch&release=7&repo=sclo-sclo

      - name: centos-sclo-rh
        description: CentOS-$releasever - SCLo rh
        gpgcheck: no
        mirrorlist: http://mirrorlist.centos.org?arch=$basearch&release=7&repo=sclo-rh

      - name: nginx
        description: Nginx Official Yum Repo
        skip_if_unavailable: true
        gpgcheck: no
        baseurl: http://nginx.org/packages/centos/$releasever/$basearch/

      - name: haproxy
        description: Copr repo for haproxy
        skip_if_unavailable: true
        gpgcheck: no
        baseurl: https://download.copr.fedorainfracloud.org/results/roidelapluie/haproxy/epel-$releasever-$basearch/

      # for latest consul & kubernetes
      - name: harbottle
        description: Copr repo for main owned by harbottle
        skip_if_unavailable: true
        gpgcheck: no
        baseurl: https://download.copr.fedorainfracloud.org/results/harbottle/main/epel-$releasever-$basearch/


    # - what to download - #
    repo_packages:
      # repo bootstrap packages
      - epel-release nginx wget yum-utils yum createrepo                                      # bootstrap packages

      # node basic packages
      - ntp chrony uuid lz4 nc pv jq vim-enhanced make patch bash lsof wget unzip git tuned   # basic system util
      - readline zlib openssl libyaml libxml2 libxslt perl-ExtUtils-Embed ca-certificates     # basic pg dependency
      - numactl grubby sysstat dstat iotop bind-utils net-tools tcpdump socat ipvsadm telnet  # system utils

      # dcs & monitor packages
      - grafana prometheus2 pushgateway alertmanager                                          # monitor and ui
      - node_exporter postgres_exporter nginx_exporter blackbox_exporter                      # exporter
      - consul consul_exporter consul-template etcd                                           # dcs

      # python3 dependencies
      - ansible python python-pip python-psycopg2                                             # ansible & python
      - python3 python3-psycopg2 python36-requests python3-etcd python3-consul                # python3
      - python36-urllib3 python36-idna python36-pyOpenSSL python36-cryptography               # python3 patroni extra deps

      # proxy and load balancer
      - haproxy keepalived dnsmasq                                                            # proxy and dns

      # postgres common Packages
      - patroni patroni-consul patroni-etcd pgbouncer pg_cli pgbadger pg_activity               # major components
      - pgcenter boxinfo check_postgres emaj pgbconsole pg_bloat_check pgquarrel                # other common utils
      - barman barman-cli pgloader pgFormatter pitrery pspg pgxnclient PyGreSQL pgadmin4 tail_n_mail

      # postgres 13 packages
      - postgresql13* postgis31* citus_13 pgrouting_13                                          # postgres 13 and postgis 31
      - pg_repack13 pg_squeeze13                                                                # maintenance extensions
      - pg_qualstats13 pg_stat_kcache13 system_stats_13 bgw_replstatus13                        # stats extensions
      - plr13 plsh13 plpgsql_check_13 plproxy13 plr13 plsh13 plpgsql_check_13 pldebugger13      # PL extensions                                      # pl extensions
      - hdfs_fdw_13 mongo_fdw13 mysql_fdw_13 ogr_fdw13 redis_fdw_13 pgbouncer_fdw13             # FDW extensions
      - wal2json13 count_distinct13 ddlx_13 geoip13 orafce13                                    # MISC extensions
      - rum_13 hypopg_13 ip4r13 jsquery_13 logerrors_13 periods_13 pg_auto_failover_13 pg_catcheck13
      - pg_fkpart13 pg_jobmon13 pg_partman13 pg_prioritize_13 pg_track_settings13 pgaudit15_13
      - pgcryptokey13 pgexportdoc13 pgimportdoc13 pgmemcache-13 pgmp13 pgq-13
      - pguint13 pguri13 prefix13  safeupdate_13 semver13  table_version13 tdigest13


    repo_url_packages:
      - https://github.com/Vonng/pg_exporter/releases/download/v0.3.1/pg_exporter-0.3.1-1.el7.x86_64.rpm
      - https://github.com/cybertec-postgresql/vip-manager/releases/download/v0.6/vip-manager_0.6-1_amd64.rpm
      - http://guichaz.free.fr/polysh/files/polysh-0.4-1.noarch.rpm





    #------------------------------------------------------------------------------
    # NODE PROVISION
    #------------------------------------------------------------------------------
    # this section defines how to provision nodes

    # - node dns - #
    node_dns_hosts: # static dns records in /etc/hosts
      - 10.10.10.10 yum.pigsty
    node_dns_server: add                          # add (default) | none (skip) | overwrite (remove old settings)
    node_dns_servers: # dynamic nameserver in /etc/resolv.conf
      - 10.10.10.10
    node_dns_options: # dns resolv options
      - options single-request-reopen timeout:1 rotate
      - domain service.consul

    # - node repo - #
    node_repo_method: local                       # none|local|public (use local repo for production env)
    node_repo_remove: true                        # whether remove existing repo
    # local repo url (if method=local, make sure firewall is configured or disabled)
    node_local_repo_url:
      - http://yum.pigsty/pigsty.repo

    # - node packages - #
    node_packages: # common packages for all nodes
      - wget,yum-utils,ntp,chrony,tuned,uuid,lz4,vim-minimal,make,patch,bash,lsof,wget,unzip,git,readline,zlib,openssl
      - numactl,grubby,sysstat,dstat,iotop,bind-utils,net-tools,tcpdump,socat,ipvsadm,telnet,tuned,pv,jq
      - python3,python3-psycopg2,python36-requests,python3-etcd,python3-consul
      - python36-urllib3,python36-idna,python36-pyOpenSSL,python36-cryptography
      - node_exporter,consul,consul-template,etcd,haproxy,keepalived,vip-manager
    node_extra_packages: # extra packages for all nodes
      - patroni,patroni-consul,patroni-etcd,pgbouncer,pgbadger,pg_activity
    node_meta_packages: # packages for meta nodes only
      - grafana,prometheus2,alertmanager,nginx_exporter,blackbox_exporter,pushgateway
      - dnsmasq,nginx,ansible,pgbadger,polysh

    # - node features - #
    node_disable_numa: false                      # disable numa, important for production database, reboot required
    node_disable_swap: false                      # disable swap, important for production database
    node_disable_firewall: true                   # disable firewall (required if using kubernetes)
    node_disable_selinux: true                    # disable selinux  (required if using kubernetes)
    node_static_network: true                     # keep dns resolver settings after reboot
    node_disk_prefetch: false                     # setup disk prefetch on HDD to increase performance

    # - node kernel modules - #
    node_kernel_modules:
      - softdog
      - br_netfilter
      - ip_vs
      - ip_vs_rr
      - ip_vs_rr
      - ip_vs_wrr
      - ip_vs_sh
      - nf_conntrack_ipv4

    # - node tuned - #
    node_tune: tiny                               # install and activate tuned profile: none|oltp|olap|crit|tiny
    node_sysctl_params: # set additional sysctl parameters, k:v format
      net.bridge.bridge-nf-call-iptables: 1       # for kubernetes

    # - node user - #
    node_admin_setup: true                        # setup an default admin user ?
    node_admin_uid: 88                            # uid and gid for admin user
    node_admin_username: admin                    # default admin user
    node_admin_ssh_exchange: true                 # exchange ssh key among cluster ?
    node_admin_pks: # public key list that will be installed
      - 'ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAAAgQC7IMAMNavYtWwzAJajKqwdn3ar5BhvcwCnBTxxEkXhGlCO2vfgosSAQMEflfgvkiI5nM1HIFQ8KINlx1XLO7SdL5KdInG5LIJjAFh0pujS4kNCT9a5IGvSq1BrzGqhbEcwWYdju1ZPYBcJm/MG+JD0dYCh8vfrYB/cYMD0SOmNkQ== vagrant@pigsty.com'

    # - node ntp - #
    node_ntp_service: ntp                         # ntp or chrony
    node_ntp_config: true                         # overwrite existing ntp config?
    node_timezone: Asia/Shanghai                  # default node timezone
    node_ntp_servers: # default NTP servers
      - pool cn.pool.ntp.org iburst
      - pool pool.ntp.org iburst
      - pool time.pool.aliyun.com iburst
      - server 10.10.10.10 iburst


    #------------------------------------------------------------------------------
    # META PROVISION
    #------------------------------------------------------------------------------
    # - ca - #
    ca_method: create                             # create|copy|recreate
    ca_subject: "/CN=root-ca"                     # self-signed CA subject
    ca_homedir: /ca                               # ca cert directory
    ca_cert: ca.crt                               # ca public key/cert
    ca_key: ca.key                                # ca private key

    # - nginx - #
    nginx_upstream:
      - {name: home,           host: pigsty,   url: "127.0.0.1:3000"}
      - { name: consul,        host: c.pigsty, url: "127.0.0.1:8500" }
      - { name: grafana,       host: g.pigsty, url: "127.0.0.1:3000" }
      - { name: prometheus,    host: p.pigsty, url: "127.0.0.1:9090" }
      - { name: alertmanager,  host: a.pigsty, url: "127.0.0.1:9093" }

    # - nameserver - #
    dns_records: # dynamic dns record resolved by dnsmasq
      - 10.10.10.2  pg-meta                       # sandbox vip for pg-meta
      - 10.10.10.3  pg-test                       # sandbox vip for pg-test
      - 10.10.10.10 meta-1                        # sandbox node meta-1 (node-0)
      - 10.10.10.11 node-1                        # sandbox node node-1
      - 10.10.10.12 node-2                        # sandbox node node-2
      - 10.10.10.13 node-3                        # sandbox node node-3
      - 10.10.10.10 pigsty
      - 10.10.10.10 y.pigsty yum.pigsty
      - 10.10.10.10 c.pigsty consul.pigsty
      - 10.10.10.10 g.pigsty grafana.pigsty
      - 10.10.10.10 p.pigsty prometheus.pigsty
      - 10.10.10.10 a.pigsty alertmanager.pigsty
      - 10.10.10.10 n.pigsty ntp.pigsty

    # - prometheus - #
    prometheus_scrape_interval: 2s                # global scrape & evaluation interval (2s for dev, 15s for prod)
    prometheus_scrape_timeout: 1s                 # global scrape timeout (1s for dev, 1s for prod)
    prometheus_metrics_path: /metrics             # default metrics path (only affect job 'pg')
    prometheus_data_dir: /export/prometheus/data  # prometheus data dir
    prometheus_retention: 30d                     # how long to keep

    # - grafana - #
    grafana_url: http://admin:admin@10.10.10.10:3000 # grafana url
    grafana_admin_password: admin                  # default grafana admin user password
    grafana_plugin: install                        # none|install|reinstall
    grafana_cache: /www/pigsty/grafana/plugins.tar.gz # path to grafana plugins tarball
    grafana_customize: true                        # customize grafana resources
    grafana_plugins: # default grafana plugins list
      - redis-datasource
      - simpod-json-datasource
      - fifemon-graphql-datasource
      - sbueringer-consul-datasource
      - camptocamp-prometheus-alertmanager-datasource
      - ryantxu-ajax-panel
      - marcusolsson-hourly-heatmap-panel
      - michaeldmoore-multistat-panel
      - marcusolsson-treemap-panel
      - pr0ps-trackmap-panel
      - dalvany-image-panel
      - magnesium-wordcloud-panel
      - cloudspout-button-panel
      - speakyourcode-button-panel
      - jdbranham-diagram-panel
      - grafana-piechart-panel
      - snuids-radar-panel
      - digrich-bubblechart-panel
    grafana_git_plugins:
      - https://github.com/Vonng/grafana-echarts



    #------------------------------------------------------------------------------
    # DCS PROVISION
    #------------------------------------------------------------------------------
    dcs_type: consul                              # consul | etcd | both
    dcs_name: pigsty                              # consul dc name | etcd initial cluster token
    # dcs server dict in name:ip format
    dcs_servers:
      meta-1: 10.10.10.10                         # you could use existing dcs cluster
      # meta-2: 10.10.10.11                       # host which have their IP listed here will be init as server
      # meta-3: 10.10.10.12                       # 3 or 5 dcs nodes are recommend for production environment

    dcs_exists_action: skip                       # abort|skip|clean if dcs server already exists
    consul_data_dir: /var/lib/consul              # consul data dir (/var/lib/consul by default)
    etcd_data_dir: /var/lib/etcd                  # etcd data dir (/var/lib/consul by default)


    #------------------------------------------------------------------------------
    # POSTGRES INSTALLATION
    #------------------------------------------------------------------------------
    # - dbsu - #
    pg_dbsu: postgres                             # os user for database, postgres by default (change it is not recommended!)
    pg_dbsu_uid: 26                               # os dbsu uid and gid, 26 for default postgres users and groups
    pg_dbsu_sudo: limit                           # none|limit|all|nopass (Privilege for dbsu, limit is recommended)
    pg_dbsu_home: /var/lib/pgsql                  # postgresql binary
    pg_dbsu_ssh_exchange: false                   # exchange ssh key among same cluster

    # - postgres packages - #
    pg_version: 13                                # default postgresql version
    pgdg_repo: false                              # use official pgdg yum repo (disable if you have local mirror)
    pg_add_repo: false                            # add postgres related repo before install (useful if you want a simple install)
    pg_bin_dir: /usr/pgsql/bin                    # postgres binary dir
    pg_packages:
      - postgresql${pg_version}*
      - postgis31_${pg_version}*
      - pgbouncer patroni pg_exporter pgbadger
      - patroni patroni-consul patroni-etcd pgbouncer pgbadger pg_activity
      - python3 python3-psycopg2 python36-requests python3-etcd python3-consul
      - python36-urllib3 python36-idna python36-pyOpenSSL python36-cryptography

    pg_extensions:
      - pg_repack${pg_version} pg_qualstats${pg_version} pg_stat_kcache${pg_version} wal2json${pg_version}
      # - ogr_fdw${pg_version} mysql_fdw_${pg_version} redis_fdw_${pg_version} mongo_fdw${pg_version} hdfs_fdw_${pg_version}
      # - count_distinct${version}  ddlx_${version}  geoip${version}  orafce${version}                                   # popular features
      # - hypopg_${version}  ip4r${version}  jsquery_${version}  logerrors_${version}  periods_${version}  pg_auto_failover_${version}  pg_catcheck${version}
      # - pg_fkpart${version}  pg_jobmon${version}  pg_partman${version}  pg_prioritize_${version}  pg_track_settings${version}  pgaudit15_${version}
      # - pgcryptokey${version}  pgexportdoc${version}  pgimportdoc${version}  pgmemcache-${version}  pgmp${version}  pgq-${version}  pgquarrel pgrouting_${version}
      # - pguint${version}  pguri${version}  prefix${version}   safeupdate_${version}  semver${version}   table_version${version}  tdigest${version}



    #------------------------------------------------------------------------------
    # POSTGRES PROVISION
    #------------------------------------------------------------------------------
    # - identity - #
    # pg_cluster:                                 # [REQUIRED] cluster name (validated during pg_preflight)
    # pg_seq: 0                                   # [REQUIRED] instance seq (validated during pg_preflight)
    # pg_role: replica                            # [REQUIRED] service role (validated during pg_preflight)
    pg_hostname: false                            # overwrite node hostname with pg instance name
    pg_nodename: true                             # overwrite consul nodename with pg instance name

    # - retention - #
    # pg_exists_action, available options: abort|clean|skip
    #  - abort: abort entire play's execution (default)
    #  - clean: remove existing cluster (dangerous)
    #  - skip: end current play for this host
    # pg_exists: false                            # auxiliary flag variable (DO NOT SET THIS)
    pg_exists_action: clean

    # - storage - #
    pg_data: /pg/data                             # postgres data directory
    pg_fs_main: /export                           # data disk mount point     /pg -> {{ pg_fs_main }}/postgres/{{ pg_instance }}
    pg_fs_bkup: /var/backups                      # backup disk mount point   /pg/* -> {{ pg_fs_bkup }}/postgres/{{ pg_instance }}/*

    # - connection - #
    pg_listen: '0.0.0.0'                          # postgres listen address, '0.0.0.0' by default (all ipv4 addr)
    pg_port: 5432                                 # postgres port (5432 by default)

    # - patroni - #
    # patroni_mode, available options: default|pause|remove
    #   - default: default ha mode
    #   - pause:   into maintenance mode
    #   - remove:  remove patroni after bootstrap
    patroni_mode: default                         # pause|default|remove
    pg_namespace: /pg                             # top level key namespace in dcs
    patroni_port: 8008                            # default patroni port
    patroni_watchdog_mode: automatic              # watchdog mode: off|automatic|required
    pg_conf: tiny.yml                             # user provided patroni config template path

    # - pgbouncer - #
    pgbouncer_port: 6432                          # default pgbouncer port
    pgbouncer_poolmode: transaction               # default pooling mode: transaction pooling
    pgbouncer_max_db_conn: 100                    # important! do not set this larger than postgres max conn or conn limit

    # - template - #
    pg_init: pg-init                              # init script for cluster template

    # - system roles - #
    pg_replication_username: replicator           # system replication user
    pg_replication_password: DBUser.Replicator    # system replication password
    pg_monitor_username: dbuser_monitor           # system monitor user
    pg_monitor_password: DBUser.Monitor           # system monitor password
    pg_admin_username: dbuser_admin               # system admin user
    pg_admin_password: DBUser.Admin               # system admin password

    # - default roles - #
    pg_default_roles:
      - username: dbrole_readonly                 # sample user:
        options: NOLOGIN                          # role can not login
        comment: role for readonly access         # comment string

      - username: dbrole_readwrite                # sample user: one object for each user
        options: NOLOGIN
        comment: role for read-write access
        groups: [ dbrole_readonly ]               # read-write includes read-only access

      - username: dbrole_admin                    # sample user: one object for each user
        options: NOLOGIN BYPASSRLS                # admin can bypass row level security
        comment: role for object creation
        groups: [dbrole_readwrite,pg_monitor,pg_signal_backend]

      # NOTE: replicator, monitor, admin password are overwrite by separated config entry
      - username: postgres                        # reset dbsu password to NULL (if dbsu is not postgres)
        options: SUPERUSER LOGIN
        comment: system superuser

      - username: replicator
        options: REPLICATION LOGIN
        groups: [pg_monitor, dbrole_readonly]
        comment: system replicator

      - username: dbuser_monitor
        options: LOGIN CONNECTION LIMIT 10
        comment: system monitor user
        groups: [pg_monitor, dbrole_readonly]

      - username: dbuser_admin
        options: LOGIN BYPASSRLS
        comment: system admin user
        groups: [dbrole_admin]

      - username: dbuser_stats
        password: DBUser.Stats
        options: LOGIN
        comment: business read-only user for statistics
        groups: [dbrole_readonly]


    # object created by dbsu and admin will have their privileges properly set
    pg_default_privilegs:
      - GRANT USAGE                         ON SCHEMAS   TO dbrole_readonly
      - GRANT SELECT                        ON TABLES    TO dbrole_readonly
      - GRANT SELECT                        ON SEQUENCES TO dbrole_readonly
      - GRANT EXECUTE                       ON FUNCTIONS TO dbrole_readonly
      - GRANT INSERT, UPDATE, DELETE        ON TABLES    TO dbrole_readwrite
      - GRANT USAGE,  UPDATE                ON SEQUENCES TO dbrole_readwrite
      - GRANT TRUNCATE, REFERENCES, TRIGGER ON TABLES    TO dbrole_admin
      - GRANT CREATE                        ON SCHEMAS   TO dbrole_admin
      - GRANT USAGE                         ON TYPES     TO dbrole_admin

    # schemas
    pg_default_schemas: [monitor]

    # extension
    pg_default_extensions:
      - { name: 'pg_stat_statements',  schema: 'monitor' }
      - { name: 'pgstattuple',         schema: 'monitor' }
      - { name: 'pg_qualstats',        schema: 'monitor' }
      - { name: 'pg_buffercache',      schema: 'monitor' }
      - { name: 'pageinspect',         schema: 'monitor' }
      - { name: 'pg_prewarm',          schema: 'monitor' }
      - { name: 'pg_visibility',       schema: 'monitor' }
      - { name: 'pg_freespacemap',     schema: 'monitor' }
      - { name: 'pg_repack',           schema: 'monitor' }
      - name: postgres_fdw
      - name: file_fdw
      - name: btree_gist
      - name: btree_gin
      - name: pg_trgm
      - name: intagg
      - name: intarray

    # postgres host-based authentication rules
    pg_hba_rules:
      - title: allow meta node password access
        role: common
        rules:
          - host    all     all                         10.10.10.10/32      md5

      - title: allow intranet admin password access
        role: common
        rules:
          - host    all     +dbrole_admin               10.0.0.0/8          md5
          - host    all     +dbrole_admin               172.16.0.0/12       md5
          - host    all     +dbrole_admin               192.168.0.0/16      md5

      - title: allow intranet password access
        role: common
        rules:
          - host    all             all                 10.0.0.0/8          md5
          - host    all             all                 172.16.0.0/12       md5
          - host    all             all                 192.168.0.0/16      md5

      - title: allow local read-write access (local production user via pgbouncer)
        role: common
        rules:
          - local   all     +dbrole_readwrite                               md5
          - host    all     +dbrole_readwrite           127.0.0.1/32        md5

      - title: allow read-only user (stats, personal) password directly access
        role: replica
        rules:
          - local   all     +dbrole_readonly                               md5
          - host    all     +dbrole_readonly           127.0.0.1/32        md5

    # pgbouncer host-based authentication rules
    pgbouncer_hba_rules:
      - title: local password access
        role: common
        rules:
          - local  all          all                                     md5
          - host   all          all                     127.0.0.1/32    md5

      - title: intranet password access
        role: common
        rules:
          - host   all          all                     10.0.0.0/8      md5
          - host   all          all                     172.16.0.0/12   md5
          - host   all          all                     192.168.0.0/16  md5

    #------------------------------------------------------------------------------
    # MONITOR PROVISION
    #------------------------------------------------------------------------------
    # - monitor options -
    pg_exporter_config: pg_exporter-demo.yaml     # default config files for pg_exporter
    node_exporter_port: 9100                      # default port for node exporter
    pg_exporter_port: 9630                        # default port for pg exporter
    pgbouncer_exporter_port: 9631                 # default port for pgbouncer exporter
    exporter_metrics_path: /metrics               # default metric path for pg related exporter
    pg_localhost: /var/run/postgresql             # localhost unix socket path


    #------------------------------------------------------------------------------
    # PROXY PROVISION
    #------------------------------------------------------------------------------
    # - haproxy - #
    haproxy_enabled: true                         # enable haproxy among every cluster members
    haproxy_policy: leastconn                     # roundrobin, leastconn
    haproxy_admin_username: admin                 # default haproxy admin username
    haproxy_admin_password: admin                 # default haproxy admin password
    haproxy_client_timeout: 3h                    # client side connection timeout
    haproxy_server_timeout: 3h                    # server side connection timeout
    haproxy_exporter_port: 9101                   # default admin/exporter port
    haproxy_check_port: 8008                      # default health check port (patroni 8008 by default)
    haproxy_primary_port: 5433                    # default primary port 5433
    haproxy_replica_port: 5434                    # default replica port 5434
    haproxy_backend_port: 6432                    # default target port: pgbouncer:6432 postgres:5432

    # - vip - #
    # vip_enabled: true                             # level2 vip requires primary/standby under same switch
    # vip_address: 127.0.0.1                      # virtual ip address ip/cidr
    # vip_cidrmask: 32                            # virtual ip address cidr mask
    # vip_interface: eth0                         # virtual ip network interface

...
```