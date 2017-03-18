---
layout:     post
title:      R语言交互式绘图包ggvis学习笔记
categories: journal
tags: [documentation,sample]
image:
  feature: data-visualization.jpg
  teaser: data-visualization_teaser.jpg
  credit:
  creditlink:
---


**`ggvis`基本函数**    
`ggvis()`函数，包括data,x,y,stroke,fill,size,shape,opacity这些参数。ggvis只是传入了数据，并未告诉函数要如何呈现，因此必须加上图层函数

{% highlight r linenos %}
library(ggvis)
p <- ggvis(mtcars, x = ~wt, y = ~mpg)
layer_points(p)
{% endhighlight %}

<!-- more -->
`ggvis`参数的含义

{% highlight r linenos %}
#stroke 阴影
mtcars %>% ggvis(~mpg, ~disp, stroke = ~vs) %>% layer_points()
#fill 填充
mtcars %>% ggvis(~mpg, ~disp, fill = ~vs) %>% layer_points()
#size大小
mtcars %>% ggvis(~mpg, ~disp, size = ~vs) %>% layer_points()
#shape形状
mtcars %>% ggvis(~mpg, ~disp, shape = ~factor(cyl)) %>% layer_points()
#：=绘制固定的颜色或大小
mtcars %>% ggvis(~wt, ~mpg, fill := "red", stroke := "black") %>% layer_points()
#opacity 透明度
mtcars %>% ggvis(~wt, ~mpg, size := 300, opacity := 0.4) %>% layer_points()
mtcars %>% ggvis(~wt, ~mpg, shape := "cross") %>% layer_points()
{% endhighlight %}

**`ggvis`图形交互**   
ggvis可以将参数的值通过按钮来传递以实现图形交互，这里调用了shiny包的功能，除了`input_slider()`（滑动条）外,还包括`input_checkbox()`（）, `input_checkboxgroup()`, `input_numeric()`, `input_radiobuttons()`, `input_select()` 和 `input_text()`。此外，还可以使用`left_right()` 和`up_down()`调整图像的位置和大小
{% highlight r linenos %}
mtcars %>% 
    ggvis(~wt, ~mpg, 
          size := input_slider(10, 100),
          opacity := input_slider(0, 1)
    ) %>% 
    layer_points()

mtcars %>% 
    ggvis(~wt) %>% 
    layer_histograms(width =  input_slider(0, 2, step = 0.10, label = "width"),
                     center = input_slider(0, 2, step = 0.05, label = "center"))
                     
keys_s <- left_right(10, 1000, step = 50)
mtcars %>% ggvis(~wt, ~mpg, size := keys_s, opacity := 0.5) %>% layer_points()

mtcars %>% ggvis(~wt, ~mpg) %>% 
    layer_points() %>% 
    add_tooltip(function(df) df$wt)
{% endhighlight %}
**`ggvis`图层**
* 点图`layer_points()`，包含属性 x, y, shape, stroke, fill, strokeOpacity, fillOpacity, 和 opacity.
{% highlight r linenos %}
    mtcars %>% ggvis(~wt, ~mpg) %>% layer_points()
{% endhighlight %}
* 路径图`layer_paths()`   
{% highlight r linenos %}
   df <- data.frame(x = 1:10, y = runif(10))  
   df %>% ggvis(~x, ~y) %>% layer_paths()   
{% endhighlight %}
加入fill属性，会得到一个椭圆
{% highlight r linenos %}
t <- seq(0, 2 * pi, length = 100)
df <- data.frame(x = sin(t), y = cos(t))
df %>% ggvis(~x, ~y) %>% layer_paths(fill := "red")
{% endhighlight %}
* 区域填充图`layer_ribbons()`,由属性y和y2控制填充的区域
{% highlight r linenos %}
df <- data.frame(x = 1:10, y = runif(10))
df %>% ggvis(~x, ~y) %>% layer_ribbons()
a<-df %>% ggvis(~x, ~y + 0.1, y2 = ~y - 0.1) %>% layer_ribbons()
{% endhighlight %}
* 矩形图 `layer_rects()`举行的位置和大小由属性x,x2,y,y2确定
{% highlight r linenos %}
set.seed(1014)
df <- data.frame(x1 = runif(5), x2 = runif(5), y1 = runif(5), y2 = runif(5))
df %>% ggvis(~x1, ~y1, x2 = ~x2, y2 = ~y2, fillOpacity := 0.1) %>% layer_rects()
{% endhighlight %}
* 文本 `layer_text()`该函数有许多属性来控制文本的样式，text显示标签，dx,dy确定文字的四周边距，angle确定文字旋转的角度，font,fontSize,fontWeight,fontStyle分别确定字体名称，字体大小，字体粗细（加粗），字体风格（倾斜）
{% highlight r linenos %}
df <- data.frame(x = 3:1, y = c(1, 3, 2), label = c("a", "b", "c"))
df %>% ggvis(~x, ~y, text := ~label) %>% layer_text()
df %>% ggvis(~x, ~y, text := ~label) %>% layer_text(fontSize := 50)
df %>% ggvis(~x, ~y, text := ~label) %>% layer_text(angle := 45)
{% endhighlight %}
* 线 `layer_lines()`根据x的值自动进行排序后连线
{% highlight r linenos %}
t <- seq(0, 2 * pi, length = 20)
df <- data.frame(x = sin(t), y = cos(t))
df %>% ggvis(~x, ~y) %>% layer_lines()
{% endhighlight %}
* `layer_histograms()`&`layer_freqpolys()`
{% highlight r linenos %}
mtcars %>% ggvis(~mpg) %>% layer_histograms()
binned <- mtcars %>% compute_bin(~mpg) 
binned %>% 
  ggvis(x = ~xmin_, x2 = ~xmax_, y2 = 0, y = ~count_, fill := "black") %>%
  layer_rects()
{% endhighlight %}
* 平滑曲线 `layer_smooths()`
{% highlight r linenos %}
mtcars %>% ggvis(~wt, ~mpg) %>% layer_smooths()
smoothed <- mtcars %>% compute_smooth(mpg ~ wt)
smoothed %>% ggvis(~pred_, ~resp_) %>% layer_paths()
span <- input_slider(0.2, 1, value = 0.75)
mtcars %>% ggvis(~wt, ~mpg) %>% layer_smooths(span = span)
{% endhighlight %}
* 多图层堆积
{% highlight r linenos %}
mtcars %>% 
  ggvis(~wt, ~mpg) %>% 
  layer_smooths() %>% 
  layer_points()
mtcars %>% ggvis(~wt, ~mpg) %>%
  layer_smooths(span = 1) %>%
  layer_smooths(span = 0.3, stroke := "red")
{% endhighlight %}
