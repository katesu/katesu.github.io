---
title: Day3 Playing with CSS Variables and JS
category: JavaScript
tags: [native JS, JavaScript30, CSS]
date: 2018-03-09
---
JavaScript30 Day3 筆記
<!--more-->

### Functions
- (使用者)操作控制按鈕，(系統)控制圖片邊框、背景顏色、模糊程度
  - **使用者**操作按鈕決定圖片邊框、背景顏色、模糊程度
    - event:
    change(滑鼠移動 range bar 放開)
    mousemove(滑鼠在 range bar 上移動)
  - **系統**改變圖片邊框、背景顏色、模糊程度
    - document.style.setProperty(prop, value)

### Steps
1. 在 root(html) 宣告 CSS variables
2. change, mousemove handler: handleUpdate
3. 在 .controls input 綁訂 change, mousemove

### Fixed


### CSS
- variables
  daclare
    ```css=
    selector {
      --customName: value;
    }
    ```
  apply
    ```css=
    selector {
      prop: var(--customName)
    }
    ```
  specificity
    {% raw %}
      <p data-height="300" data-theme-id="0" data-slug-hash="BYxowx" data-default-tab="css,result" data-user="katesu" data-embed-version="2" data-pen-title="specificity of CSS variables" class="codepen">See the Pen <a href="https://codepen.io/katesu/pen/BYxowx/">specificity of CSS variables</a> by Kate Su (<a href="https://codepen.io/katesu">@katesu</a>) on <a href="https://codepen.io">CodePen</a>.</p>
      <script async src="https://static.codepen.io/assets/embed/ei.js"></script>
    {% endraw %}


### native JS
- 邏輯運算子短路求值(Short-circuit evaluation)
  - falsy: '', null, undefined, NaN, 0 
  - truthy: [], {}, 非 false 與 falsy
  - || 與 && 都是由左到右解析表達式
  - || (or)
    `exp1 || exp2` 
    - 第一個表達式為 false 或 falsy 則繼續向右解析直至任一表達式為 true 或 truthy，並回傳該表達式結果；所有表達式為 false 或 falsy 則回傳最後一個表達式的結果
    - 若 exp1 運算結果為 true 或 truthy
      || 回傳 exp1 結果
    - 若 exp1 運算結果為 false 或 falsy
      || 會進行 exp2 運算並且回傳結果
    
    ```js=
    var suffix = undefined || this.dataset.sizing || '';

    // 相當於
    if (undefined) {
      var suffix = undefined; {
    } else if (this.dataset.sizing){
      var suffix = this.dataset.sizing;
    } else {
      var suffix = '';
    }
    ```

  - && (and)
    `exp1 && exp2`
    - 第一個表達式為 true 或 truthy 則繼續向右解析直至所有表達式為  true 或 truthy為止；任一表達式結果為 false 或 falsy，即結束解析並回傳該表達式結果
    - 但其中只要表達式結果為 false 或 falsy，即停止解析並回傳**該表達式結果**

    ```js=
    var a = 1, b = 3;
    var result = a && b + 1 && a + 1
    
    // 相當於
    if (a){
      if (b + 1){
        var result = a + 1;
      } else {
        var result = b + 1
      }
    } else {
      var result = a
    }
    ```

    
- `el.dataset`
  - NodeList
    - It is a DOMStringMap object like a array but have a few methods of arrays
    - It is composed of all the custom `data-*` attributes set on the element
  - `el.dataset.customName` 取得自訂義 data 屬性
- `el.documentELement.style.setProperty(CSSprop, value)` 以 HTML inline style 操作 CSS 樣式
- `el.HTMLattribute`
  - `el.name` 取得 el 的 name 屬性
  - `el.value` 取得 el 的 value 屬性


## References
1. [運算式與運算子](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Guide/Expressions\_and\_Operators
) @MDN Web Docs
1. [Javascript 基礎打底系列 (三) - 邏輯運算子，與短路邏輯 (short circuit logic) 的應用
](http://sweeteason.pixnet.net/blog/post/43022921) @小雕雕的家
1. [HTMLElement.dataset - Web APIs](https://developer.mozilla.org/zh-TW/docs/Web/API/HTMLElement/dataset) @MDN Web Docs

