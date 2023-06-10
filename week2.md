# https憑證申請

## 安裝套件
```
yum install epel-release mod_ssl certbot
```
## 申請ipv6的憑證
```
certbot certonly --webroot -w /var/www/html -d kaifneg273.dynv6.net --email s1109105128student.nqu.edu.tw --agree-tos
```
##縮短指令
```
certbot --apache -d kaifeng273.dynv6.net
```
