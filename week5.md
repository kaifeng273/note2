# DNS_sever
## 查詢Domain Name對應ip
於 /etc/hosts 或 DNS caches 或DNS server
## linux 查詢工具
### dig
```
$ cat /etc/resolv.conf  
$ dig www.nqu.edu.tw    
$ dig @8.8.8.8 www.nqu.edu.tw
$ dig www.nqu.edu.tw ns 
```
### host
```
host csie.nqu.edu.tw 8.8.8.8
```
## BIND架設
### 1.檢查53號埠是否占用
```
netstat -tunlp | grep 53
```
### 2.檢查 firewalld 、enforce 是否關上
```
getenforce
systemctl status firewalld
```
### 3. Windows 上 Ping Linux IP 看是否成功
### 4. 安裝 bind、bind-chroot、bind-utils
```
yum install bind bind-chroot bind-utils -y
```
### 5.設定配置檔
```
gedit /etc/named.conf
```
```
	listen-on port 53 { any; };
	
	allow-query     { any; };
```
### 6.重新啟動sever
```
systemctl restart named
```
## 管理網域:正向解析
### 1.編輯網域
```
$ vim /var/named/a.com.zone
```
```
$TTL 600 ;10 minutes

@ IN SOA	@ s110910528@student.nqu.edu.tw 
		2021031803 ;serial
		10800      ;refresh
		900        ;retry
		604800     ;expire
		86400      ;minimum
		)
@		NS    dns1.a.com.
dns.com.	A     192.168.129.128 dns1		A     192.168.129.128 
www		A     192.168.129.100  
eshop		CNAME www
ftp		A     192.168.129.200
abc		A     192.168.129.150
```
### 2.編輯 /etc/named.rfc1912.zone
```
$ vim /etc/named.rfc1912.zones
```
```
zone "a.com" IN {
	type master;
	file "a.com.zone";
	allow-update { none; };
};
```
