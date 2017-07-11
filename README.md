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
* Add modules that you need
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

* Use ```cadaver```
```bash
cadaver http://127.0.0.1:8080/webdav/
```

