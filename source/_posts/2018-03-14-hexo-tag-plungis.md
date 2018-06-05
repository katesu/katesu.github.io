---
title: Hexo 標籤外掛(Tag Plugins)
category: Hexo
tags: []
date: 2018-03-14
---

標籤外掛能夠引用文章內容或是嵌入外部的影片、程式碼

<!--more-->

## 文句引用
```
{% blockquote [author[, source]] [link] [source_link_title] %}
引用內容
{% endblockquote %}
```

### 一般的quote

```
{% blockquote %}
可愛就是正義!
{% endblockquote %}
```

{% blockquote %}
可愛就是正義!
{% endblockquote %}

### quote 具作者與出處
```
{% blockquote ディオ・ブランド, ジョジョの奇妙な冒険Part1 ファントムブラッド %}
俺は人间をやめるぞ、JOJO
{% endblockquote %}

```

{% blockquote ディオ・ブランド, ジョジョの奇妙な冒険Part1 ファントムブラッド %}
俺は人间をやめるぞ、JOJO
{% endblockquote %}
   
   
   
## 嵌入 YouTube
```
{% youtube 影片ID %}
```

{% youtube uRtLmZwutII%}
但影片尺寸無法調整。

改用 Swig 標籤 raw 嵌入 YouTube 的嵌入程式碼，
raw 標籤中的內容不會被轉譯。

```
{% raw %}
<iframe width="854" height="480" src="https://www.youtube.com/embed/uRtLmZwutII" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
{% endraw %}
```

{% raw %}
<iframe width="854" height="480" src="https://www.youtube.com/embed/uRtLmZwutII" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
{% endraw %}

   
   
## 嵌入程式碼

### JSFiddle
```
{% jsfiddle shorttag [tabs] [skin] [width] [height] %}
```

### CodePen
使用 raw 標籤，嵌入方法與 raw 嵌入 YouTube 相同

### gist
```
{% gist gist_id [/filename] %}
```

{% gist katesu/4feded35cd1b78051d9996f3a6942aeb %}




## References
1. [標籤外掛（Tag Plugins）](https://hexo.io/zh-tw/docs/tag-plugins.html) @Hexo
1. [hexo嵌入在线代码演示（codepen、jsFiddle等）](https://noname4me.github.io/2017/10/21/hexo-iframe/) @辣手摧花


