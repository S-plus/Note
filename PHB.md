# 记录系统开发
## 开发环境
    1．内网状态
    2．CentOS-7-x86_64-Everything-1708（以下简称CentOS）
    3. Python3.6.4（以下简称Python3）
    4．Django2.0.3（无特殊说明时以下简称Django）
    5．Httpd-2.4.6-67.el7.centos.x86_64(为CentOS7系统自带)
    6．Mysql
## 环境安装
### CentOS7
安装环境各有不同，这里不再赘述
### Python3.6.4
参考资料：https://www.cnblogs.com/JahanGu/p/7452527.html</br>
由于CentOS7自带Python2.7.5但是Django2.x不再支持Python3.4前的版本故要考虑Python版本兼容问题
安装Python3前需要先安装一些开发包，CentOS没有自带
#### 1.安装开发包（有带-devel）前请先安装相应的运行库，如装zlib-devel前先装zlib
需要的包如下：
```
zlib-devel
bzip2-devel
openssl-devel
ncurses-devel
sqlite-devel
readline-devel
tk-devel
gcc
make
```
由于是内网环境，所有安装都用rpm –ivh实现
#### 2.到官网下载Python3安装包
解压
```
tar –xvJf Python-3.6.4.tar.xz
```
进入解压后的目录下编译安装
```
cd Python-3.6.4
./configure prefix=/(python安装目录)
make && make install
```
设置软连接
```
ln –s /(python安装目录)/bin/python3 /usr/bin/python
```
修改yum配置
```
vi /usr/bin/yum
```
把`#! /usr/bin/python` 修改为 `#! /usr/bin/python2`
同理` vi /usr/libexec/urlgrabber-ext-down `文件里的 `#! /usr/bin/python` 也要改为`#! /user/bin/python2`
### Django安装
参考资料：</br>
http://blog.csdn.net/zhengwei125/article/details/65443959</br>
http://blog.csdn.net/darongzi1314/article/details/78413455

安装前先安装pytz运行库，注：建议下载tar.gz格式解压后使用`python setup.py install`
```
Python setup.py install
```
安装好后在命令行内输入Python进入Python环境输入
```python
Import django
django.VERSION
```
如果有版本号出来说明Django安装成功</br>
设置软连接
```
ln –s /(python安装目录)/lib/python3.6/site-packages/Django-2.0.3-y3.6.egg/django/bin/django-admin.py /usr/local/bin
```
然后到项目目标目录下执行
```
django-admin.py startproject (项目名称)
```
运行
```
python manage.py runserver 
```
打开服务器浏览器输入127.0.0.1:8000测试是否成功  
修改app`settings.py`文件中的`ALLOWED_HOSTS = ['*']`  
### 修改防火墙配置  
查看防火墙状态  
```
firewall-cmd --state
```
开放端口
```
firewall-cmd --zone=public --add-port=(所需的端口)/tcp --permanent  //--permanent永久生效，没有此参数重启后失效
```
重新载入
```
firewall-cmd --reload
```
查看开放的端口  
```
firewall-cmd --zone=public --list-ports
```
到项目目录下启动服务
```
python manage.py 0.0.0.0:(端口)
```
在服务器下的终端浏览器上输入服务器及开放的端口进行测试

