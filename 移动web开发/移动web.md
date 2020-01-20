# 移动web端
#### 流式布局
- 就是百分比布局，非固定像素，内容向两侧填充，理解成流动的布局，称为流式布局
#### 移动端的viewport-视觉窗口
- viewport是移动端特有。这是一个虚拟的区域，承载网页的，DOM检查不到。
- 承载关系：浏览器承载viewport,viewport承载网页（浏览器---->viewport---->网页）
- pc端网页放到移动端，并正常浏览的过程叫适配
- dpr屏幕像素比
![](images/viewport.png)
   + iphone3 一个物理像素点的大小和一个px大小正好一样，一个px大小的屏幕里只有一个物理像素点  一个物理像素点装10kb
   + iphone4 一个px大小的屏幕里有两个物理像素点  一个物理像素点装5kb 图片质量降低
   + iphone6 plus  一个px大小的屏幕里有三个物理像素点  一个物理像素点装3.kb  物理像素显示出来
   + 为了让图片清晰 在iphone4下准备2px-20kb的图片  （2px变大，图片质量也变大）  压缩显示到1px屏幕，图片原本质量没变，只是尺寸变了，一个物理像素就是10kb
##适配方案
#### 标准适配方案
- 问题：pc端网页放在移动端会出现缩放效果。
- 适配要求：
  + 网页宽度必须和浏览器保持一致(浏览器的宽度装载不了网页的宽度会出现滚动条，浏览器和设备一致，viewport和浏览器一致)
  + 默认显示的缩放比例和PC端保持（缩放比例1.0）
  + 不允许用户自行缩放网页
  + 满足这些要求达到了适配，国际上通用的适配方案，标准的移动端适配方案。
- 适配设置：
  + 如果任何设置都没有，默认走的就是viewport的默认设置
  + `<meta name="viewport">` :设置视口的标签,在head里面并且应该紧接着编码设置
  + viewport的功能：
      1. width    可以设置宽度   (device-width 当前设备的宽度)
      2. height   可以设置高度
      3. initial-scale  可以设置默认的缩放比例
      4. user-scalable  可以设置是否允许用户自行缩放
      5. maximum-scale  可以设置最大缩放比例
      6. minimum-scale  可以设置最小缩放比例
  + 在`<meta name="viewport" content="" >`content="" 使用以上参数
      1. width=device-width   宽度一致比例是1.0 视口和浏览器一样，视口和网页一致
      2. initial-scale=1.0    宽度一致比例是1.0
      3. user-scalable=no     不允许用户自行缩放  （yes，no  1,0）
      标准适配方案：
      ``` 
      <meta name="viewport" content="width=device-width,initial-scale=1.0,user-scalable=0">
      ```
  + meta:vp + tab  快捷方式
#### 非主流适配方案（淘宝）
   + 页面的真实尺寸会比在设备的上尺寸要大几倍
   + 假设设备是iphone4 -> 320px -> 网页尺寸 640px
   + 缩放操作，有2倍的  有3倍  和屏幕像素比(drp)有关系
   + 什么是屏幕像素（drp:物理像素，像素点） px(页面的尺寸单位)
   + 物理像素 是设备显示屏的最小可视颗粒的大小  
   + 以前的手机（直板手机），现在有 高清显示屏  视网膜屏  retina屏（更多的像素点压缩在一块屏幕里）
   + 显示的效果就提高了更细腻，但是在显示同等质量的图片的时候（模糊效果）
     + 屏幕清晰度提高了，但是网页质量图片质量不提高，会产生模糊效果
     +
   + 在屏幕像素比（一个px宽的屏幕能放几个物理像素）高的设备  图片（非矢量）显示会模糊
   + 提高网页的清晰度  根据屏幕的像素比 来缩放网页
   + 但是这样的适配方案成本非常高
   + 一般的企业开发当中使用的还是标准化设置
   + 在高清显示屏当中：图片可能会失真（模糊）
#### 版心
- 最大宽度设置成了640px  max-width: 640px;
- 路径的绘制
- 设计稿psd的尺寸就是640px
  + 目的：当设备的尺寸比设计稿不至于失真
- 640px的尺寸设计稿的原因：根据当前主要流行的设备尺寸有关系iphone4,4s 尺寸320px
- 750px的设计稿：参考原型iphone6 尺寸375px
- 最小宽度320px  保证最小的宽度320px不让页面错乱   min-width: 320px;


 
#### 不建议在移动端使用jquery  
   + 可以使用jquery,但是不建议
   + jquery  做了很多桌面浏览器(pc端浏览器)的兼容问题 特别是IE，但是移动端没有IE浏览器
   + 移动端主流的浏览器：谷歌 火狐（2016年停止了维护和更新） safari浏览器  百度  360 qq ...
   + 特点：内核基本上都是  webkit  或者 blink  兼容  -webkit-
   + 使用H5的api 或者说使用一个 叫做： zepto.js 的库（基于高版本浏览器开发）  
