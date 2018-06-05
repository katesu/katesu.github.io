---
title: 嵌入影片RWD
category: css
tags: []date: 2018-03-17
---

[Hexo 標籤外掛(Tag Plugins)](http://localhost:4000/Hexo/2018/02/22/hexo-tag-plungis/)中的嵌入的 youtube 影片方式都固定尺寸的影片，也可藉由css設定修改成RWD

<!--more-->

## RWD影片範例
<div class="video-rwd">
    <iframe src="https://www.youtube.com/embed/uRtLmZwutII" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
</div>

## Idea
在`<iframe>`外層建立一個寬高等比例且寬度隨視窗縮放的容器，使`<iframe>`寬高與該容器相同。

## Code
```
{% raw %}
<div class="video-rwd">
    <iframe src="https://www.youtube.com/embed/uRtLmZwutII" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
</div>
{% endraw %}
```

```scss
.video-rwd{
    position: relative;
    width: 100%;
    height: 0;
    padding-bottom: 56.2%;
    iframe,
    object,
    embed{
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
    }
}
```

### 等比例的容器
youtobe 影片比例為 寬16:高9，等於 寬1:高0.5625，當`padding`和`margin`單位為 % 時會以父層的`width`為參考值，以此特性建立了`width: 100%`與父層同寬的`.video-rwd`，其`padding-bottom`為父層寬度的 56.52%。

當`.video-rwd`寬為 100px 時，`padding`是 56.52px，寬高比維持16:9。

使用`padding-top`或`padding-bottom`哪一個都可以，在此是藉其 % 以父層為參考值變動的特點，保持容器16:9的尺寸。

### 定位影片位置與尺寸
因為父層`.video-rwd`沒有高度，所以使用`position: absolute`將`<iframe>`定位在父層右上角，並且將寬高設定 100% 與父層相同，固定16:9的比例。

### Try & False
一開始是將`<iframe>`定位 top/left/bottom/right 0，完全對齊父層，結果影片只有300x150。

在 stackflow 查到
{% blockquote sg3s answered Sep 30 2011 at 18:55 https://stackoverflow.com/questions/3979000/iframe-and-conflicting-absolute-positions IFRAME and conflicting absolute positions %}
We need to style the iframe container mainly because an iframe on itself doesn't let itself be sized with top/left/bottom/right. But what will work is setting its width and height to 100%. 
{% endblockquote %}
`<iframe>`無法以 top/left/bottom/right 控制寬高尺寸而改成寬高 100%。

## References
1. [如何將youtube影片嵌入RWD(自適應網頁)](https://www.webdesigns.com.tw/youtube-rwd.asp) @一化網頁設計