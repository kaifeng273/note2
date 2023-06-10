# webdav 架設
## 安裝第三方資料庫
```
yum install epel-release
```
## 檢查http是否有支援Webdav
```
httpd -M | grep dav
```
## 於html 資料夾下創建 webdav 資料夾並修改權限
```
cd /var/www/html
mkdir webdav
chown -R apache:apache /var/www/html
chmod -R 755 /var/www/html 
```
## 編輯配置檔
```
vim /etc/httpd/conf.d/webdav.conf
```
###配置檔內容
```
DavLockDB /var/www/html/DavLock
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html/webdav/
    ErrorLog /var/log/httpd/error.log
    CustomLog /var/log/httpd/access.log combined
    Alias /webdav /var/www/html/webdav
    <Directory /var/www/html/webdav>
        DAV On
        #AuthType Basic
        #AuthName "webdav"
        #AuthUserFile /etc/httpd/.htpasswd
        #Require valid-user
        </Directory>
</VirtualHost>
```
## 開啟http
```
$ systemctl restart httpd
```
