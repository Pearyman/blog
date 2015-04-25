<h1>关于@font-face属性</h1>
因为最近的设计师总是喜欢用微软雅黑的字体，而浏览器中默认的是宋体。但是我们有的时候并不想总是用到font-family属性。
所以，我觉得有必要看看@font-face属性。
说道，@font-face ,我不得不提到webFont。这是在css3中新增的属性。首先，我们可以使用@font-face属性来利用服务器端的字体。
具体格式为：
	@font-face{

	fontfamily:WebFont;

	src:url(‘font/Fontin_Sans_R_45b.otf’) format(“opentype”);

	font-weight:normal;

	}

在上面的代码中，使用font-family属性中的”webFont”来声明服务端的字体。

在SRC属性值中，指定服务器的指定路径。

再举个例子，假如在http://www.liyanan.net/promation/fontinsans.html中存在我们使用的字体。那我们应该这样获取它

 

	<style type=”text/css”>

		@font-face{

		fontfamily:WebFont;

		src:url(‘font/Fontin_Sans_R_45b.otf’) format(“opentype”);

		font-weight:normal;

		}

	</style>

	 

	<body>

		<address>

		this page uses the

		<a href=”http://www.liyanan.net/promation/fontinsans.html”></a>

		</address>

	</body>

同样，使用@font-face同样可以获取本地的字体。

大家只需要将路径中的url()修改文local（）即可。

	@font-face{

		font-family:Arial;

		src:local(‘Arial’);

	}
同时，@font-face属性显示客户端本地的好处是可以先显示本地客户端的字体，同时，如果我们我们加上SRC()这样，当客户端字体找不到的时候，我们就可以去找服务器端的字体。
兼容性方面

微软的IE 5已经是开始支持这个属性，但是只支持微软自有的.eot (Embedded Open Type) 格式，而其他浏览器直到现在都没有支持这一字体格式。
然而，从Safari 3.1开始，网页重构工程师已经可以设置.ttf(TrueType)和.otf(OpenType)两种字体做为自定义字体了。

另外，本地的字体文件大小为90K-120K。但可以压缩。

下面说说性能发面：

  我的建议是除非它对于页面是非常重要的，否则不要使用@font-face。
最主要的原因是由于如果@font-face声明之前有script标签的话，字体文件的下载将阻滞整个页面的加载。样式表同样也有这样的阻滞问题。但是样式表是对于整张页面提供样式的，而字体文件仅仅加入了一个自定义的字体。
如果你仍然要使用@font-face，我建议在页面全部加载完毕后再下载字体文件， 这将解决IE中的问题——整张页面渲染之后，字体才会再后台下载，并在下载完成后增强我们的样式效果。
这个技巧在其他浏览器中也同样有好处。使用后加载，大部分的浏览器将都不会出现浏览器忙的标识。

  在别人的文章中提到了预读取字体文件，不过需要注意的是这个技术并不适合IE。我认为IE将是最难解决的问题，我同时希望能够将样式表、脚本文件和图片的优先级提高。
这取决于页面以及字体文件的使用。
我不建议在样式表中使用 data:URIs  来定义字体文件。由于样式表可能包含了EOT和TTF两种格式的数据，这可能会让下载的数据加倍。这同样也会另样式表的加载时间增长，而在大部分浏览器中样式表会阻断页面加载。

几点建议：

1,只在你确定你非常需要 @font-face的时候才使用它 <br/>
2,将你的@font-face定义在所有的SCRIPT标签前 <br/>
3,如果你有许多字体文件，考虑将它们分散到几个域名下。<br/>
4,不要包含没有使用的 @font-face声明——IE将不分它使用与否，通通加载<br/>
5,Gzip字体文件，同时给它们一个未来的过期头部声明<br/>
6,考虑字体文件的后加载，起码对于IE。

这个经过我的实验，确实得到了很多的启发，并且这种方法在移动端上确实很适用。

具体的代码在这里 https://github.com/Pearyman/jscode/blob/master/test/font-face.html
 