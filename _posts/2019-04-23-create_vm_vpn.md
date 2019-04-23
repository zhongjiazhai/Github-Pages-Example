---
layout:     post
title:      如何在谷歌云搭建个人VPS节点完成科学上网
category: blog
description: 全国科学上网配置
---
本博客所有文章采用的授权方式为 自由转载-非商用-非衍生-保持署名 ，转载请务必注明出处，谢谢。

   <script type="text/javascript">var cnzz_protocol = (("https:" == document.location.protocol) ? " https://" : " http://");document.write(unescape("%3Cspan id='cnzz_stat_icon_1275018137'%3E%3C/span%3E%3Cscript src='" + cnzz_protocol + "s19.cnzz.com/z_stat.php%3Fid%3D1275018137%26show%3Dpic' type='text/javascript'%3E%3C/script%3E"));</script>
 
 ##  谷歌云的注册
 
 谷歌云注册地址：https://console.cloud.google.com
 
 * 在注册谷歌云的过程中按照要求一步一步完成，没有太多的问题。
 * 完成谷歌云的注册后，第一次注册会免费得到300美金及一年的使用权限。
 
 ##  VM实例的创建
 
 * 按照图片实例，点击Compute Engine 中的VM
 
 ![vm1](images/blog/2019-04-23/vm1.png)
 
 * 点击创建实例
 
 ![vm2](images/blog/2019-04-23/vm2.png)
 
 第一步：名称可以自定义
 第二步：选择创建节点所在的区域和地区，这个根据需求吧。
 第三步：机器类型，就是选择你需要的机器配置，当然做科学上网的vps节点的服务器不需要太高的配置，那么我们就选择最低的一个配置，当然价格也是最便宜的。
 第四步：启动磁盘，默认的也是第一个，如果不是默认的第一个点击打开选中第一个，如图：
 
 ![vm3](images/blog/2019-04-23/vm3.png)
 
 第五步：图中标注的第四步，也就是防火墙，允许HTTP流量和HTTPS流量，全部打勾。选择创建
 创建完成后可以看到如下内容：
 
 ![vm4](images/blog/2019-04-23/vm4.png)
 
 说明你已经创建成功。
 
 ##  创建防火墙规则
 
* 按照图片标记，打开

![vm5](images/blog/2019-04-23/vm5.png)

* 点击创建防火墙规则
入站：

![vm6](images/blog/2019-04-23/vm6.png)

名称：可以自己定义 说明：也是自己定义，可以选择填写
日志：默认是关闭状态，默认维持不变
网络：默认是default
优先级：默认保持不表
流量方向：选择入站
对匹配项选择执行的操作：允许
目标：网络中的所有实例
来源IP地址范围：0.0.0.0/0
协议和端口：全部允许
点击创建；
以上是配置入站的防火墙规则，同理可以去配置出站的防火墙规则；
出站：

![vm7](images/blog/2019-04-23/vm7.png)

## 创建VM节点

* 按照如下截图操作：

![vm9](images/blog/2019-04-23/vm9.png)

* 来到如下的界面环境：

![vm8](images/blog/2019-04-23/vm8.png)

* 输入代码：

      sudo -i   # 切换用户权限
      wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocksR.sh && chmod +x shadowsocksR.sh
      ./shadowsocksR.sh # 执行sh文件
 
![vm10](images/blog/2019-04-23/vm10.png)

![vm11](images/blog/2019-04-23/vm11.png)

![vm12](images/blog/2019-04-23/vm12.png)

按照提示输入，最后会得到用户的密码，端口等信息，复制出来，以后配置vpn等时候使用。

到这里我们在谷歌云创建vps节点的操作已经完成了，如果不出意外的话，你在手机ssr等工具上输入我们刚刚配置的服务器地址、端口、密码、算法、混淆方式等，就可以完成上外网的操作了。

### 知识点分享

在我们建立节点的时候如何判断地区的速度更快节点更稳定呢？
我们通过这个地址： www.ipip.net
如图：

![vm13](images/blog/2019-04-23/vm13.png)

之后选择你所在的地区及宽带提供商，输入我们刚才配置的外部ip地址然后查看一下响应速度。如果你的最后的速度在70ms以内应该还算是可以的，如果大于70ms，那就修改节点的地区重新创建一下，最后选择合适的节点地区。

![vm14](images/blog/2019-04-23/vm14.png)

![vm15](images/blog/2019-04-23/vm15.png)

## 完结

  联系方式
* My blog address :[zhongjiazhai](http://zhongjiazhai.github.io)
* Email address: zhaizhongjia2010@163.com
* Weibo: [ZhongJia_Zhai](https://weibo.com/u/1944978350)

         
  
    

 
 
