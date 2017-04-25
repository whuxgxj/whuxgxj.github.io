---
layout: post
title: 数据分析笔试
categories: journal
author: shiyi
tags:
  - documentation
  - sample
image:
  feature: data_analyst.jpg
---

## 考点1 SQL语句

例题：有一个计费表，表名jifei，字段如下：phone(8位的电话号码)，month（月份），expenses（月消费，费用为0表明该月没有产生费用） 下面是该表的一条记录：64262631,201011,30.6 这条记录的含义就是64262631的号码在2010年11月份产生了30.6元的话费。 按照要求写出满足下列条件的sql语句：

### 1、 查找2010年6、7、8月有话费产生但9、10月没有使用并（6、7、8月话费均在51-100元之间的用户

{% highlight sql linenos %} select distinct phone from jifei where (month in (201007,201008,201009) and month not in (201009,201010)) and expenses between 51 and 100 {% endhighlight %}

### 2、 查找2010年以来（截止到10月31日）所有后四位尾数符合AABB或者ABAB或者AAAA的电话号码。（A、 B 分别代表1--9中任意的一个数字）

{% highlight sql linenos %} select distinct phone from jifei where mid(phone,5,1)=mid(phone,6,1) and mid(phone,7,1)=mid(phone,8,1) and mid(phone,5,1) \<> mid(phone,7,1) {% endhighlight %}

### 3、 删除jifei表中所有10月份出现的两条相同记录中的其中一条记录。

{% highlight sql linenos %} select identity(int,1,1) as id, _into new_table from jifei; delete from new_table where (phone,month,expenses) in (select phone,month,expenses from new_table group by phone,month,expenses having count(_) > 1) and id not in (select min(id) from new_table group by phone,month,expenses having count(\*) > 1); {% endhighlight %}

### 4、查询所有9月份、10月份月均使用金额在30元以上的用户号码（结果不能出现重复）

{% highlight sql linenos %} select distinct phone from jifei where (month in (201009,201010)) and (expenses > 30) {% endhighlight %}

## 考点2 逻辑思考能力

### 1、 某人卖掉了两张面值为60元的电话卡，均是60元的价格成交的。其中一张赚了20%，另一张赔了20%，问他总体是盈利还是亏损，盈/亏多少？

設第一張成本價爲x,(60-x)/x=0.2,x=50 第二張成本價爲y,(60-y)/y=-0.2,y=75 總體盈虧：120-（50+75）= -5 亏损5元

### 2、 有个农场主雇了两个小工为他种小麦，其中A是一个耕地能手，但不擅长播种；而B耕地很不熟练，但却是播种的能手。农场主决定种10亩地的小麦，让他俩各包一半，于是A从东头开始耕地，B从西头开始耕。A耕地一亩用20分钟，B却用40分钟，可是B播种的速度却比A快3倍。耕播结束后，庄园主根据他们的工作量给了他俩600元工钱。他俩怎样分才合理呢?

一人一半，因为不论二人效率和速度如何，都负责耕种了一半的土地

### 3.`1 11 21 1211 111221` 下一行是什么？

312211 13112221

### 4.烧一根不均匀的绳，从头烧到尾总共需要1个小时。现在有若干条材质相同的绳子，问如何用烧绳的方法来计时一个小时十五分钟呢？（绳子分别为A 、B、C、D、E、F 。。。。。来代替）

先同时点燃两根绳子，A两头都点燃，B点燃一头，当A烧完时开始点燃B的另一头，此时用时30分钟，当B烧完时拿出绳子C，两头都点（此时用时45分钟），当绳子C烧完时刚好用时一小时十五分钟。
