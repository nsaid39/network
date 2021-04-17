# 固定IPv4設定
先看網卡的名稱
```
$ ifconfig -a
```
## Alpine
```
$ sudo nano /etc/network/interfaces
```
![](https://i.imgur.com/5THJYH5.jpg)  
```
reboot
```

## Ubuntu server
```
$ sudo nano /etc/netplan/00-installer-config.yaml
```

![](https://i.imgur.com/zwUMiac.jpg)  
```
$ sudo netplan try
```
先try  
再apply  
```
$ sudo netplan apply
```



###### tags: `TCP/IP`