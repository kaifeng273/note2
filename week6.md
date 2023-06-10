# Docker
## 安裝
### 1.確保沒有Docker
```
yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```
### 2.安裝
```
yum install -y yum-utils
yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```
### 3.開啟Docker
```
systemctl start docker
```
### 4.抓取映像檔
```
docker pull centos:centos7.9.2009
```
## 使用Docker架設網頁
### 1.下載映像檔
```
docker run -it --name web centos:7.9.2009 bash
```
### 2.安裝hpptd
```
yum install httpd -y
```
### 3.開啟新Terminal，修改映像檔名
```
docker commit web centos:web
```
### 4.將主機的8000端口映射到容器的80端口
```
docker run -d -p 8000:80 centos:web /usr/sbin/apachectl -DFOREGROUND
```
