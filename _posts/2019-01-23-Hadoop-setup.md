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

## 集群启动
sbin/start-all.sh

## 历史执行查询服务启动
sbin/mr-jobhistory-daemon.sh start historyserver

## 启动 hive2 服务
nohup hive --service metastore >/dev/null 2>&1 &      ## 必须先启动hive元数据存储服务

then 之后启动hive2 的服务：

nohup hive --service hiveserver2 >/dev/null 2>&1 &  ## 再启动后面的hive2服务

## 启动 spark 集群

${SPARK_HOME}/sbin/start-all.sh
${SPARK_HOME}/sbin/start-thriftserver.sh --master yarn    ## 使用spark 用户启动。即被指定 spark队列中。

## 停止

${SPARK_HOME}/sbin/stop-thriftserver.sh
${SPARK_HOME}/sbin/stop-all.sh
${HADOOP_HOME}/sbin/mr-jobhistory-daemon.sh stop historyserver
${HADOOP_HOME}/sbin/stop-all.sh

linux用户名 hadoop/hadoop root/password

## hive/beeline 
例子：
beeline
!connect jdbc:hive2://bigdata111:10000
hadoop/hadoop
## mysql
数据库名 root/root1234
      hive/hive1234
      登陆格式： mysql -uroot -proot1234
### 下面说一下集群启动中遇到的问题：

* 在启动hadoop过程中，jps 发现namenode 没有启动，通过日志查看 tail -f hadoop-hadoop-namenode-bigdata111.log，发现是in_use.lock文件权限问题？


做了如下的操作：

	1. 修改日志文件权限：chown -R hadoop:hadoop /usr/local/bigdata/hadoop/logs
	
	2. 修改文件所在文件夹权限 chown -R hadoop:hadoop/usr/local/bigdata/hadoop/data/dfs/name
	
        3. 重新启动，问题解决了。
	
	
### Linux 常用命令查看文件路径

 hdfs dfs -ls /
 rm -rf* ##删除当前文件夹下所有内容
 rm -rf current/ ##删除current 文件夹下所有内容
 hdfs namenode -format namenode 节点格式化
 ls -ltr 
 mv 旧的文件名 新的文件名
 
 ### hive 表中加载数据
 
 load data [local] inpath 'filepath' [overwrite] into table tablename[partition(partcol1=val1,partcol2=val2)]
 在load 表的过程中，表的stored 格式必须是textfile,否则出现错误；

