---
layout:     post
title:      Macos找回系统管理员账号
category: blog
description: 几行代码解除你的困惑，而不是愚蠢的重装系统，代码改变世界，改变生活。
---
   <script type="text/javascript">var cnzz_protocol = (("https:" == document.location.protocol) ? " https://" : " http://");document.write(unescape("%3Cspan id='cnzz_stat_icon_1275018137'%3E%3C/span%3E%3Cscript src='" + cnzz_protocol + "s19.cnzz.com/z_stat.php%3Fid%3D1275018137%26show%3Dpic' type='text/javascript'%3E%3C/script%3E"));</script>
    
   ![2018111](images/blog/20181111.png)
   
   系统管理员：顾名思义就是管理你电脑软件安装、软件删除、文件删除的一个系统用户，对应的就是访客，访客的权限只有访问浏览的权限，而没有删除及修改电脑文件的权限。所以，如果你Macos系统失去了管理员权限，那么就相当于你已经失去了对笔记本的绝对控制权限，无法删除软件，同样你也无法安装软件。有时候在我们日常操作中会忘记系统管理员账号密码，也有时候想修改系统管理员账号的名称而造成失去管理员账号了。
   
   
   有的人选择了最复杂的操作***重新安装系统***这不是不可取，一来浪费时间，二来还得重新安装自己所需要的软件，得不偿失呀。有这么聪明的办法敲击几行代码就可以三分钟不到就能搞定，你需要搞一天时间，何必呢？


下面我来介绍一下如何通过几行命令就能重设管理员账号。

1. 进入单用户模式（Single User Model），清除启动配置

开机按住cmd+s，注意是长按，不是和windows一样点按。
在＃root>下输入以下4条命令（如果看到bash-3.2#是一样的）： 
fsck -y 
mount -uaw / 
rm /var/db/.AppleSetupDone 
reboot

第1条命令，对文件系统检查修复，输入后会给出一些提示命令，需要等几秒才能完成； 
第2条命令，是挂载分区，执行后没有任何提示，并不是命令没执行或执行错误； 
第3条命令，删除系统安装完毕的配置，看命令的名字就可以知道，执行后同样没有任何提示； 
第4条命令，重启。

2.新建管理员用户

执行上面的操作后，重启的界面和第一次进系统是一样的了，这时候，该怎么配置就怎么配置，很简单的。

这个可以随意配置，反正这个用户后面不一定会保留。

3.将以前的用户设为管理员

  ![reboot](images/blog/reboot.png)


打开系统偏好设置–>用户与群组，勾选之前的普通用户，勾选上“允许用户管理这台电脑” 
这里写图片描述 
以前的用户就成管理员了，重启进入以前的账户，把刚刚新建的用户删除了就好了（为了安全，可以把要删除的账户改为普通用户，再次重启生效）

   联系方式
* My blog address :[zhongjiazhai](http://zhongjiazhai.github.io)
* Email address: zhaizhongjia2010@163.com
* Weibo: ZhongJia_Zhai

       本博客所有文章采用的授权方式为 
       自由转载-非商用-非衍生-保持署名 
       转载请务必注明出处，谢谢。



