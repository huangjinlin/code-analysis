<!-- TOC START min:1 max:3 link:true update:true -->
  - [flex-grammar](#flex-grammar)
  - [flex-examples](#flex-examples)
  - [bootstrap4-inputGroup](#bootstrap4-inputgroup)
  - [bootstrap3-inputGroup](#bootstrap3-inputgroup)
  - [solved-by-flexbox_input-add-on](#solved-by-flexbox_input-add-on)
  - [refer to](#refer-to)

<!-- TOC END -->


## flex-grammar
1.flex-wrap
```css
  /* 换行，第一行在上方 */
  .box{flex-wrap:wrap}
```
![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071008.jpg)
2.align-items
```css
  .box {
    align-items: flex-start | flex-end | center | baseline | stretch;
  }
```
![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071011.png)
3.flex
```css
  /* 默认值为0 1 auto */
  .item {
    flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
  }
```
4.flex-grow
flex-grow属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。
```css
  .item {
    flex-grow: <number>; /* default 0 */
  }
```
![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071014.png)


## flex-examples
![image](http://upload-images.jianshu.io/upload_images/4197259-69cf49aebd90899b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```css
  .box {
    display: flex;
    align-items: center;
  }
```
![image](http://upload-images.jianshu.io/upload_images/4197259-d4ff840daecaa285.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```css
  .box {
    display: flex;
    justify-content: center;
    align-items: center;
  }
```

## bootstrap4-inputGroup
```html
  <div class="input-group">
    <div class="input-group-prepend">
      <span class="input-group-text">@</span>
    </div>
    <input type="text" class="form-control">
    <div class="input-group-append">
      <span class="input-group-text">.00</span>
    </div>
  </div>
```
```less
  /*_variables.scss*/
  // $border-width = $input-btn-border-width $input-border-width = 1px
  // input-height-border = $input-border-width * 2
  $border-width:                1px !default;
  $input-btn-border-width:      $border-width !default;
  $input-border-width:                    $input-btn-border-width !default;
  $input-height-border:                   $input-border-width * 2 !default;
  //$line-height-base = $input-btn-line-height =  $input-line-height = 1.5
  $line-height-base:            1.5 !default;
  $input-btn-line-height:       $line-height-base !default;
  $input-line-height:                     $input-btn-line-height !default;
  $font-size-base:              1rem !default; // Assumes the browser default, typically `16px`
  $input-btn-padding-y:         .375rem !default;
  $input-btn-padding-x:         .75rem !default;
  $input-height-inner:                    ($font-size-base * $input-btn-line-height) + ($input-btn-padding-y * 2) !default;
  $input-height:                          calc(#{$input-height-inner} + #{$input-height-border}) !default;
  /*_forms.scss*/
  .form-control {
    display: block;
    width: 100%;
    height: $input-height;
    padding: $input-padding-y $input-padding-x;
    font-size: $font-size-base;
    line-height: $input-line-height;
    color: $input-color;
    background-color: $input-bg;
    background-clip: padding-box;
    border: $input-border-width solid $input-border-color;
  }
  /*_input-group.scss*/
  .input-group {
    position: relative;
    display: flex;
    flex-wrap: wrap; // For form validation feedback
    align-items: stretch;
    width: 100%;
    > .form-control{
      position: relative; // For focus state's z-index
      flex: 1 1 auto;
      // Add width 1% and flex-basis auto to ensure that button will not wrap out
      // the column. Applies to IE Edge+ and Firefox. Chrome does not require this.
      width: 1%;
      margin-bottom: 0;
    }
  }
  .input-group-prepend,
  .input-group-append {
    display: flex;
    .input-group-text + .input-group-text{
      margin-left: -$input-border-width;
    }
  }
  .input-group-prepend { margin-right: -$input-border-width; }
  .input-group-append { margin-left: -$input-border-width; }
  .input-group-text {
    display: flex;
    align-items: center;
    padding: $input-padding-y $input-padding-x;
    margin-bottom: 0; // Allow use of <label> elements by overriding our default margin-bottom
    font-size: $font-size-base; // Match inputs
    font-weight: $font-weight-normal;
    line-height: $input-line-height;
    color: $input-group-addon-color;
    text-align: center;
    white-space: nowrap;
    background-color: $input-group-addon-bg;
    border: $input-border-width solid $input-group-addon-border-color;
    @include border-radius($input-border-radius);

    // Nuke default margins from checkboxes and radios to vertically center within.
    input[type="radio"],
    input[type="checkbox"] {
      margin-top: 0;
    }
  }
```
## bootstrap3-inputGroup
```html
<div class="input-group">
  <span class="input-group-addon">$</span>
  <input type="text" class="form-control">
  <span class="input-group-addon">.00</span>
</div>
```
```less
  /*variables.less*/
  @padding-base-vertical:     6px;
  @padding-base-horizontal:   12px;
  @font-size-base:          14px;
  @line-height-base:        1.428571429; // 20/14
  @line-height-computed:    floor((@font-size-base * @line-height-base)); // ~20px
  @input-height-base:              (@line-height-computed + (@padding-base-vertical * 2) + 2);
  //** Large `.form-control` height
  /*input-groups.less*/
  .input-group {
    position: relative; // For dropdowns
    display: table;
    border-collapse: separate; // prevent input groups from inheriting border styles from table cells when placed within a table
    .form-control {
        // Ensure that the input is always above the *appended* addon button for
        // proper border colors.
        position: relative;
        z-index: 2;

        // IE9 fubars the placeholder attribute in text inputs and the arrows on
        // select elements in input groups. To fix it, we float the input. Details:
        // https://github.com/twbs/bootstrap/issues/11561#issuecomment-28936855
        float: left;

        width: 100%;
        margin-bottom: 0;
      }
  }
  .input-group-addon,
  .input-group .form-control {
    display: table-cell;

    &:not(:first-child):not(:last-child) {
      border-radius: 0;
    }
  }
  .input-group-addon{
    width: 1%;
    white-space: nowrap;
    vertical-align: middle; // Match the inputs
  }
  .input-group-addon {
    padding: @padding-base-vertical @padding-base-horizontal;
    font-size: @font-size-base;
    font-weight: normal;
    line-height: 1;
    color: @input-color;
    text-align: center;
    background-color: @input-group-addon-bg;
    border: 1px solid @input-group-addon-border-color;
    border-radius: @input-border-radius;
    // Nuke default margins from checkboxes and radios to vertically center within.
    input[type="radio"],
    input[type="checkbox"] {
      margin-top: 0;
    }
  }
  /*forms.less*/
  .form-control {
    display: block;
    width: 100%;
    height: @input-height-base; // Make inputs at least the height of their button counterpart (base line-height + padding + border)
    padding: @padding-base-vertical @padding-base-horizontal;
    font-size: @font-size-base;
    line-height: @line-height-base;
    color: @input-color;
    background-color: @input-bg;
    background-image: none; // Reset unusual Firefox-on-Android default style; see https://github.com/necolas/normalize.css/issues/214
    border: 1px solid @input-border;
    border-radius: @input-border-radius; // Note: This has no effect on <select>s in some browsers, due to the limited stylability of <select>s in CSS.
    .box-shadow(inset 0 1px 1px rgba(0,0,0,.075));
    .transition(~"border-color ease-in-out .15s, box-shadow ease-in-out .15s");
  }
```
## solved-by-flexbox_input-add-on
```html
<div class="InputAddOn">
  <span class="InputAddOn-item">…</span>
  <input class="InputAddOn-field">
  <button class="InputAddOn-item">…</button>
</div>
```
```css
  .InputAddOn {
    display: flex;
    margin-bottom: 1.5em;
  }
  .InputAddOn-field {
    flex: 1;
  }
  .InputAddOn-item {
    background-color: rgba(147, 128, 108, 0.1);
    color: #666666;
    font: inherit;
    font-weight: normal;
  }
  .InputAddOn-field,
  .InputAddOn-item {
    border: 1px solid rgba(147, 128, 108, 0.25);
    padding: 0.5em 0.75em;
  }
```
## refer to
  - css世界
  3.4.2 内联模型
  5.2 内联元素基石line-height
  8.1 line-height的另外一个朋友font-size
  - bootstrap3
  [doc](https://getbootstrap.com/docs/3.3/components/)
  [input-groups.less](https://github.com/twbs/bootstrap/blob/v3.3.7/less/input-groups.less)
  [variables.less](https://github.com/twbs/bootstrap/blob/v3.3.7/less/variables.less)
  [forms.less](https://github.com/twbs/bootstrap/blob/v3.3.7/less/forms.less)
  - bootstrap4
  [doc](http://getbootstrap.com/docs/4.1/getting-started/introduction/)
  [_input-group.scss](https://github.com/twbs/bootstrap/blob/v4-dev/scss/_input-group.scss)
  [_variables.scss](https://github.com/twbs/bootstrap/blob/v4-dev/scss/_variables.scss)
  [_forms.scss](https://github.com/twbs/bootstrap/blob/v4-dev/scss/_forms.scss)
  - Flex 布局教程
  [语法篇](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)
  [实例篇](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html)
  - solved-by-flexbox
  [demo](https://philipwalton.github.io/solved-by-flexbox/demos/input-add-ons/)
  [input-add-on.css](https://github.com/philipwalton/solved-by-flexbox/blob/master/assets/css/components/input-add-on.css)
