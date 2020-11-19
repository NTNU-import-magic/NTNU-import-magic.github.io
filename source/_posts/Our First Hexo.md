---
title: Our First Hexo
catalog: true
date: 2020-11-11 13:44:00
# subtitle: A succinct hexo theme...
# top: 999
header-img: /img/header_img/newhome_bg.jpg
tags:
- Hexo
categories:
- Blog
---

# Hexo Blog - Live My Life Theme

## 過程中遇到的小問題

### 當吃到 ```INFO Validating config WARN Deprecated config detected: “external_link“ with a Boolean``` 時
把```_config.yml```裡的
```yml=
external_link:
  enable: true|false
```
改成
```yml=
external_link:
  enable: true # Open external links in new tab
  field: site # Apply to the whole site
  exclude: ''
```
![](https://i.imgur.com/W04NGCO.png)

### 當吃到 ```lineno``` ```column``` ```filename```的 Warning
```
(node:117248) Warning: Accessing non-existent property 'lineno' of module exports inside circular dependency
(Use `node --trace-warnings ...` to show where the warning was created)
(node:117248) Warning: Accessing non-existent property 'column' of module exports inside circular dependency
(node:117248) Warning: Accessing non-existent property 'filename' of module exports inside circular dependency
(node:117248) Warning: Accessing non-existent property 'lineno' of module exports inside circular dependency
(node:117248) Warning: Accessing non-existent property 'column' of module exports inside circular dependency
(node:117248) Warning: Accessing non-existent property 'filename' of module exports inside circular dep
endency
```

![](https://i.imgur.com/hVyKWqP.png)



原因如[這裡](https://github.com/nodejs/node/pull/29935)

說白一點就是nodejs@14版本太高的問題，大部分我看到的文章都是要你降級程12版。

但我覺得太毒瘤太不資工正確了。

這是我所查到有用的三篇文章：
- [第一篇](https://www.haoyizebo.com/posts/710984d0/)
- [第二篇](https://github.com/stylus/stylus/pull/2538)（github上討論有關這個問題的處理方法）
- [第三篇](https://github.com/stylus/stylus/pull/2538/commits/16e2a6c6f96f80b0d700411879f1c13991a0a1a5)（github中nodejs@14 stylus在 ```lineno``` ```column``` ```filename``` 的error設定）

延續第三篇搭配第二篇，把路徑```node_module\nib\node_module\stylus\lib\nodes\index.js```
裡的
```js=
export.true = new export.Boolean(true);
export.false = new export.Boolean(false);
```
一起註解掉
```js=
/*export.true = new export.Boolean(true);
export.false = new export.Boolean(false);*/
```

![](https://i.imgur.com/a7QK3Ig.png)

## 想把每一篇文章底部的socialshare改成自己要的

像我，我只想要```twitter``` ```facebook``` ```google``` ```mail```

首先，先去```themes/livemtlife/layout/partial/socialshare.ejs```中把```<div>```裡的
```html=
<div class="social-share" data-initialized="true" data-disabled="tencent ,douban ,qzone ,linkedin ,facebook ,google ,diandian" data-wechat-qrcode-helper="" align="center">
```
中的 ```google``` 和 ```facebook``` 刪掉，因為它原本把兩者的link都disable掉了。(PS: ```data-wechat-qrcode-helper=""```也可以砍掉，因為我等一下會把```wechat```那段 ```<li></li>``` 砍掉

然後，將
```html=
<!-- 刪掉 wechat weibo QQ -->

    <li class="social-share-li">
      <a class="social-share-icon icon-wechat">
        <i class="fa fa-weixin fa-1x" aria-hidden="true"></i>
      </a>
    </li>
    <li class="social-share-li">
      <a target="_blank" class="social-share-icon icon-weibo">
        <i class="fa fa-weibo fa-1x" aria-hidden="true"></i>
      </a>
    </li>
    <li class="social-share-li">
      <a target="_blank" class="social-share-icon icon-qq">
        <i class="fa fa-qq fa-1x" aria-hidden="true"></i>
      </a>
    </li>
```
改成
```html=
<!-- 新增 google facebook -->

    <li class="social-share-li">
      <a target="_blank" class="social-share-icon icon-google">
        <i class="fa fa-google fa-1x" aria-hidden="true"></i>
      </a>
    </li>
    <li class="social-share-li">
      <a target="_blank" class="social-share-icon icon-facebook">
        <i class="fa fa-facebook fa-1x" aria-hidden="true"></i>
      </a>
    </li>
```
 ## 不想用不蒜子統計
 
 到```themes/livemylife/layout/partial/header.ejs```把以下的```<span></span>```給註記掉。
 
 ```html=
 <!-- 不蒜子统计 start -->
    <!--<span class="meta">
              Viewed <span id="busuanzi_value_page_pv"><i class="fa fa-spinner fa-spin"></i></span> Times
    </span>-->
<!-- 不蒜子统计 end -->
 ```