#### box-sizing
   + 移动端以流式布局为主,百分比布局,非固定像素布局
   + 无法准确计算容器的尺寸 
   + `box-sizing: border-box; `防止内容溢出  不出现滚动条  提供用户体验
#### 点击高亮
   + 轻击 轻触 高亮效果`-webkit-tap-highlight-color: red;`
   + 轻击 轻触 不高亮效果`-webkit-tap-highlight-color: transparent;`
#### 二倍图解决失真问题 
   + 精灵图压缩后才可以提高图片的质量，定位也要缩小一倍
#### 图片的下间隙
```
        body{
            /*font-size: 0px;*/
        }
        img{
            display: block;
        }
        img{
            vertical-align: middle;
        }
```
   + transform层级会提高 
#### 移动端touch事件
- 解释touch:
   + touch是移动端的触摸事件 而且是一组事件
   + touchstart 当手指触摸屏幕的时候触发
   + touchmove 当手指在屏幕来回的滑动时候触发
   + touchend 当手指离开屏幕的时候触发
   + touchcancel 当被迫终止滑动的时候触发（来电，弹消息）
   + 利用touch相关事件实现移动端常见滑动效果和移动端常见的手势事件
- 使用touch:
   + 绑定事件 box.addEventListener('touchstart',function () { });
   + 事件对象
   1. 名字：TouchList------触摸点（一个手指触摸就是一个触摸点，和屏幕的接触点的个数）的集合
   2. changedTouches    改变后的触摸点集合
   3. targetTouches     当前元素的触发点集合
   4. touches           页面上所有触发点集合
- 触摸点集合在每个事件触发的时候会不会去记录触摸
   1. changedTouches 每个事件都会记录
   2. targetTouches，touches 在离开屏幕的时候无法记录触摸点
- 分析滑动实现的原理：
   1. 就是让触摸的元素随着手指的滑动做位置的改变
   2. 位置的改变：需要当前手指的坐标
   3. 在每一个触摸点中会记录当前触摸点的坐标 e.touches[0] 第一个触摸点
   4. clientX clientY      基于浏览器窗口（视口）
   5. pageX   pageY        基于页面（视口）
   6. screenX screenY      基于屏幕
#### 移动端的手势事件（移动端没有自己封装）
- swipe swipeLeft swipeRight swipeUp swipeDown
- 左滑和右滑手势怎么实现
```
    var bindSwipeEvent = function (dom,leftCallback,rightCallback) {
            /*手势的条件*/
            /*1.必须滑动过*/
            /*2.滑动的距离50px*/
            var isMove = false;
            var startX = 0;
            var distanceX = 0;
            dom.addEventListener('touchstart',function (e) {
                startX = e.touches[0].clientX;
            });
            dom.addEventListener('touchmove',function (e) {
                isMove = true;
                var moveX = e.touches[0].clientX;
                distanceX = moveX - startX;
            });
            dom.addEventListener('touchend',function (e) {
                /*滑动结束*/
                if(isMove && Math.abs(distanceX) > 50){
                    if(distanceX > 0){
                        rightCallback && rightCallback.call(this,e);//this是当前的dom对象
                    }else{
                        leftCallback && leftCallback.call(this,e);
                    }
                }
                /*重置参数*/
                isMove = false;
                startX = 0;
                distanceX = 0;
            });
        };
        bindSwipeEvent(document.querySelector('.box'),function (e) {//function是windown对象
            console.log(this);
            console.log(e);
            console.log('左滑手势');
        },function (e) {
            console.log(this);
            console.log(e);
            console.log('右滑手势');
        });

    }
```
####  tap事件（移动端没有自己封装）
- tap事件  轻击 轻触  （响应速度快）
-  移动端也有click事件 （在移动为了区分是滑动还是点击，click点击延时300ms）
- 影响用户体验 响应太慢了。
- 提高移动端点击响应，提高用户体验
- 解决方案：
  + 使用tap事件（不是移动端原生事件，通过touch相关事件衍生过来） （zepto.js tap事件）了解其原理
  ```
       window.onload = function () {
           /*使用tap事件*/
           /*1. 响应的速度比click要快   150ms */
           /*2. 不能滑动*/
           var bindTapEvent = function (dom, callback) {
               /*事件的执行顺序*/
               /*在谷歌浏览器模拟看不到300ms的效果*/
               /*在真机上面才能看看到延时效果*/
               var startTime = 0;
               var isMove = false;
               dom.addEventListener('touchstart', function () {
                   //console.log('touchstart');
                   startTime = Date.now();
                   /*Date.now();*/
               });
               dom.addEventListener('touchmove', function () {
                   //console.log('touchmove');
                   isMove = true;
               });
               dom.addEventListener('touchend', function (e) {
                   //console.log('touchend');
                   console.log((Date.now() - startTime));
                   if ((Date.now() - startTime) < 150 && !isMove) {
                       callback && callback.call(this, e);
                   }
   
                   startTime = 0;
                   isMove = false;
               });
               /*dom.addEventListener('click',function () {
                //console.log('click');
                });*/
           }
   
           bindTapEvent(document.querySelector('.box'), function (e) {
               console.log(this);
               console.log(e);
               console.log('tap事件')
           });
       };
  ```
  + 使用一个叫：fastclick.js 提供移动端click响应速度的 https://www.bootcdn.cn/fastclick/
   1. 下载：https://cdn.bootcss.com/fastclick/1.0.6/fastclick.min.js
   2. 使用：
     ```
        <script src="../js/fastclick.min.js"></script>
        <script>
            /*当页面的dom元素加载完成*/
            document.addEventListener('DOMContentLoaded', function() {
                /*初始化方法*/
                FastClick.attach(document.body);
            }, false);
            /*正常使用click事件就可以了*/
        </script>
    ```
