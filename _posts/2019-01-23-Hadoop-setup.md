---
layout:     post
title:      Hadoop集群的搭建
category: blog
description: 集群搭建教程
---


   <script type="text/javascript">var cnzz_protocol = (("https:" == document.location.protocol) ? " https://" : " http://");document.write(unescape("%3Cspan id='cnzz_stat_icon_1275018137'%3E%3C/span%3E%3Cscript src='" + cnzz_protocol + "s19.cnzz.com/z_stat.php%3Fid%3D1275018137%26show%3Dpic' type='text/javascript'%3E%3C/script%3E"));</script>

### 使用VMvare创建一个虚拟机，我使用的是Red had linux 7.4,并关闭全部虚拟机的防火墙

* 因为默认的虚拟机主机名都是linux，所以为了便于虚拟机的识别，创建完成虚拟机后我们对虚拟机名进行修改，我们把用于主节点的虚拟机名称设为
 bigdata111(按自己的喜好创建)

* 修改主机名的命令:sudo gedit /etc/hostname

* 为了虚拟机之间能ping通，需要修改虚拟机的ip地址; 命令：sudo gedit /etc/hosts

![hosts](images/blog/2019-01-23/hosts.jpg)

在linux如何查看ip地址，命令： ifconfig -a;

![ifconfig-a](images/blog/2019-01-23/ifconfig-a.jpg)

* 修改虚拟机网络设置
 1、虚拟机网络适配器选择 NAT模式，如下图：
 ![NAT](images/blog/2019-01-23/NAT.jpg)
 2、虚拟机网络设置，如下图：
 ![network](images/blog/2019-01-23/network.jpg)
 3、修改虚拟机网络文件配置，命令： vim /etc/sysconfig/network-scripts/ifcfg-enp0s3 
 修改完截图如下：
 ![ifcfg-enp0s3](images/blog/2019-01-23/ifcfg-enp0s3.jpg)
 ### 集群安装好后，根据域名修改部分配置文件
 
文件名：core-site.xml yarn-site.xml hive-site.xml


