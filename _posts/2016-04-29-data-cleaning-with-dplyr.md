---
layout:     post
title:      使用dplyr包进行数据清理
categories: journal
tags: [documentation,sample]
image:
  feature: data_cleaning.jpg
  teaser: data_cleaning_teaser.jpg
  credit:
  creditlink:
---

### 定义：      

   - 数据结构    
   - 数据语义    

### 整理杂乱的数据集：   
      
##### Case 1: 列名称是值，不是变量名    
       
  {% highlight r linenos %}
  #>                   religion <$10k $10-20k $20-30k $30-40k $40-50k $50-75k
  #>                      (chr) (int)   (int)   (int)   (int)   (int)   (int)
  #> 1                 Agnostic    27      34      60      81      76     137
  #> 2                  Atheist    12      27      37      52      35      70
  #> 3                 Buddhist    27      21      30      34      33      58
  #> 4                 Catholic   418     617     732     670     638    1116
  #> 5       Don’t know/refused    15      14      15      11      10      35
  #> 6         Evangelical Prot   575     869    1064     982     881    1486
  #> 7                    Hindu     1       9       7       9      11      34
  #> 8  Historically Black Prot   228     244     236     238     197     223
  #> 9        Jehovah's Witness    20      27      24      24      21      30
  #> 10                  Jewish    19      19      25      25      30      95
  #> ..                     ...   ...     ...     ...     ...     ...     ...
  #> Variables not shown: $75-100k (int), $100-150k (int), >150k (int), Don't
  #> know/refused (int).    
  {% endhighlight %}
  
<!-- more -->    
  补救措施：   
 
  - 使用`gather`函数，gather（数据集，key=变量列名称，value=值列名称,要转换的列）将变量转换为观测值  
    `gather(data, key, value, ..., na.rm = FALSE, convert = FALSE,factor_key = FALSE)`
  - 新增变量列：`mutate(.data, ...)`
  - 选择所需要的列：`select(.data, ...) `   
    - `starts_with(x, ignore.case = TRUE)`: names starts with x
    - `ends_with(x, ignore.case = TRUE)`: names ends in x
    - `contains(x, ignore.case = TRUE)`: selects all variables whose name contains x
    - `matches(x, ignore.case = TRUE)`: selects all variables whose name matches the regular expression x
    - `num_range("x", 1:5, width = 2)`: selects all variables (numerically) from x01 to x05.
    - `one_of("x", "y", "z")`: selects variables provided in a character vector.
    - `everything()`: selects all variables.
  - 从小到大排序：`arrange(.data, ...)`    desc降序
  - 选择符合条件的行：`filter(.data, ...)`,可有多个条件
  - 新增变量列，但删除已有的变量：`transmute(.data, ...)`
  - 变量重命名：`rename(.data, ...)`
  - 选择指定行：`slice(.data, ...)`
  - 计算指定值：`summarise(.data, ...)`
  - 数据分组：`group_by(.data, ..., add = FALSE)`

               
##### Case 2: 多个变量存储在同一列    
              
  {% highlight r linenos %}
  #> Source: local data frame [5,769 x 22]
  #> 
  #>     iso2  year   m04  m514  m014 m1524 m2534 m3544 m4554 m5564   m65    mu
  #>    (chr) (int) (int) (int) (int) (int) (int) (int) (int) (int) (int) (int)
  #> 1     AD  1989    NA    NA    NA    NA    NA    NA    NA    NA    NA    NA
  #> 2     AD  1990    NA    NA    NA    NA    NA    NA    NA    NA    NA    NA
  #> 3     AD  1991    NA    NA    NA    NA    NA    NA    NA    NA    NA    NA
  #> 4     AD  1992    NA    NA    NA    NA    NA    NA    NA    NA    NA    NA
  #> 5     AD  1993    NA    NA    NA    NA    NA    NA    NA    NA    NA    NA
  #> 6     AD  1994    NA    NA    NA    NA    NA    NA    NA    NA    NA    NA
  #> 7     AD  1996    NA    NA     0     0     0     4     1     0     0    NA
  #> 8     AD  1997    NA    NA     0     0     1     2     2     1     6    NA
  #> 9     AD  1998    NA    NA     0     0     0     1     0     0     0    NA
  #> 10    AD  1999    NA    NA     0     0     0     1     1     0     0    NA
  #> ..   ...   ...   ...   ...   ...   ...   ...   ...   ...   ...   ...   ...
  #> Variables not shown: f04 (int), f514 (int), f014 (int), f1524 (int), f2534
  #>   (int), f3544 (int), f4554 (int), f5564 (int), f65 (int), fu (int).
  {% endhighlight %} 

  -  分离变量名：
 {% highlight r linenos %}
separate(data, col, into, sep = "[^[:alnum:]]+",remove = TRUE,convert = FALSE, extra = "warn", fill = "warn", ...)
 {% endhighlight %}

            
##### case 3: 变量同时存在于行和列中    
                
  {% highlight r linenos %}
  #> Source: local data frame [22 x 35]
  #> 
  #>         id  year month element    d1    d2    d3    d4    d5    d6    d7
  #>      (chr) (int) (int)   (chr) (dbl) (dbl) (dbl) (dbl) (dbl) (dbl) (dbl)
  #> 1  MX17004  2010     1    tmax    NA    NA    NA    NA    NA    NA    NA
  #> 2  MX17004  2010     1    tmin    NA    NA    NA    NA    NA    NA    NA
  #> 3  MX17004  2010     2    tmax    NA  27.3  24.1    NA    NA    NA    NA
  #> 4  MX17004  2010     2    tmin    NA  14.4  14.4    NA    NA    NA    NA
  #> 5  MX17004  2010     3    tmax    NA    NA    NA    NA  32.1    NA    NA
  #> 6  MX17004  2010     3    tmin    NA    NA    NA    NA  14.2    NA    NA
  #> 7  MX17004  2010     4    tmax    NA    NA    NA    NA    NA    NA    NA
  #> 8  MX17004  2010     4    tmin    NA    NA    NA    NA    NA    NA    NA
  #> 9  MX17004  2010     5    tmax    NA    NA    NA    NA    NA    NA    NA
  #> 10 MX17004  2010     5    tmin    NA    NA    NA    NA    NA    NA    NA
  #> ..     ...   ...   ...     ...   ...   ...   ...   ...   ...   ...   ...
  #> Variables not shown: d8 (dbl), d9 (lgl), d10 (dbl), d11 (dbl), d12 (lgl),
  #>   d13 (dbl), d14 (dbl), d15 (dbl), d16 (dbl), d17 (dbl), d18 (lgl), d19
  #>   (lgl), d20 (lgl), d21 (lgl), d22 (lgl), d23 (dbl), d24 (lgl), d25 (dbl),
  #>   d26 (dbl), d27 (dbl), d28 (dbl), d29 (dbl), d30 (dbl), d31 (dbl).
  {% endhighlight %} 
   
  - 将原来的列值转换为列名称：`spread(data, key, value, fill = NA, convert = FALSE, drop = TRUE)`

                 
##### Case 4: 多种类型的观测单元被存储在同一个表中。             

将一个表拆分为多个表    

  - `Unique()`
  - `Left_join()`

               
##### Case 5: 单个观测单元存储在多个表中。        
             
结合plyr包的*ply函数，将多个文件的数据读取到同一个数据集中