#### 两栏自适应-小技巧
```        
            一个元素设浮动
            另外一个设overflow: hidden;
            /*让这个元素绝对绝缘  bfc*/
            /*不让其他浮动元素影响自己*/
            /*不让自己的浮动去影响别的元素*/
           
```
#### 区域滚动效果-iScroll
- 条件：一个容器装着一个容器html结构
  + 找到大容器
  + 子容器大于父容器
  ```
  //移动端使用e.preventDefault()禁止滚动及取消
  window.onload = function () {
  	document.querySelector('.jd_cateLeft').addEventListener('touchmove',function(e){
  
  	e.preventDefault();
  
  });
  document.querySelector('.jd_cateRight').addEventListener('touchmove',function(e){
  
  	e.preventDefault();
  
  });
      /*区域滚动效果*/
      /*条件：一个容器装着一个容器html结构*/
      /*找到大容器*/
      /*子容器大于父容器*/
      new IScroll(document.querySelector('.jd_cateLeft'),{
          scrollX:false,
          scrollY:true
      });
      new IScroll(document.querySelector('.jd_cateRight'),{
          scrollX:true,
          scrollY:false
      });
  }
  ```
## 响应式布局
#### 设备划分
![](images/设备划分.png)  
#### 媒体查询
- 使用媒体查询能针对不同屏幕区间设置不同的布局和样式
- 怎么使用媒体查询：关于媒体查询 @media
- 语法： @media screen and (max-width: 768px) and (min-width: 320px){属性样式}
- 前端开发资源库：https://www.awesomes.cn/
#### bootstrap--查文档
- 简介
   + ui框架，有预制界面组件。css html js。用于开发响应式布局、移动设备优先的 WEB 项目。
   + 响应式框架：amazeui
   + 可以自定义样式，修改默认样式。
   + 底层是媒体查询
- 基本模板
```
   <!--h5文档申明-->
   <!DOCTYPE html>
   <!--文档语言申明  en英文 zh-CN中文简体 zh-tw中文繁体 -->
   <html lang="zh-CN">
   <head>
       <!--文档编码申明-->
       <meta charset="utf-8">
       <!--要求当前网页使用浏览器最高版本的内核来渲染-->
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <!--视口的设置：视口的宽度和设备一致，默认的缩放比例和PC端一致，用户不能自行缩放-->
       <meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=0">
       <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！ -->
       <!-- 优先加载和浏览器解释 -->
   
       <title>title</title>
   
       <!-- Bootstrap 核心样式-->
       <link href="../lib/bootstrap/css/bootstrap.css" rel="stylesheet">
       <!-- html5shiv 和  respond 分别用来解决IE8版本浏览器不支持 H5标签和媒体查询的  不兼容问题-->
       <!-- HTML5 shiv and Respond.js for IE8 support of HTML5 elements and media queries -->
       <!-- 警告：不能以file形式打开，本地打开。最好http://打开 -->
       <!-- WARNING: Respond.js doesn't work if you view the page via file:// -->
       <!-- 在 IE 9 以下引入-->
       <!--[if lt IE 9]>
       <script src="../lib/html5shiv/html5shiv.min.js"></script>
       <script src="../lib/respond/respond.min.js"></script>
       <![endif]-->
   </head>
   <body>
   <!--TODO-->
    
   <!-- bootstrap依赖jquery-->
   <!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->
   <script src="../lib/jquery/jquery.min.js"></script>
   <!-- bootstrap js 核心文件-->
   <!-- Include all compiled plugins (below), or include individual files as needed -->
   <script src="../lib/bootstrap/js/bootstrap.min.js"></script>
   </body>
   </html>
```
- Normalize.css和reset.css
   + Normalize.css：这是由 Nicolas Gallagher 和 Jonathan Neal 维护的一个CSS 重置样式库。
   + reset.css自己写的
   +  共同点：都是重置样式库，增强浏览器的表现一致性
   + 不同点：举个例子（ul）
     1. reset.css   list-style:none ---因为需求
     2. normalize.css 不会重置ul样式 ---本身已经在每个浏览器表现一致的元素
   + 一句话：都是增强浏览器的表现一致性，本身一致的reset.css可能会去改，但是normalize不会重置已经一致的元素
