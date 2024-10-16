### [wireshark网络抓包分析工具](https://zhuanlan.zhihu.com/p/506417526)

[TCP/IP网络模型](TCP-IP网络模型.md)

>常见协议包抓取
>1. ARP协议
>2. ICMP协议
>3. TCP协议
>4. UDP协议
>5. DNS协议
>6. HTTP协议

---

### 混杂模式和普通模式

##### 混杂模式:混杂模式就是接收所有经过网卡的数据包,包括不是发给本机的包,即不验证MAC地址

##### 普通模式: 普通模式下网卡只接收发给本机的包(包括广播包)传递给上层程序,其他包一律丢弃

>一般来说,混在模式不会影响网卡的正常工作,多在网络监听工具上使用

---

#### wireshark过滤器 


#### ARP(Address Resolution Protocol)协议
>地址解析协议
> 根据IP地址获取物理地址的一个TCP/IP协议

ftp抓包筛选

>`ftp.request.command == USER`：显示包含 FTP 用户名请求的数据包 \
`ftp.request.command == PASS`：显示包含 FTP 密码请求的数据包 \
`ftp.request.command == LOGIN`：显示包含 FTP 登录请求的数据包 \
`ftp.request.command == RETR`：显示包含 FTP 文件下载请求的数据包 \
`ftp.request.command == STOR`：显示包含 FTP 文件上传请求的数据包 \
`ftp.request.command == DELE`：显示包含 FTP 文件删除请求的数据包

> ftp and tcp contains "Login"

1. Frame: 物理层的数据帧概况

2. Ethernet II: 数据链路层以太网帧头部信息

3. Internet Protocol Version 4: 互联网层IP包头部信息

4. Transmission Control Protocol: 传输层T的数据段头部信息

5. Hypertext Transfer Protocol: 应用层的信息

![img_11.png](img_11.png)













