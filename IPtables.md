# IPtables
## 介紹
iptables是運行在使用者空間的應用軟體，通過控制Linux核心netfilter模組，來管理網路封包的處理和轉發  
  iptables 就是Linux 作業系統的防火牆  
架構為
「表（tables）」  
「鏈（chain）」  
「規則（rules）」三個層面


在Alpine上新增此套件
```
$ sudo apk add iptables
```
新增iptables，(重新開機失效)  
```
sudo iptables -t nat -A POSTROUTING -o eth0 ! -d 10.233.0.0/24 -j MASQUERADE
```
-t ：後接 table，例如 nat或 filter，若省略，則使用預設 filter  
-L ：列出目前的 table的規則  
-n ：不進行 IP與 HOSTNAME的反查，顯示訊息速度會快很多！  
-v ：列出更多的資訊，包括通過該規則的封包總位元數、相關的網路介面等  
chain
    POSTROUTING：在進行路由判斷之後所要進行的規則  
MASQUERADE ：這個設定值就是『 IP 偽裝成為封包出去 (-o) 的那塊裝置上的 IP 』！  


觀看iptable的設定，此指令需要root  
```
$ sudo iptables -t nat -L -n 
```
![](https://i.imgur.com/6JrknUe.png)  

封包從網卡進入  
nat進行轉址  
路由判斷就是去查看路由表  

```
sudo iptables -I INPUT -s 10.233.0.1 -j DROP
```
-I insert  
-D delete  

-s source  
-d destination  

-j jump


```
$ sudo iptables -F
$ sudo iptables -t nat -F
```
-F 清除所有iptables的設定
-t 指定table