- .container-响应式布局容器；.container-fluid-流式布局容器
- 栅格系统
   + 其实就是行和列的布局，网格状布局
   + 行.row：.container容器默认有15px的左右内间距  .row 填充父容器的15px的左右内间距   margin-left,margin-right -15px拉伸 
   + 列：col-\*-*  col：列样式：*不确定（参数）
     - 第一个*：屏幕的大小
        1. 大屏设备     lg   大屏设备以上生效包含本身
        2. 中屏设备     md   中屏设备以上生效包含本身
        3. 小屏设备     sm   小屏设备以上生效包含本身
        4. 超小屏设备   xs   超小屏设备以上生效包含本身
     - 第二个*：每一行的分等份，默认分成12等份 ，数字代表的是占多少份
   + ![](images/栅格.png)  
   + 栅格嵌套
   + 列的偏移 col-xs-offset-1
   + 列的排序 
     1. push 往后推 col-xs-push-9
     2. pull 往前拉 col-xs-pull-3
 - 响应式工具
   + 针对不同设备展示或隐藏页面内容
   + ![](images/响应式工具.png) 
   + 3.2版本以后  建议使用hidden
- 常用类：
  + .container
  + .row  .col-\*-*  .col-\*-offset-*  .col-\*-pull-*  .col-\*-push-*
  + 浮动:.pull-left .pull-right 
  + 文字:.text-center .text-right .text-left  
  + 响应式工具：hidden-xs hidden-sm hidden-md hidden-lg

#### 自定义字体图标
```angular2
/*自定义字体图标*/
/*1.通过@font-face定义自己的字体*/
@font-face {
    /*2.申明自己的字体名称*/
    font-family: 'wjs';
    /*3.引入字体文件（约束某一段字符代码什么图案）*/
    src:
    url(../fonts/MiFie-Web-Font.svg) format('svg'),
    url(../fonts/MiFie-Web-Font.eot) format('embedded-opentype'),
    url(../fonts/MiFie-Web-Font.ttf) format('truetype'),
    url(../fonts/MiFie-Web-Font.woff) format('woff');
}
/*4.怎么使用维护性更好*/
.wjs_icon{
    font-family: wjs;
}
.wjs_icon_phone::before{
    content: "\e908";
}
```
#### less（预编译语言）--查文档
- cmd命令行编译 lessc text.less text.css
- 配置自动编译 webstrom
- 注释： /**/--可以编译在css件中   //---css不支持，不会编译在css文件中
- 变量：@mainColor:#e92322; @className:box;
    + 必须@前缀，：是等于的以上，必须分号结束；
    + 不能以数字开头，不能包含特殊字符，区分大小写
    + 使用：background: @mainColor;
    + 字符拼接：.@{className}{
             color: @mainColor;
           }
- mixins（混入，方法、函数混入）
    + 定义函数 .w50(){
             width: 50%;
           }
    + 定义函数包含参数 
      1. 定义了参数（没有默认值），调用的时候必须传参
      2. 怎么定义默认值 和定义变量值是一样的
      3. 定义了参数（有默认值），可传可不传
       ```
          .borderRadius(@width:100px){
                 border-radius: @width;
                 -webkit-border-radius:@width;
                 -moz-border-radius:@width;
                 -o-border-radius:@width;
                 -ms-border-radius:@width;
               }
    + 调用函数
       ```
         .w50-f_left{
           .w50();
           .borderRadius(20px);
         } 
 - 嵌套 
    + 需要连接的情况：&  (如:hover)  
 - Import 导入 
    + @import "文件名";
 - 函数（内置函数 运算）查文档
