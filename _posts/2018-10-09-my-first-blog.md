---
layout:     post
title:      个人博客站点的成功建立
category: blog
description: 博客站点的建立、以及自己为什么要写博客？
---
## 博客站点建立的心路历程

定义心路历程是否有些过头了？我个人认为不偏不倚，通过自己8个小时的琢磨及模仿，终于成功的搭建了属于自己的博客站点。在这里特别要感谢 [BeiYuu][]
正是得益于他的文档帮助，站点的开源样式才顺利完成。就像他的文章[我为什么写博客?][2]中所讲到的，技术很简单，只要你有一颗热于学习和创造
的心，你也能完成自己站点的操作。希望之后能通过自己水平的提高能修改出符合自己风格和样式的界面。终归博客站点是要写博客内容的，这才是建立这个站点的根本，你的站点做的再牛逼，写出高质量、水准的文章也是白扯。

## 小白在建立站点的时候请留意以下三点：

* 首先，我们要非常清楚github这个平台项目如何使用，例如如何建立存储库，如何删除存储库，如何设置存储库名等，因为在之前我也只是听说GitHub这个平台，平时工作
也用不着，所以之前也只是停留在听说的阶段。如果你之前用过github那么建立这个站点来说就非常easy了。
* 其次，这篇文章[使用Github Pages建独立博客][1]，写的非常详细也很清楚，把搭建过程中的问题，需要怎么操作都写的非常清楚，按照步骤一步一步走就好了，不过有些看不大明白的也没有大的关系，有些是介绍概念性的，自己知道这个脚本是干啥用的就好了。
* 最后，在修改属于自己的微博链接、twitter、instagram的时候记住粘贴的时候不要粘错行避免不必要的麻烦。

## 详细介绍几个在建立站点时的名词和步骤

* 如何哪个脚本可以让界面显示自己的微博、Twitter、instagram?
 你想在界面显示你自己的博客名称，自定义你的名称，只需要修改根目录下名称为index.md的文件，如下这一行代码中的名称即可。
![blog-name](/images/other/blog-name.png)
 修改属于你自己的微博链接，首先找到你自己的微博链接地址，之后把链接地址放在这一行脚本中：
 ![weibo-name](/images/other/weibo-name.png)
 tiwtter等其他等修改都是类似的，当然你也可以自己添加自己的其他软件平台账号，这个就看你自己的发挥了。
 我的完成的效果如下：
 ![the-last.png](/images/other/the-last.png)
 * 如何才能把Github-Pages-Example文件踪夹复制或者克隆到自己的目录下呢？
 点击fork，
 ![the-fork](/images/other/the-fork.png)
 * 修改储存库的名称
 ![the-setting](/images/other/the-setting.png)

## 配置和使用Github
Git是版本管理的未来，他的优点我不再赘述，相关资料很多。推荐这本[Git中文教程][4]。

