## 解决github访问速度慢或者clone速度慢的问题
###  修改本地hosts文件
* windows系统的hosts文件的位置如下：C:\Windows\System32\drivers\etc\hosts
* mac/linux系统的hosts文件的位置如下：/etc/hosts
### 获取Github相关网站的ip
* 访问 [https://www.ipaddress.com/](https://www.ipaddress.com) 找到页面中下方的“IP Address Tools – Quick Links”
* 分别输入github.global.ssl.fastly.net和github.com，查询ip地址
>* 140.82.114.4     github.com
>* 199.232.5.194 github.global.ssl.fastly.net
* 最后执行ipconfig /flushdns命令，刷新 DNS 缓存。