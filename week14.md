# Linux高級檔案管理設定
```
mkdir testdir; cd testdir
```
```
touch {a..d}
```
```
ls -l  # 查看屬性
```
```
cd ..
```
拿掉創造者的w權限
```
chmod u-w testdir/  # 
```
加上 i lock，使root不能修改新增刪除
```
chattr +i a  
```
移除i lock
```
chattr -i a  
```
加上 a lock，使root只能追加文字
```
chattr +a a 
```
移除a lock
```
chattr -a a  
```
針對目錄需要加上 -R，目錄中的文件就會有 chattr lock
```
chattr +i -R testdir
```
