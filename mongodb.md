## mongodb安装和配置
### 安装
* 官网地址：https://www.mongodb.com/download-center/community
* 下载完成进行安装
* Choose Setup Type 选择(自定义)
* __注:install MongiDB Compass  有点耗时间，可以取消__
* MongoDB的数据目录存储在 db 目录下。但是这个目录不会在安装之后主动创建，需要我们在安装完成后手动创建它【就是手动创建一个文件夹】。例如我在c盘装MongoDB，则在同级目录新建 data 目录 和 log 目录
* 配置数据库目录和日志目录
>* 1.win标+r 以管理员身份打开命令窗口 
>* 2.切换至mongoDB的bin目录下,输入命令
>>* mongod --dbpath 数据目录(C:\Program Files\Data\db)
>>* mongod  –logpath C:\Program Files\Data\log\mongod.log
>* 3.浏览器打开 http://localhost:27017/ 出现如下：It looks like you are trying to access MongoDB over HTTP on the native driver port.  则证明连接成功
* 配置数据库权限
>* 新打开命令行工具,切换至mongoDB的bin目录下，命令行输入
>>* mongod --dbpath "D:\Program Files\mongodb\data\db" --logpath "D:\Program Files\mongodb\data\log\MongoDB.log" --auth
>* 带有-auth参数时，必须通过认证才可以查询数据。如果没有加-auth参数，即使配置了安全认证用户，也不需要认证谁都可以操作。
>* 创建用户
>* 命令行工具至mongoDB的bin目录下，使用mongo.exe进入mongo命令行
>* use test __存在test数据库就打开，不存在就创建test数据库__
>* db.createUser({user:'admin', pwd:'123456',roles:[{role:'root',db:'test'}]})    _有的说是db.addUser 但我的不行 可能是mongo得版本不一样_
>* use test 切换至数据库
>* show users 可以查看创建的用户