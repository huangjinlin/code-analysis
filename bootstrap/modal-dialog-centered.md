<!-- not to html -->
<!-- TOC START min:1 max:3 link:true update:true -->
  - [bootstrap4_modal-dialog-centered](#bootstrap4_modal-dialog-centered)
  - [solved-by-flexbox_vertical-centering](#solved-by-flexbox_vertical-centering)
  - [weui](#weui)
  - [cssWord](#cssword)
  - [refer to](#refer-to)

<!-- TOC END -->
## bootstrap4_modal-dialog-centered
```html
  <div class="modal fade">
    <div class="modal-dialog modal-dialog-centered">
    </div>
  </div>
```
```less
  // _variables.scss
  $zindex-modal:                      1050 !default;
  $modal-dialog-margin:               .5rem !default;
  // _modal.scss
  .modal {
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: $zindex-modal;
    display: none;
    overflow: hidden;
    // Prevent Chrome on Windows from adding a focus outline. For details, see
    // https://github.com/twbs/bootstrap/pull/10951.
    outline: 0;
    // We deliberately don't use `-webkit-overflow-scrolling: touch;` due to a
    // gnarly iOS Safari bug: https://bugs.webkit.org/show_bug.cgi?id=158342
    // See also https://github.com/twbs/bootstrap/issues/17695
  }
  .modal-dialog {
    position: relative;
    width: auto;
    margin: $modal-dialog-margin;
    // allow clicks to pass through for custom click handling to close modal
    pointer-events: none;
  }
  .modal-dialog-centered {
    display: flex;
    align-items: center;
    min-height: calc(100% - (#{$modal-dialog-margin} * 2));

    // Ensure `modal-dialog-centered` extends the full height of the view (IE10/11)
    &::before {
      display: block; // IE10
      height: calc(100vh - (#{$modal-dialog-margin} * 2));
      content: "";
    }
  }  
```

## solved-by-flexbox_vertical-centering
```html
  <div class="Aligner">
    <div class="Aligner-item Aligner-item--top">…</div>
    <div class="Aligner-item">…</div>
    <div class="Aligner-item Aligner-item--bottom">…</div>
  </div>
```
```css
  .Aligner {
    display: flex;
    align-items: center;
    min-height: 24em;
    justify-content: center;
  }

  .Aligner-item {
    flex: 1;
  }

  .Aligner-item--top {
    align-self: flex-start;
  }

  .Aligner-item--bottom {
    align-self: flex-end;
  }
```
## weui
```html
  <div class="weui-loading_toast">
      <div class="weui-mask_transparent"></div>
      <div class="weui-toast">
          <i class="weui-loading weui-icon_toast"></i>
          <p class="weui-toast__content">...</p>
      </div>
  </div>
```
```less
  // weui-mask.less
  .weui-mask_transparent{
      position: fixed;
      z-index: 1000;
      top: 0;
      right: 0;
      left: 0;
      bottom: 0;
  }
  // weui-toast.less
  .weui-toast {
      position: fixed;
      z-index: 5000;
      width: 7.6em;
      min-height: 7.6em;
      top: 180px;
      left: 50%;
      margin-left: -3.8em;
      background: rgba(17,17,17,0.7);
      text-align: center;
      border-radius: 5px;
      color: #FFFFFF;
  }
```

## cssWord
```html
  <div class="container">
      <div class="dialog">
          <div class="content">内容占位</div>
      </div>
  </div>
```
```css
  .container {
      position: fixed;
      top: 0; right: 0; bottom: 0; left: 0;
      /* for IE8 */
      background: url(data:image/png;base64,iVB...g==);
      /* for IE9+ */
      background: rgba(0,0,0,.5), none;
      text-align: center;
      white-space: nowrap;
      z-index: 99;
  }
  .container:after {
      content: "";
      display: inline-block;
      height: 100%;
      vertical-align: middle;
  }
  .dialog {
      display: inline-block;
      vertical-align: middle;
      border-radius: 6px;
      background-color: #fff;
      text-align: left;
      white-space: normal;
  }
```
## refer to
  - bootstrap4
  [doc](https://getbootstrap.com/docs/4.1/components/modal/#vertically-centered)
  [_variables.scss](https://github.com/twbs/bootstrap/blob/v4-dev/scss/_variables.scss)
  [_modal.scss](https://github.com/twbs/bootstrap/blob/v4-dev/scss/_modal.scss)
  - solved-by-flexbox
  [demo](https://philipwalton.github.io/solved-by-flexbox/demos/vertical-centering/)
  [aligner.css](https://github.com/philipwalton/solved-by-flexbox/blob/master/assets/css/components/aligner.css)
  - weui
  [loading.html](https://github.com/Tencent/weui.js/blob/master/src/loading/loading.html)
  [weui-mask.less](https://github.com/Tencent/weui/blob/5770268257b5d2d3de14e776296dc453969217f6/src/style/widget/weui-tips/weui-mask.less)
  [weui-toast.less](https://github.com/Tencent/weui/blob/master/src/style/widget/weui-tips/weui-toast.less)
  - cssWorld
  5.3.8基于vertical-align属性的水平垂直居中弹框
  [demo](http://demo.cssworld.cn/5/3-10.php)
