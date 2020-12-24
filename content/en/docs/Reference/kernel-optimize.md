---
title: "OS Kernel Parameters"
linkTitle: "OS Kernel Parameters"
weight: 2
date: 2020-11-15
description: >
  How os kernel parameters is optimized in pigsty 
---

# Database kernel optimisation


```bash
# Database kernel optimisation
fs.aio-max-nr = 1048576 # 限制并发未完成的异步请求数目，，不应小于1M
fs.file-max = 16777216  # 最大打开16M个文件

# kernel
kernel.shmmax = 485058		# 共享内存最大页面数量: $(expr $(getconf _PHYS_PAGES) / 2)
kernel.shmall = 1986797568 	# 共享内存总大小： $(expr $(getconf _PHYS_PAGES) / 2 \* $(getconf PAGE_SIZE))
kernel.shmmni = 16384 		# 系统范围内共享内存段的最大数量 4096 -> 16384
kernel.msgmni = 32768		# 系统的消息队列数目,影响可以启动的代理程序数 设为内存MB数
kernel.msgmnb = 65536		# 影响队列的大小
kernel.msgmax = 65536		# 影响队列中可以发送的消息的大小
kernel.numa_balancing = 0   # Numa禁用
kernel.sched_migration_cost_ns = 5000000 # 5ms内，调度认为进程还是Hot的。
kernel.sem = 2048 134217728 2048 65536   # 每个信号集最大信号量2048，系统总共可用信号量134217728，单次最大操作2048，信号集总数65536

# vm
vm.dirty_ratio = 80                       # 绝对限制，超过80%阻塞写请求刷盘
vm.dirty_background_bytes = 268435456     # 256MB脏数据唤醒刷盘进程
vm.dirty_expire_centisecs = 6000          # 1分钟前的数据被认为需要刷盘
vm.dirty_writeback_centisecs= 500         # 刷新进程运行间隔5秒
vm.mmap_min_addr = 65536                  # 禁止访问0x10000下的内存
vm.zone_reclaim_mode = 0                  # Numa禁用

# vm swap
vm.swappiness = 0                         # 禁用SWAP，但高水位仍会有
vm.overcommit_memory = 2                  # 允许一定程度的Overcommit
vm.overcommit_ratio = 50                  # 允许的Overcommit:$((($mem - $swap) * 100 / $mem))

# tcp memory
net.ipv4.tcp_rmem = 8192 65536 16777216		# tcp读buffer: 32M/256M/16G
net.ipv4.tcp_wmem = 8192 65536 16777216		# tcp写buffer: 32M/256M/16G
net.ipv4.tcp_mem = 131072 262144 16777216	# tcp 内存使用 512M/1G/16G
net.core.rmem_default = 262144      		# 接受缓冲区默认大小: 256K
net.core.rmem_max = 4194304         		# 接受缓冲区最大大小: 4M
net.core.wmem_default = 262144      		# 发送缓冲区默认大小: 256K
net.core.wmem_max = 4194304         		# 发送缓冲区最大大小: 4M
# tcp keepalive
net.ipv4.tcp_keepalive_intvl = 20	# 探测没有确认时，重新发送探测的频度。默认75s -> 20s
net.ipv4.tcp_keepalive_probes = 3	# 3 * 20 = 1分钟超时断开
net.ipv4.tcp_keepalive_time = 60	# 探活周期1分钟
# tcp port resure
net.ipv4.tcp_tw_reuse = 1           # 允许将TIME_WAIT socket用于新的TCP连接。默认为0
net.ipv4.tcp_tw_recycle = 0			# 快速回收，已弃用
net.ipv4.tcp_fin_timeout = 5        # 保持在FIN-WAIT-2状态的秒时间
net.ipv4.tcp_timestamps = 1
# tcp anti-flood
net.ipv4.tcp_syncookies = 1			# SYN_RECV队列满后发cookie，防止恶意攻击
net.ipv4.tcp_synack_retries = 1		# 收到不完整sync后的重试次数 5->2
net.ipv4.tcp_syn_retries = 1         #表示在内核放弃建立连接之前发送SYN包的数量。
# tcp load-balancer
net.ipv4.ip_forward = 1						# IP转发
net.ipv4.ip_nonlocal_bind = 1				# 绑定非本机地址
net.netfilter.nf_conntrack_max = 1048576	# 最大跟踪连接数
net.ipv4.ip_local_port_range = 10000 65535	# 端口范围
net.ipv4.tcp_max_tw_buckets = 262144		# 256k  TIME_WAIT
net.core.somaxconn = 65535          		# 限制LISTEN队列最大数据包量，触发重传机制。
net.ipv4.tcp_max_syn_backlog = 8192 		# SYN队列大小：1024->8192
net.core.netdev_max_backlog = 8192			# 网卡收包快于内核时，允许队列长度

```