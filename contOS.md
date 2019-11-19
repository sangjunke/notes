## 服务器centOS环境配置 安装node mongodb nginx 
### node 安装
*  一.安装wget
>* yum install -y wget
* 二.下载node最新的安装包
>* wget https://npm.taobao.org/mirrors/node/v12.13.0/node-v12.13.0-linux-x64.tar.xz
* 三.依次执行下面命令解压安装包
>* xz -d node-v12.13.0-linux-x64.tar.xz _安装xz:yum install xz_
>* tar -xf node-v12.13.0-linux-x64.tar
* 部署
>* ln -s ~/node-v12.13.0-linux-x64/bin/node /usr/bin/node
>* ln -s ~/node-v12.13.0-linux-x64/bin/npm /usr/bin/npm
* 测试
>* node -v
>* npm -v
### 安装mongodb
* 创建yum源文件
>* #cd /etc/yum.repos.d
>* #vim mongodb-org-4.0.repo 
* 添加以下内容
```
[mngodb-org]
name=MongoDB Repository
baseurl=http://mirrors.aliyun.com/mongodb/yum/redhat/7Server/mongodb-org/4.0/x86_64/
gpgcheck=0
enabled=1
<!-- 这里可以修改 gpgcheck=0, 省去gpg验证 -->
```
* 更新包
>* yum update
* 安装mongodb
>* yum -y install mongodb-org
* 启动/查看服务
>* systemctl start mongod.service
>* systemctl status mongod.service
* 查看端口状态
>* netstat -ntlp
* 关闭端口
>* netstat -anp 查看端口详情
>* kill -9 PID 杀掉进程
* 运行mongodb
>* mongo
>* show dbs
* 配置远程连接
* 编辑 mongod.conf 配置
>* vi /etc/mongod.conf
>* 将 bindIp: 127.0.0.1 改成 bindIp: 0.0.0.0，注意 tab 和空格对齐
* 开放端口　
>* firewall-cmd --zone=public --add-port=27017/tcp --permanent
>* firewall-cmd --reload
>* firewall-cmd --zone=public --query-port=27017/tcp
>* 如果提示 _FirewallD is not running_, _systemctl status firewalld_ 查看firewalld状态,发现当前是dead状态，即防火墙未开启。_systemctl start firewalld_ 开启防火墙
* 重启服务
>* systemctl restart mongod.service
* 创建管理员
>* db.createUser({user: "sangjk",pwd: "sangjunke..",roles: [ { role: "root", db: "admin" }]})
* 开启权限认证
>* vi /etc/mongod.conf
>* 找到 #security: ，改成如下开启安全认证：
```
security:
　　authorization: enabled
```
>* 一定注意格式 tap和空格 ！！！
* 重启服务
>* systemctl restart mongod.service
### 安装nginx
* #使用以下命令
* sudo yum install -y nginx
* #sudo表示使用管理员权限运行命令
* #yum是centos系统中下载安装程序的命令
* #如果提示中发现yum资源库中没用Nginx的话，则使用以下命令进行添加
* sudo rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
* 启动nginx
>* nginx
* 停止服务
* nginx -s stop
* 如果上面停止nginx的方式无效 可以强制停止 _pkill -9 nginx_
* 重启nginx 
>* nginx -s reload
* 由于在Linux下写配置文件，容易丢个符号，导致启动失败，所以启动之前可以检查一下配置文件的正确性
>* nginx -t
* 修改配置文件
>* 文档:https://www.cnblogs.com/alvin-niu/p/9502271.html
