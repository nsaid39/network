# **SSH遠端登入**
# Server端設定

**首先先更新ssh**
```
$ sudo apt-get install ssh
```

---
**建立帳號**
```
$ sudo useradd -m -s /bin/bash username
```
-m 創造一個家目錄
-M 不創造家目錄(或是不打)
-s 指定新用戶的Shell

---
**設定密碼**
```
$ sudo passwd username
```

---
# Client端
**Client端登入**
```
$ ssh username@host
```

---
# 登入詢問
每次連線前都會詢問
是否是否要下載連到那台機器OpenSSH Server所提供的公鑰
![Y/N](https://i.imgur.com/BESqxkZ.png)


yes後，會在家目錄中新增一個.ssh/known_hosts 檔
裡面記錄下載的公鑰

原本沒有 .ssh/
![沒'.ssh/'](https://i.imgur.com/3tYg17R.png)

同意後
![有'.ssh/'](https://i.imgur.com/VnhFyEg.png)
known_hosts檔內存放下載好的公鑰
![known_hosts](https://i.imgur.com/ga7QFdT.png)


---

可以透過修改/etc/ssh/ssh_config的參數來達成免詢問
```
$ sudo nano /etc/ssh/ssh_config
```
將此檔案裡的
```
#Stricthostkeychecking ask
```
改成
```
Stricthostkeychecking no
```
取消掉它的註解
之後就不會再詢問



---

# 免密碼登入
A主機要登入B主機時，是透過SSH對稱式加密。
每次登入時都需要密碼登入，可透過固定彼此的公、私鑰來免輸入密碼程序。

**創公、私鑰**
```
$ ssh-keygen -t rsa -P ''
```
-P要大寫
後面是兩個單引號''，中間不能有空格
![RSA](https://i.imgur.com/hlwKb3U.png)


在家目錄裡的.ssh (~/.ssh)
會建立以下檔案
id_dsa        -->私鑰
id_dsa.pub    -->公鑰
![公、私鑰](https://i.imgur.com/Lob5j3s.png)


---
**傳送公鑰去Server端**
```
$ ssh-copy-id username@host -p 22
```
-p    port號
(port可不打，預設為22)
![傳公鑰](https://i.imgur.com/xVrgmP7.png)


傳送成功後，
會在Server端的~/.ssh/建立一個authorized_keys
裡面紀錄Client端的公鑰、username@hostname
![authorized_keys](https://i.imgur.com/jSVC0yI.png)



---
**測試結果**
最後只要登入時，不用密碼就可以登入了。
![login without passwd](https://i.imgur.com/vbEjnLU.png)
