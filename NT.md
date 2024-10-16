
## IIS 加固
禁止IIS短文件名泄露
>fsutil 8dot3name set 1

## Linux密码策略(满足大小写字母,数字,特殊字符)[/etc/pam.d/system-auth]

`lcredit=-1 ucredit=-1 dcredit=-1 ocredit=-1`

### 解释如下：
lcredit=-1 密码应包含的小写字母的至少一个

ucredit=-1 密码应包含的大写字母至少一个

dcredit=-1 将密码包含的数字至少为一个

ocredit=-1 设置其他符号的最小数量，例如@，＃、! $％等，至少要有一个

enforce_for_root 确保即使是root用户设置密码，也应强制执行复杂性策略。

minlen=10密码最少长度10

minclass=3至少包含小写字母、大写字母、数字、特殊字符等4类字符中等3类

## Linux密码长度不小于8个字符[/etc/login.defs]

* PASS_MAX_DAYS  999  #密码最长有效期
* PASS_MIN_DAYS  0    #更改密码后的等待时间
* PASS_MIN_LEN   8    #密码最小长度
* PASS_WARN_AGE  7    #密码到期前多少天提醒用户

## Linux一分钟仅(允许)5次登录失败，超过5次，登录账号锁定1分钟[/etc/pam.d/login]

`auth   requisite   pam_tall2.so deny=6 unlock_time=60`

## 仅使用证书登录SSH[/etc/ssh/sshd_config]
>PasswordAuthentication yes改为no

>#PubkeyAuthentication yes 取消注释

### SSH服务加固，禁止root远程登录[/etc/ssh/sshd_config]

>在PermitRootLogin下面添加PermitRootLogin no

### 设置root用户的计划任务
>每天早上7.50自动开SSH服务，22.50关闭；每周六的7.30重新启动SSH服务，使用crontab -l 显示

使用crontab -e 编辑

![Alt text](image.png)

## 修改SSH服务端口为2222 使用netstat -anltp | grep sshd 查看信息

>找到#Port22 取消注释 改为2222 重启sshd服务
>报错 输入 sudo semanage port -a -t ssh_port_t -p tcp 2222 或 \
编辑 /etc/selinux/config  设置SELINUX=disable


## 设置数据连接的超时时间为2min[/etc/vsftpd/vsftpd.conf]
后connection后
>data_connection_timeout=120

## 设置站点本地用户访问的最大传输速率为1M[/etc/vsftpd/vsftpd.conf]

>local_max_rate=1048567

## 防火墙策略

## 1. 只允许转发来自172.16.0.0/24局域网段的DNS解析请求数据包
`iptables -A FORWARD -p udp --dport 53 -s 172.16.0.0/24 -j ACCEPT`

## 2. 禁止任何机器ping本机
`iptables -A INPUT -p icmp --icmp-type 8 -j DROP`

## 3. 禁止本机ping任何机器
`iptables -A OUTPUT -p icmp --icmp-type 8 -j DROP`

## 4. 禁用23端口
`iptables -A INPUT -p tcp --dport 23 -j DROP`

`iptables -A INPUT -p udp --dport 23 -j DROP`

## 5. 禁止转发来自MAC地址为29:0E:29:19:65:EF主机的数据包

`iptables -A FORWARD -m mac --mac-source 29:0E:29:19:65:EF -j DROP`

## 6. 为防御IP碎片攻击，设置iptables防火墙策略限制IP碎片的数量，仅允许每秒处理1000个

`iptables -A INPUT -f -m limit --limit 1000/s --limit-burst 1000 -j ACCEPT`

## 7. 为防止SSH服务被暴力枚举，设置iptables防火墙策略仅允许172.16.10.0/24网段内的主机通过SSH连接本机

`iptables -A INPUT -p tcp --dport 22 -s 172.16.10.0/24 -j ACCEPT`

`iptables -A INPUT -p tcp --dport 22 -j DROP`

### 命令解释:

* iptables linux上设置IPv4数据过滤规则的工具
* -A FORWARD 向iptables的FORWARD链添加一条规则 [FORWARD 链是用来处理经过当前设备（作为路由器）转发的数据包]
* -p udp 指定参数匹配的协议是UDP 意味着这条规则只适用于UDP数据包
* --dport 53 指定目的端口为53(DNS)
* -s(source) 172.16.0.0/24 源IP地址的过滤条件
* -j(jump) ACCEPT -j用来指定满足前面条件的数据包该如何处理 ACCEPT表示接受
* -A INPUT [INPUT 链用于处理进入本机的数据包]
* --icmp-type 8 用于指定ICMP消息的类型,类型8是ICMP Echo Request[这是发送 ping 请求时使用的消息类型]
* -j(jump) DROP DROP 表示直接丢弃这些数据包,不给任何响应
* -A OUTPUT [OUTPUT 链用于处理从本机出去的数据包]
* -m mac 这指定使用mac模块 -m参数是告诉iptables使用一个拓展模块
* --mac-source &&& 用于指定源MAC地址 匹配MAC地址为&&&的所有数据包
* -f 这个选项表示匹配分片的数据包。分片是 TCP/IP 协议处理大于最大传输单元（MTU）的数据包的一种方式，大的数据包会被分成更小的片段进行传输
* -m limit：这是一个匹配扩展模块，用于提供速率限制功能。通过这个模块，可以控制匹配特定条件的数据包的处理频率
* --limit 1000/s：这个参数设置了数据包的匹配限制为每秒最多 1000 个数据包。即，该规则只允许最多每秒处理 1000 个匹配的数据包
* --limit-burst 1000：突发限制参数，允许在短时间内处理的数据包数量超过平均速率限制（这里同样是 1000 个数据包）。这意味着在一开始，连续的 1000 个数据包可以被接受，直到达到突发值限制。之后，只有符合设定的平均速率（这里是 1000 个/秒）的数据包才会被接受