#### 直接在浏览器端使用less
- 无自动化编译工具
- less无法在浏览器端直接使用
- 浏览器不识别
- 必须解析成css代码
- 通过less解析插件（javascript）--less.js
- 引入less文件需要加上 type="text/less"
- less.watch(); 无刷新预览样式
- 以http形式打开网页预览
#### em和rem
- rem认识
    + em rem是相对单位
    + em大小是基于父元素的字体大小
    + rem的大小是基于？？？
       1. 浏览器默认的字体大小是16px
       2. r 意思 root 根元素，html标签 
       3. rem的大小是基于html元素的字体大小
- 适配方案rem：宽度和高度都能做到适配（等比缩放）
    + 思路：通过控制html上的字体大小去控制页面上所有已rem为单位的基准值控制尺寸
    + 把页面上px单位转换成rem单位
    + 页面制作的时候 psd 上的量取的px转成rem使用
    + 怎么换算？？？预设一个基准值 方便计算 100px（html{font-size: 100px;}） 
    + 适配的时候设置基准值  320px  50px 怎么算：（640px 100px ===320px 50px）
    + 换算公式：当前rem基准值 = 预设的基准值 / 设计稿宽度 * 当前设备的宽度 
    + 怎么去改变rem基准值 （js换算，媒体查询推荐）
  ```
       @media (min-width: 320px) {
             html{
                 font-size: 50px;
             }
         }
         @media (min-width: 414px) {
             html{
                 font-size: 64.6875px;
             }
         }
         @media (min-width: 640px) {
             html{
                 font-size: 100px;
             }
         }
  ```
  - rem+less适配（less用来维护适配方案）
    + 变量:rem适配方案不好维护  设备会更新  设计稿尺寸  预设基准值
       ```
         //适配主流设备十几种
         @adapterDeviceList:750px,720px,640px,540px,480px,424px,414px,400px,384px,375px,360px,320px;
         //设计稿尺寸
         @psdWidth:750px;
         //预设基准值
         @baseFontSize:100px;
         //设备的种类
         @len:length(@adapterDeviceList);

        ```
    + mixins
        ```angular2
        //遍历使用的是for循环
        //less没有循环语法
        //使用函数的迭代 死循环
        //根据数组的长度去停止当前循环
        //给函数的执行附加条件
        //需要序号来判断  通过序号遍历 @index 1 开始
        //遍历成功
        .adapterMixin(@index) when(@index > 0){
            @media (min-width:extract(@adapterDeviceList,@index)){
              html{
                font-size: @baseFontSize/@psdWidth * extract(@adapterDeviceList,@index);
              }
            }
        
          .adapterMixin(@index - 1);
        }
    
        ```
    + adapter.less中调用
        ```angular2
           .adapterMixin(@len);
        ```
#### 移动端布局的适配
- 伸缩布局 flex
- 流式布局 百分比
- 响应式 媒体查询（超小屏的时候：流式布局）
- 以上三种共同点：元素只能做宽度的适配（排除图片）
- rem布局
#### zepto.js
- 轻量、高级浏览器的JavaScript库（移动端）
#### swiper.js
- 应用较广泛的移动端网页触摸内容滑动js插件
#### cors、jsonp
#### 瀑布流
#### 适配移动端
- 库-电脑/很多功能/js功能/集合工具函数的方法 插件-内存条/功能单一  
- 框架：
  + ui框架（bootstrap包含了若干个插件--完整的功能） (妹子ui,jqueryUI,easyUI,jqueryMobile,mui,framework7)
    1. 关于移动端的UI框架：bootstrap,jqueryMobile,mui,framework7
    2. 模板引擎：artTemplate,handlebars,mustache,baiduTemplate,velocity,underscore
  + js框架（带有一定的开发思想，不涉及样式）-vue 
     mvc:模型、视图、控制器，把系统分成若干份模块
  3. app
#### meta
- ios是否运行创建快捷启动方式
    ```<meta content="yes" name="apple-mobile-web-app-capable">```
- ios顶部通知栏的样式 黑色
    ```<meta content="black" name="apple-mobile-web-app-status-bar-style">```
- 遇到数字不让转成电话号码格式
    ```<meta content="telephone=no" name="format-detection">```
- 网站的说明
    ```<meta name="description" content="....">```
- 网站关键字
     ```<meta name="Keywords" content="....">```
- ```<link type="image/x-icon" rel="shortcut icon" href="images/favicon.ico">```
  




​    



