<h1>meta之h5页面所存在的缓存问题</h1>

	自从h5的出现，web端又一次站在了风口浪尖上。

	正题：

	html5是制作手机移动页面的工具，但是今天发现的问题是当我们的h5页面嵌入到原生的ios应用中后，

页面中有东西更新的时候，手机端并不能够实时的响应我们所做出的改变。于是，便想到是缓存的原因。

    在浏览器上，我们可以刷新或强制刷新，但是移动页面已经嵌入到了原生应用里面，没有了地址栏，我们

似乎不太灵光了。

    这时，<meta>隆重登场。

    1，<meta http-equiv="pragram" content="no-cache"> 

	禁止浏览器从本地缓存中调阅页面。

	2，<meta http-equiv="cache-control" content="no-cache, must-revalidate"> 
	
	网页不保存在缓存中，每次访问都刷新页面。

	3，<meta http-equiv="expires" content="0">

	网页在缓存中的过期时间为0，一旦网页过期，必须从服务器上重新订阅。

	此三种meta标签都是可以清除页面缓存，从而达到实时更新的效果的。

	只好拿来这里炫一下了。

 二、再来说说htmll5页面的其它meta标签的作用吧

  一般我们在页面上加入<meta name="viewport" content=""> view指的是屏幕缩放。

  其中，meta中的content中有以下几个属性：

  width：指的是viewport的宽度 [一般是device-width],

  hright: 指的是viewport的高度 [223-10000]，(这个没有用过)

  user-scalable [yes | no]是否允许缩放

  initial-scale [数值] 初始化比例（范围从 > 0 到 10）

  minimum-scale [数值] 允许缩放的最小比例

  maximum-scale [数值] 允许缩放的最大比例

 target-densitydpi 值有以下（一般推荐设置中等响度密度或者低像素密度，后者设置具体的值dpi_value，另外webkit内核已不准备再支持此属性）

     -- dpi_value 一般是70-400//没英寸像素点的个数

     -- device-dpi设备默认像素密度

     -- high-dpi 高像素密度

     -- medium-dpi 中等像素密度

     -- low-dpi 低像素密度


 虽然这里面有很多，但是我们一般在content里面只写几个 类似这样：

 <meta name="viewport" content=" initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />

 这条就是初始化比例为1，缩放最大比例为1，不允许用户缩放。

 再来说说我们熟悉的meta

 1 <!-- 声明文档使用的字符编码 -->

    <meta charset='utf-8'>

 2  <!-- 优先使用 IE 最新版本和 Chrome 这个在一些项目中用过，主要对付的是360等国产浏览器-->

    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"/>

 3	<!-- 页面描述 -->

    <meta name="description" content="不超过150个字符"/>

 4  <!-- 页面关键词 -->

    <meta name="keywords" content=""/>

 5  <!-- 启用360浏览器的极速模式(webkit) -->

    <meta name="renderer" content="webkit">

 6  <!-- 添加 RSS 订阅 -->

    <link rel="alternate" type="application/rss+xml" title="RSS" href="/rss.xml"/>

 7  <!-- 添加 favicon icon -->

    <link rel="shortcut icon" type="image/ico" href="/favicon.ico"/>

 8 	<!-- windows phone 点击无高光 -->

    <meta name="msapplication-tap-highlight" content="no">


另外 针对苹果应用 还有

1、开启对web app程序的支持

	<meta name="apple-mobile-web-app-capable" content="yes">

说明：

    网站开启对web app程序的支持，其实意思就是删除默认的苹果工具栏和菜单栏，开启全屏显示

2、 改变顶部状态条的颜色

	<meta name="apple-mobile-web-app-status-bar-style" content="black" />

说明：

    在 web app 应用下状态条（屏幕顶部条）的颜色；

    默认值为 default（白色），可以定为 black（黑色）和 black-translucent（灰色半透明）；

 3、safari 浏览器有一个“添加到主屏幕”的功能，用户可以像保存书签一样把一个网站添加到主屏幕，下次用户直接点击主屏幕上的图标就能进入网站。

	这个功能不仅方便用户快速访问我们的网站，而且也使我们的 WebApp 更像一个原生应用

	因为 iOS 分辨率，所以 icon.png 图片的尺寸也各不相同，我们可以通过sizes属性来分别定义，iOS 系统会自动获取向匹配的图片

	<span style="font-size:14px;"><!-- iOS 图标 begin -->  
        <link rel="apple-touch-icon-precomposed" href="/apple-touch-icon-57x57-precomposed.png"/>  
        <!-- iPhone 和 iTouch，默认 57x57 像素，必须有 -->  
        <link rel="apple-touch-icon-precomposed" sizes="114x114" href="/apple-touch-icon-114x114-precomposed.png"/>  
        <!-- Retina iPhone 和 Retina iTouch，114x114 像素，可以没有，但推荐有 -->  
        <link rel="apple-touch-icon-precomposed" sizes="144x144" href="/apple-touch-icon-144x144-precomposed.png"/>  
        <!-- Retina iPad，144x144 像素，可以没有，但推荐有 -->  
	</span>  


