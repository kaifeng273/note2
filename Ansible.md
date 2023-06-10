# Ansible
## 1. 開啟三台虛擬機設定hostname
```
hostnamectl set-hostname centos7-1
bash
```
```
hostnamectl set-hostname centos7-2
bash
```
```
hostnamectl set-hostname centos7-3
bash
```
## 2. 生成金鑰(公私鑰)
```
ssh-keygen
```
## 3. 編輯 /etc/hosts 檔案
```
vim /etc/hosts
```
內容
```
192.168.129.128 centos7-1
192.168.129.127 centos7-2
192.168.129.126 centos7-3
```
## 4.複製本地用戶的公鑰到遠程主機上的帳號中
```
ssh-copy-id root@centos7-2
ssh-copy-id root@centos7-3
```

## 5. 遠端登錄
```
ssh root@centos7-2
ssh root@centos7-3
```
## 6. 安裝ansible
```
yum install ansible -y
```
## 7. 編輯 /etc/ansible/hosts 檔案
```
vim /etc/ansible/hosts
```
內容
```
[server1]
192.168.129.127

[server2]
192.168.129.126

[servers]
192.168.129.127
192.168.129.126
```
## 8. 檢查 client 端是否有回應
```
ansible servers -m ping
```
## 9. 指定 server1 執行 ifconfig 的指令並回傳結果
```
ansible server1 -m command -a "ifconfig"
```
## 10. 執行 Shell指令
```
ansible servers -m shell -a "ifconfig ens33 | grep inet"
```
## 11. 切換到 tmp 資料夾
```
ansible servers -m shell -a "chdir=/tmp pwd"
```
## 12. 檢查檔案 /tmp/a 是否存在，如果存在則執行 ls -l 命令

```
ansible servers -m shell -a "creates=/tmp/a ls -l"
```
## 13. 在 /var/log 資料夾中執行命令 ls -l | grep log
```
ansible servers -m shell -a "chdir=/var/log cmd='ls -l | grep log'"
```
## 14. 列出 Ansible 中的主機清單 
```
ansible servers --list hosts
```
## 15. 執行 id user | grep group 查找使用者所屬的群組信息
```
ansible servers -m shell -a "id user | grep group"
```
## 16. 執行 ifconfig | grep -A 5 ens33 ，以查找名為 "ens33" 的網絡接口的詳細信息
```
ansible servers -m shell -a "ifconfig | grep -A 5 ens33"
```
## 17. 執行 echo hi > /tmp/a.txt 命令，將 "hi" 寫入到 /tmp/a.txt 文件中
```
ansible servers -m shell -a "echo hi > /tmp/a.txt"
```
## 18. 在 /tmp 資料夾執行，並檢查是否存在檔案/etc/passwd，如果不存在，則執行 echo hi
```
ansible servers -m shell -a "chdir=/tmp creates=/etc/passwd echo hi"
```
## 19. 在遠程主機上執行本地主機上的腳本文件
```
ansible server1 -m script -a "./test.sh"
```
```
ansible server1 -m script -a "./test2.sh"
```
test2.sh
```
result=`ifconfig | grep -A 5 ens33 | grep inet | grep -v inet6 | awk '{print $2}'`
echo $result
```
## 20. 遠端安裝
```
ansible server1 -m yum -a "name=httpd state=latest"
```
## 21. 遠端移除 
```
ansible server1 -m yum -a "name=httpd state=absent"
```
## 22. 遠端複製
```
ansible server1 -m copy -a "src=/root/1.txt dest=/tmp/hi.txt backup=yes mode=664 owner=user group=user"
```
## 23. 從遠端抓檔案到本地端
```
ansible server1 -m fetch -a "src=/etc/passwd dest=/root"
```
## 24. 創建了一個名為 "test.txt" 的檔案，並將其所有者設為 "user"，所屬群組設置為 "user"，檔案權限設為 666
```
ansible server1 -m file -a "path=/tmp/test.txt owner=user group=user mode=666"
```
## 25. 修改資料夾屬性
```
ansible server1 -m file -a "path=/tmp/testdir mode=700"
```
## 26. 創建了一個 1.txt 的連結，連結到 /tmp/testdir 目錄
```
ansible server1 -m file -a "src=/tmp/testdir name=/root/1.txt state=link"
```
## 27. 遠端開啟 httpd server
```
ansible server1 -m service -a "name=httpd state=started"
```
## 28. 新增群組
```
ansible server1 -m group -a "name=testgroup"
```
## 29. 新增群組使用者
```
ansible server1 -m user -a "name=testuser group=testgroup uid=1100 comment='peter' home=/home/testuser"
```
## 30. 測試使用者有沒有存在
```
ansible server1 -m user -a "id user"
```
```
ansible server1 -m user -a "getent passwd user"
```
## 31. 同時安裝
```
ansible server1 -m yum -a "name=httpd,vsftpd state=present"
```
