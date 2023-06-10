# Docker_file
## 1. 建立 test-dockerfile 資料夾
```
mkdir test-dockerfile
```
## 2. 建立 DockerFile 檔案
```
gedit Dockerfile
```
內容
```
FROM centos:7.9.2009
RUN yum -y install httpd
EXPOSE 80
ADD index.html /var/www/html
```
## 3. 建立首頁
```
echo "kaifeng" > index.html
```
## 4. 執行 Docker
```
systemctl start docker
```
## 5. 執行建構
```
docker build -t roy:httpd .
```
## 6. 執行鏡像檔
```
docker run -d -p 8888:80 roy:httpd /usr/sbin/apachectl -DFOREGROUND
```
# Docker-Compose
## 1. 下載
```
curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
## 2. 給予執行權限
```
chmod +x /usr/local/bin/docker-compose
```
## 3. 建立資料夾
```
mkdir test-dockercompose
```
## 4. 建立 docker-compose.yml 檔案
```
gedit docker-compose.yml
```
內容
```
version: '3'
services:
  web:
    image: "roy:httpd"
    ports: 
      - "8899:80"
    command: "/usr/sbin/apachectl -DFOREGROUND"
```
## 5. 執行docker-compose
```
docker-compose up -d
```