扩展：
	1,为用户加上提示

通过添加一个JavaScript代码来邀请用户添加到主屏幕，该库使用了HTML5的本地存储跟踪是否已经显示过了，以避免重复出现。

目前使用比较多和有在更新的一个库来自这里：http://cubiq.org/add-to-home-screen

	2、设置桌面图标的标题

为了在主屏达到最好的显示效果，title最好限制在六个中文长度内，超长的内容会被隐藏：

	<span style="font-size:14px;"><meta name="apple-mobile-web-app-title" content="标题"></span> 


	3、设置启动画面 

	当用户点击主屏图标打开 WebApp 时，系统会展示启动画面，在未设置情况下系统会默认显示该网站的首页截图，当然这个体验不是很好，所以我们需要通过以下代码来自定义启动画面：

	<link rel="apple-touch-startup-image" href="Startup.png" /> 

	<!-- iOS 启动画面 begin -->  
        <link rel="apple-touch-startup-image" sizes="768x1004" href="/splash-screen-768x1004.png"/>  
        <!-- iPad 竖屏 768 x 1004（标准分辨率） -->  
        <link rel="apple-touch-startup-image" sizes="1536x2008" href="/splash-screen-1536x2008.png"/>  
        <!-- iPad 竖屏 1536x2008（Retina） -->  
        <link rel="apple-touch-startup-image" sizes="1024x748" href="/Default-Portrait-1024x748.png"/>  
        <!-- iPad 横屏 1024x748（标准分辨率） -->  
        <link rel="apple-touch-startup-image" sizes="2048x1496" href="/splash-screen-2048x1496.png"/>  
        <!-- iPad 横屏 2048x1496（Retina） -->  
       
        <link rel="apple-touch-startup-image" href="/splash-screen-320x480.png"/>  
        <!-- iPhone/iPod Touch 竖屏 320x480 (标准分辨率) -->  
        <link rel="apple-touch-startup-image" sizes="640x960" href="/splash-screen-640x960.png"/>  
        <!-- iPhone/iPod Touch 竖屏 640x960 (Retina) -->  
        <link rel="apple-touch-startup-image" sizes="640x1136" href="/splash-screen-640x1136.png"/>  
        <!-- iPhone 5/iPod Touch 5 竖屏 640x1136 (Retina) -->  
    <!-- iOS 启动画面 end -->  

    或者以下代码，具体没有实践，还需考证

    <!!-- iPhone SPLASHSCREEN-->  
	<!link href="http://wlog.cn/html/"apple-touch-startup-image-320x460.png" media="(device-width: 320px)" rel="apple-touch-startup-image" />  
	<!!-- iPhone (Retina) SPLASHSCREEN-->  
	<!link href="apple-touch-startup-image-640x920.png" media="(device-width: 320px) and (-webkit-device-pixel-ratio: 2)" rel="apple-touch-startup-image" />  
	<!!-- iPad (portrait) SPLASHSCREEN-->  
	<!link href="apple-touch-startup-image-768x1004.png" media="(device-width: 768px) and (orientation: portrait)" rel="apple-touch-startup-image" />  
	<!!-- iPad (landscape) SPLASHSCREEN-->  
	<!link href="apple-touch-startup-image-748x1024.png" media="(device-width: 768px) and (orientation: landscape)" rel="apple-touch-startup-image" />  
	<!!-- iPad (Retina, portrait) SPLASHSCREEN-->  
	<!link href="apple-touch-startup-image-1536x2008.png" media="(device-width: 1536px) and (orientation: portrait) and (-webkit-device-pixel-ratio: 2)" rel="apple-touch-startup-image" />  
	<!!-- iPad (Retina, landscape) SPLASHSCREEN-->  
	<link href="apple-touch-startup-image-1496x2048.png"media="(device-width: 1536px)  and (orientation: landscape) and (-webkit-device-pixel-ratio: 2)"rel="apple-touch-startup-image" /> 


PS:再来补充一些

 1 <meta http-equiv="refresh" content="5">

 这个标签可以实现页面每5秒刷新一下

 2 <meta http-equiv="refresh" content="5 ; url='http://baidu.com'">

 让页面5秒后跳转到百度


 后面这两个参考 http://www.zhangxinxu.com/wordpress/2015/03/meta-http-equiv-refresh-content/ 有兴趣大家可以看看。






