要使用Git，需要安装它的客户端，推荐在Linux下使用Git，会比较方便。Windows版的下载地址在这里：[http://code.google.com/p/msysgit/downloads/list](http://code.google.com/p/msysgit/downloads/list "Windows版Git客户端")。其他系统的安装也可以参考官方的[安装教程][5]。

下载安装客户端之后，各个系统的配置就类似了，我们使用windows作为例子，Linux和Mac与此类似。

在Windows下，打开Git Bash，其他系统下面则打开终端（Terminal）：
![Git Bash](/images/githubpages/bootcamp_1_win_gitbash.jpg)

### 1、检查SSH keys的设置
首先我们需要检查你电脑上现有的ssh key：

    $ cd ~/.ssh

如果显示“No such file or directory”，跳到第三步，否则继续。

### 2、备份和移除原来的ssh key设置：
因为已经存在key文件，所以需要备份旧的数据并删除：

    $ ls
    config	id_rsa	id_rsa.pub	known_hosts
    $ mkdir key_backup
    $ cp id_rsa* key_backup
    $ rm id_rsa*

### 3、生成新的SSH Key：
输入下面的代码，就可以生成新的key文件，我们只需要默认设置就好，所以当需要输入文件名的时候，回车就好。

    $ ssh-keygen -t rsa -C "邮件地址@youremail.com"
    Generating public/private rsa key pair.
    Enter file in which to save the key (/Users/your_user_directory/.ssh/id_rsa):<回车就好>

然后系统会要你输入加密串（[Passphrase][6]）：

    Enter passphrase (empty for no passphrase):<输入加密串>
    Enter same passphrase again:<再次输入加密串>

最后看到这样的界面，就成功设置ssh key了：
![ssh key success](/images/githubpages/ssh-key-set.png)

### 4、添加SSH Key到GitHub：
在本机设置SSH Key之后，需要添加到GitHub上，以完成SSH链接的设置。

用文本编辑工具打开id_rsa.pub文件，如果看不到这个文件，你需要设置显示隐藏文件。准确的复制这个文件的内容，才能保证设置的成功。

在GitHub的主页上点击设置按钮：
![the-setting-ssh](/images/other/the-setting-ssh.png)

选择SSH Keys and GPG keys项，把复制的内容粘贴进去，然后点击New Keys按钮即可：
![ssh-name](/images/other/ssh-name.png)

PS：如果需要配置多个GitHub账号，可以参看这个[多个github帐号的SSH key切换](http://omiga.org/blog/archives/2269)，不过需要提醒一下的是，如果你只是通过这篇文章中所述配置了Host，那么你多个账号下面的提交用户会是一个人，所以需要通过命令`git config --global --unset user.email`删除用户账户设置，在每一个repo下面使用`git config --local user.email '你的github邮箱@mail.com'` 命令单独设置用户账户信息

### 5、测试一下
可以输入下面的命令，看看设置是否成功，`git@github.com`的部分不要修改：

    $ ssh -T git@github.com


如果是下面的反应：

    The authenticity of host 'github.com (207.97.227.239)' can't be established.
    RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
    Are you sure you want to continue connecting (yes/no)?


不要紧张，输入`yes`就好，然后会看到：

    Hi <em>username</em>! You've successfully authenticated, but GitHub does not provide shell access.

### 6、设置你的账号信息
现在你已经可以通过SSH链接到GitHub了，还有一些个人信息需要完善的。

Git会根据用户的名字和邮箱来记录提交。GitHub也是用这些信息来做权限的处理，输入下面的代码进行个人信息的设置，把名称和邮箱替换成你自己的，名字必须是你的真名，而不是GitHub的昵称。

    $ git config --global user.name "你的名字"
    $ git config --global user.email "your_email@youremail.com"

#### 设置GitHub的token

新版的接口已经不需要配置token了，所以下面这段可以跳过了

有些工具没有通过SSH来链接GitHub。如果要使用这类工具，你需要找到然后设置你的API Token。

在GitHub上，你可以点击*Account Setting > Account Admin*：
![set ssh keys](/images/githubpages/bootcamp_1_token.jpg)

然后在你的命令行中，输入下面的命令，把token添加进去：

    $ git config --global user.name "你的名字"
    $ git config --global user.token 0123456789your123456789token

如果你改了GitHub的密码，需要重新设置token。

### 成功了
好了，你已经可以成功连接GitHub了。




## 写博客的初衷

![r_blogging.jpg](/images/blog/r_blogging.jpg)


其中文章[我为什么写博客][3]这篇文章写的非常之好，写出了我们为什么要写博客的初衷。能通过自己耐心的书写把自己平时在工作、生活中有意思的经历、美好的回忆、以及自己取得成果分享出来，这会是有不一样的体会。当然，博文不是自己随便抒发情感，没有质量的博文，要想自己的文章能有一个高的思想水准、高质量，也是需要自己慢慢琢磨和推敲的。虽然你拥有很多的工作技术经验、拥有很丰富的知识生活阅历，能完全通过语言文字把自己想要表达的完全表达出来也是一件非常苦难的事情。一篇高质量的博文大概需要满足一下几点：

* 追求质量，宁缺勿滥；
* 以初学者角度看问题，不故作高深；
* 不制造电子垃圾，不拾人牙慧；
* 从实际问题出发，注重共性;

而对于我的第一篇博文，相距以上几点还差之甚远，拥有很大的学习和提升空间。写到这里，如果你能明白我在说什么事情，那我还有希望继续写博文，继续提高，相反，如果你不知道我在说啥，那我可能真的没有救了。自从大学毕业后这样长篇书写内容、书写自己想法的文章真的一次没有写过了。
同样我也相信这样一句话：
在快知识、微段子横行的今天，能对一个个问题深入的去思考，一方面得到的是心灵的平静，更多的则是深入思考之后的收获的喜悦感，会有不一样的体会的。我也努力坚持
学习更多的知识，增加自己的知识水平及文字表述能力，早日写出高质量的博文，早日能有深入思考之后的喜悦感。
在文章[Why I blog][3],中有些片段写的非常有深度，写出了坚持些博客的理由和初衷，包括以下几点内容：


### 有助于修正和完善对事物的认识

随着年龄的增长和经验的累积，逐渐地，人们会形成对事物固定化的认识，大到宗教信仰，小到通心菜的最佳烹饪方法，依赖和死守这些经验和固化的认识，生活就如同失去了动力，任由惯性引领。

写博客促使我们重拾“分析”和“思考”，帮助我们实现自我认识的修正和完善。前期阅读资料->写博中不断对自己提问、梳理思路->整理优化博文，经过这个过程，我们可以修正原先错误的认知，抑或加深了对原有知识的理解。

写博有助于修正和完善对事物的认识——这是我写博的主要原因，仅凭此，我就认为写博客是一件十分有意义的事。

### 增强自信心

写博客有点像演讲，演讲中我们向公众陈述自己的看法和认识、把内心世界展示给别人，一般人对此感到恐惧。另外，有时博文中的观点会引发争论，或褒或贬，对每一个博主而言，直面他人的质疑和批评需要很大的勇气。

但随着撰写博文数量的增加，你会发现自己抗打击的能力越来越强，陈述观点的时候会变得更加自信、面对公众时变得更加坦然。博客就是这么一个平台，助你实现以上转变、完成华丽地转身。


同时在文章中也给出了，如何才能写出一篇高质量的博客：

* 避免内容平淡。内容平淡的博客不会让你脱颖而出，因这样的博客实在是太多了。把观点写清楚并记录下思考和分析的过程，我知道这很难办到，但若博文中缺乏论点、内容空洞，写博客就变成毫无意义的事。

* 让更多的人知道。一篇辛辛苦苦写就的博文，阅读者寥寥，不但没有让更多人从博文中受益，而且博主也会渐渐失去写博的劲头。写就一篇高质量的博文已经花了我们很多时间和精力，但在博文发表后，我们还应对其做更多地推广，让更多的人阅读它，充分发挥它的作用。

* 积极参与交流和互动。积极地与博文读者进行交流和互动，能为你的博客聚集更多的人气。开启博文的评论功能，及时关注评论的更新并以最快的速度回复，这需要投入持续的热情，目前我也努力地在这方面作尝试。



## 结束语
到这里，我的第一篇博文想表达的内容基本都表达完毕了，能完成搭建自己的站点，我也是心满意足了，虽然在文章中存在诸多语句不通，文笔表达很烂的现象，但是我相信
这是一个新的开始，一个改变自我的开始。希望自己在以后的日子里能有很大的提高和改变。
**生命在于折腾**
再次感谢 
* [BeiYuu](http://beiyuu.com)
 
my blog addrss:[zhongjiazhai](http://zhongjiazhai.github.io)

## 参考文献内容及注解
http://beiyuu.com/github-pages
http://beiyuu.com/why-blog
http://www.cnblogs.com/bangerlee/archive/2011/09/11/2173632.html   "Why I Blog翻译版"
http://progit.org/book/zh/ "Pro Git中文版"
http://help.github.com/mac-set-up-git/ "Mac下Git安装"

[BeiYuu]:    http://beiyuu.com  "BeiYuu"
[1]:   http://beiyuu.com/github-pages
[2]:   http://beiyuu.com/why-blog
[3]:   http://www.cnblogs.com/bangerlee/archive/2011/09/11/2173632.html   "Why I Blog翻译版"
[4]: http://progit.org/book/zh/ "Pro Git中文版"
[5]: http://help.github.com/mac-set-up-git/ "Mac下Git安装"
