---
title: Day1 JavaScript Drum Kit
category: JavaScript
tags: [native JS, JavaScript30]
date: 2018-02-23
---
JavaScript30 Day1 筆記
<!--more-->

### Functions
- (使用者)按下指定按鍵按鈕(系統)會播出指定的聲音
  - **使用者**按下按鈕
    - event: keydown
  - **系統**播放指定樂器聲音
    - audio.play()


### Steps
1. 宣告 keydown handler: playSound
    - 取得特定按鍵的 keyCode 
    - 按到非特定按鍵即停止 function
    - 播放擁有與 keyCode 相同 `data-key` 的 audio
1. 宣告 transitionend handler: removeTransition
    - 對畫面中代表該按鍵的元素添加 class 開始 active 的 transition 動畫
    - 綁定各按鍵元素，監聽 transitionend 事件，偵測按鍵動畫以結束移除 class  
1. 綁訂事件
    - 對 window 綁訂 keydown
    - 對.key 綁訂 transitionend 


### Fixed
- 連續敲擊鍵盤並沒有連續播放
  1. 原因：必須等音樂播放完畢後再觸發 keydown 才會播放
  2. 方法：`audio.currentTime = 0`，強制事件觸發音樂就從0秒播放

### Native JS
- `el.classList.add / remove / toggle('...')`
- event listener
  - keydown
  - transitionend
  - event object has different properties within every event
  - this within a event handler is the.object which invokes it

- `document.querySelector()` - an element
- `document.querySelectorAll()` - all  elements
- ```audio[data-key=`${...}`]```
  - 允許嵌入運算式的字面量字串，取代 '...' + variable + '...' 
  - '...' 會使 ${ ... } 轉為字串
  - 不需插入換行符號即可直接換行
  - 也可作為一般的字串使用

- `${ ... }` - 計算任何的表達式
  - if() only one line statement

- audio
  - `audio.play()` - play the audio
  - `audio.currentTime = 0` - jump to specified position (in seconds) of audio

- ES6
  - const
    - does not hoisting
    - only works inside declared scope
    - must valued when declared
    - cannot revalued again if valued

  

## References
- [let 和 const 命令](http://es6.ruanyifeng.com/#docs/let#const-%E5%91%BD%E4%BB%A4) @ECMAScript 6入门
