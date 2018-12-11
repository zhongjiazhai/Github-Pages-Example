---
layout:     post
title:      Hive 函数lateral view、split 介绍
category: blog
description: 
---

   <script type="text/javascript">var cnzz_protocol = (("https:" == document.location.protocol) ? " https://" : " http://");document.write(unescape("%3Cspan id='cnzz_stat_icon_1275018137'%3E%3C/span%3E%3Cscript src='" + cnzz_protocol + "s19.cnzz.com/z_stat.php%3Fid%3D1275018137%26show%3Dpic' type='text/javascript'%3E%3C/script%3E"));</script>


   联系方式
* My blog address :[zhongjiazhai](http://zhongjiazhai.github.io)
* Email address: zhaizhongjia2010@163.com
* Weibo: ZhongJia_Zhai

    ** 本博客所有文章采用的授权方式为自由转载-非商用-非衍生-保持署名 转载请务必注明出处，谢谢。
### 一、简述
简述：Lateral view  函数用于和split，explode等UDTF一起使用，它能够将一行数据拆分成多行数据，在此基础上可以对拆分后的数据进行聚合。
Lateral view 再把结果组合，产生一个支持别名表的虚拟表。

### 二、举例说明

  假如一张表PageAds,它有两列数据，第一列数据是pageid ，第二列是adid_list，即用逗号分隔的广告ID集合
  
  
            Pageid string 	Arrag<int> adid_list
            “front_page”	  [1,2,3]
            “contact_page”	[3,4,5]
   
  ## 要求：统计所有广告id在所有页面出现的次数
  * 首先拆分广告ID
  
              Select pageid,adid  from pageAds lateral view explode(adid_list) adtable as adid;

执行后结果如下：
  
              String pageid 	Int adid
                “front_page”	1
                “front_page”	2
                “front_page”	3
              “contact_page”	3
               “contact_page”	4
               “contact_page”	5

*  做一个聚合的统计
             
             Select adid,count(1) from pageAds lateral view explode(adid_list) adtable as adid Group by adid;
     执行结果如下
           Int adid 	Count(1)
                   1	1
                   2	1
                   3	2
                   4	1
                   5	1
 ## 项目实际案例实际操作
   * 背景介绍 现有目标表为：TBL_MMS_SHOP，从目标表中字段名mrchnt_no_trm 提取商编和终端号；
      
      如下提取规则：
      
      a、“商编号1|终端号1，商编号2|终端号2………”
      b、提取商编长度小于等于15位且终端号长度小于等于8位数据
   * 第一步，先把字段rchnt_no_trm一行数据通过lateral view 函数分割成多行数据
   
            select 
                  mrch_nt_no_trm_split
            from pdmstg.tbl_mms_shop 
            lateral view explode(split(mrchnt_no_trm,',')) mrchnt_no_trm as mrchnt_no_trm_split;
  * 介绍一下split 函数
      split 函数 字符串分割函数，这个函数相对比较简单，
      基本使用方法： split('a,b,c,d,d',',')
      得到的结果为：
      ["a","b","c","d","d"]
      
      如果要截取字符串中的某个值
      
      需要使用split('a,b,c,d,d',',')[0]
      
      得到的结果为：a
      
  * 介绍完split函数，我们接着介绍项目实例，第二步骤，利用split函数截取商编号和终端编号
  
  
             Select  
                   Split(mrch_nt_no_trm_split,’\\\|’)[0]  as crd_acr_id –商编号
                  ,Split(mrch_nt_no_trm_split,’\\\|’)[1]  as crd_acr_tml_txt –终端号
             From PDMSTG.TBL_MMS_SHOP lateral view explode(split(mrchnt_no_trm,’,’))
             mrchnt_no_trm as mrchnt_no_trm_split
           
           
  * 第三步骤 利用substr函数截取字符串长度
  
          Select 
                Substr(crd_acr_id,1,15)
               ,Substr(crd_acr_tml_txt,1,8)
          From (
                Select  
                        Split(mrch_nt_no_trm_split,’\\\|’)[0]  as crd_acr_id –商编号
                       ,Split(mrch_nt_no_trm_split,’\\\|’)[1]  as crd_acr_tml_txt –终端号
                 From PDMSTG.TBL_MMS_SHOP lateral view explode(split(mrchnt_no_trm,’,’))
                 mrchnt_no_trm as mrchnt_no_trm_split）
      





       


