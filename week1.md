# ipv6架設
## 關閉 enforce firewalld
```
setenforce 0
systemctl stop firewalld
```
## 開啟httpd
```
systemctl start httpd
```
## 確認ipv6位置
```
ifconfig
```
## 連線方式 [位置]/資料夾/檔案(可用dynv6縮短網址)
```
[2401:e180:8d00:32a1:643a:55e8:3be9:d5cd]/webdav/hi.txt
kaifeng.dynv6.net/webdav/hi.txt
```
![](https://github.com/kaifeng273/note2/blob/main/picture/week1/w1.png)
![](https://github.com/kaifeng273/note2/blob/main/picture/week1/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%202023-06-04%20221126.png)
