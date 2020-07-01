# CentOS-Flask-Nginx-
写个简单的接口
1.云服务器:装好CentOS7，配置安全组策略端口开放，添加一个8899为例；
2.Python3环境:
  (1)下载python压缩包wget https://www.Python.org/ftp/python/3.6.1/Python-3.6.1.tar.xz
  (2)解压tar xJf  Python-3.6.1.tar.xz
  (3)安装解压类库yum -y install zlib*
  (4)进入解压文件夹安装./configure  --prefix=/usr/local/python3 && make && make install
  (5)创建软连接ln -s /usr/local/python3/bin/python3 /usr/bin/python3、ln -s /usr/local/python3/bin/pip3 /usr/bin/pip3
  (5)安装虚拟环境包pip3 install virtualenv
  (6)新建一个目录用于安装虚拟环境进行开发，/lwf为例;
  (7)进入lwf安装虚拟环境 /usr/local/python3/bin/virtualenv  -p /usr/bin/python3 venv，第一个目录表示虚拟环境包命令行所在目录，-p 目录表指定要安装虚拟环境的python版本，安装完后会生成一个venv目录
  (8)激活虚拟环境 source venv/bin/activate
  (9)虚拟环境下安装pip install uwsgi、pip install flask
  (10)进入venv文件夹新建配置文件uwsgi.ini
      [uwsgi]
      # py文件所在目录
      chdir           = /lwf
      callable = app
      # py文件名
      wsgi-file= simpleApi.py
      # 进程数
      processes       = 5
      # 使用8899端口
      http = 0.0.0.0:8899
      pidfile = project-master.pid
  (11)启动uwsgi进程:激活虚拟环境、venv目录下: nohup uwsgi uwsgi.ini &,nohup表断开ssh后uwsgi进程不会挂起,&表后台运行，注意此时直接断开ssh链接进程依然会停止，故需输入exit手动退出ssh即可保持进程运行,杀uwsgi进程:killall -9 uwsgi,查看uwsgi进程:ps -ef | grep uwsgi
2.Nginx:似乎flask自带web服务器，所以nginx用不上了，要的话可以参考https://www.jianshu.com/p/f1acbd401bed


centOS&mysql服务端:
(1)由于yum源没有mysql资源，所以安装：yum -y install wget来下载mysql，下载mysql：wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm ，安装：rpm -ivh mysql-community-release-el7-5.noarch.rpm，最后安装mysql：yum install mysql-server
(2)启动mysql：systemctl start mysqld，查询mysql运行状态：service  mysqld  status

(3)
(4)
(5)
(6)
(7)
(8)
