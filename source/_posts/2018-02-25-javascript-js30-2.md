---
title: Day2 CSS + JS Clock
category: JavaScript
tags: [native JS, JavaScript30]
date: 2018-02-25
---
JavaScript30 Day2 筆記
<!--more-->

### Functions
- 時針、分針、秒針依時間改變旋轉
  - **系統**每秒、分、時自動更新指針角度


### Steps
1. 宣告 setInterval function: setDate
    - get seconds/ minutes/ hours of current and turns them into degrees
      - 秒：secs/60算出比例乘上360度
      - 分：概念同上
      - 時：huors/12算出比例乘上360度
    - document.style.transform = rotate(...) 改變指針角度
2. setInterval(setDate, 1000)
    -  每1000毫秒(1秒)執行一次 setDate


### Fixed
- 指針與實際指針相差90度
  1. 原因：一開始水平指針被 CSS rotate(90)改變成垂直，JS 修改角度是從0度開始
  2. 作法：JS 每秒改變的角度還要加上90度

- 秒針歸零時會閃一下
  1. 原因：`transition: all 0.05s`，60秒450度到0秒90度是向後旋轉， transition 0.05s duration 會看到秒針閃一下
  2. 作法：
      - 讓秒針不歸零
      - 60秒到0秒之間取消 transition

### Improvements
  - 時針沒按比例移動，直接跳1/12格

### CSS
  - `transform-orign: 100% / x y`
  - `rotate(deg)`
    - +deg - 順時針
    - -deg - 逆時針

### Native JS
  - `new Date()` - 獲得當前時間
  - `new Date.getSeconds()` - 取得當前時間秒數
  - `new Date.getMinets()` - 取得當前時間分鐘
  - `new Date.getHours()` - 取得當前時間小時
  - `setInterval(func, milliseconds)` - 每多少毫秒重複執行 func

  
## References
- [WindowOrWorkerGlobalScope.setInterval() - Web APIs](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setInterval) @MDN Web Docs
- [CSS transform 能旋轉、傾斜、縮放變形 box](http://boohover.pixnet.net/blog/post/35341387
) @網頁藝術思考
- [CSS沒有極限 - CSS transform-origin](https://wcc723.github.io/css/2013/10/10/css-transform-origin/) @前端，沒有極限
