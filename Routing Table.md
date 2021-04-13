# Routing Table

# **開啟ip_forward**
到/etc/proc/sys/net/ipv4/ip_forward
將裡面的0改成1
意指任命此台裝置成為router，開啟轉送封包

*以上方法只要重新開機就會被清除，所以我們需要永久開啟的方法。

**ip_forward永久開啟**
在/etc/sysctl.conf 中加入
```
net.ipv4.ip_forward = 1
```


---
# **新增Routing Table**
```
$ sudo route add -net 10.0.50.0 netmask 255.255.255.0 gw 120.96.143.50
```
-net ->目的地network ID
netmask ->目的地子網路遮罩
gw ->gateway

*以上語法也是只要重開機就會重置

**永久修改Routing Table**
建立此檔案，永久修改Routing Table。

!!!!!!!!要記得安裝bash!!!!!!!!

![](https://i.imgur.com/9mR700F.png)

OR

![](https://i.imgur.com/R7AQv8r.png)

*上為一次key很多不同ip，下為只固定一台

記得chmod +x


**啟用開機執行檔功能**
```
sudo rc-update add local
```
重開機
```
sudo reboot
```

原理：每次重開機的時候，系統都會執行此檔案

###### tags: `TCP/IP` `Router`