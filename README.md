## apache-webdav

How to configure apache webdav service?

### Install Apache 

Install from reposity(Ubuntu)

```bash
sudo apt-get install apache2 apache2-utils
```

### Start | Stop Apache

start command

```bash
 /etc/init.d/apache2 start
```

stop command

```bash
 /etc/init.d/apache2 stop
```

log directory:```/var/log/apache2/```

### Configure Webdav
* Add modules that you need by using ```a2enmod``` tool.
```bash
a2enmod dav
a2enmod dav_fs
a2enmod dav_lock
a2enmod alias
a2enmod auth_digest
a2enmod auth_core
a2enmod authn_core
a2enmod authn_file
a2enmod authz_core
a2enmod authz_user
a2enmod authz_setenvif
a2enmod setenvif
```

* Modify configure file
	* [apache2.conf](apache2.conf)
	* [sites-enabled/001-default.conf](sites-enabled/001-default.conf)

* Add user authentication(optional)
	* use htpasswd
```bash
htpasswd -cm file_path user_name
```

* Restart Apache
```bash
/etc/init.d/apache2 restart
```

### Webdav Client

You can use browser or ```cadaver``` tool to access webdav service.

* Install cadaver command
```bash
sudo apt-get install cadaver
```

* Use ```cadaver``` tool
```bash
cadaver http://127.0.0.1:8080/webdav/
```

## 签发证书，构建HTTPS服务

使用```openssl```工具可以自己签发证书，生成```.pem```和```.key```搭建https服务
命令
```bash
openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mykey.key -out mycert.pem
```

### 生成的证书中包含IP

使用[openssl.cnf](openssl/openssl.cnf)生成证书包含IP命令
```bash
openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mykey.key -out mycert.pem -config openssl.cnf
```

### 生成的证书保证机器可信任（添加安全例外）

* 客户端浏览器点击添加例外

* 客户端系统（Ubuntu）添加例外
使用Ubuntu的```update-ca-certificates```工具添加例外，将想要添加例外的网站```.pem```文件位置（本地文件系统）添加到```/etc/ca-certificates.conf```文件最后，然后运行```update-ca-certificates```命令

* 客户端系统（Centos）添加例外
使用Centos的```ca-certificates```工具添加例外，将想要添加例外的网站```.pem```文件放到```/etc/pki/ca-trust/source/anchors/```文件夹下，然后运行```update-ca-trust```命令
