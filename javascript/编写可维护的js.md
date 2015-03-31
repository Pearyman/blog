<h1>编写可维护的js</h1>
变量·函数·运算符

变量
首先，我们先来看一个极其简单的例子

	<textarea>
	function doSomething(){
		var result=10+value;
		var value=10;
		return result;
	} // NAN
	</textarea>


var的副作用
隐式全局变量和明确定义的全局变量间有些小的差异，就是通过delete操作符让变量未定义的能力。
1,通过var创建的全局变量（任何函数之外的程序中创建）是不能被删除的。
2,无var创建的隐式全局变量（无视是否在函数中创建）是能被删除的。
这表明，在技术上，隐式全局变量并不是真正的全局变量，但它们是全局对象的属性。属性是可以通过delete操作符删除的，而变量是不能的.
个人建议使用单var格式
1, 提供了一个单一的地方去寻找功能所需要的所有局部变量
2, 防止变量在定义之前使用的逻辑错误
3, 帮助你记住声明的全局变量，因此较少了全局变量
4, 少代码（类型啊传值啊单线完成）
举个例子
	function doSomethingWithItems(items){
		var value=10,
		result=value+10,
		i,
		len;
		for(i=0,len=items.length; i++) {
			doSomething(item);
		}
	}

函数
大家都知道Javascript 有两个种定义Function的方法非常常用。例如
		function a(){
			alert("a");
		}
		var a = function(){
			alert("a")
		}
虽然两个种方式定义出来的 function 调用的时候结果一样，但是中间还是有区别的。
举个简单的例子，假如我们要重定义 a() ，而且新的方法要继承 a() 里面所有方法并且进行其他扩展的话。
就可以明显看到这两个方式的区别了。
1. 首先，我们先建立一个临时的变量来存储 a()
		var b = a;
		然后，重新定义a()
		第一种方式:
	function a(){
		b();
		alert("ok");
	}
		第二种方式:
	a = function(){
		b();
		alert("ok");
	}
这是大家可以尝试发现。第一种方式重新定义的 a() 会出现堆栈溢出的错误。
而第二种方式却成功保留了原来 a() 所执行的脚本，成功 alert 出了 "a" "ok" 的字样，说明 a() 的方法被重定义了。
这里就可以很明显区分两个方式的区别了。定义的顺序不同。
第一种，刚开始其实没有重新定义 a 这个function 而在里面执行了其本身。
第二种方式， a = function () 这里没有执行到 function 里面的代码 a 已经被重新定义了。所以这里的重定义是有效的
位运算符
JS和javascript有着相同的一套位运算符
在java中，位运算符处理的是整数。但是在JS中没有整数类型，只有双精度浮点数。因此我们需要把数字运算数先转换成整数，然后再进行运算。然后再转换过去。
在大多数语言中，位运算符接近于硬件处理，所以处理的速度非常快。
而在JS中，JS的执行环境接触不到硬件，所以非常慢。并且JS很少被用来执行位操作。
特别注意的是，在JS中，& “与”运算符常常被写成“&&”。位运算符出现在JS中降低了这门语言的冗余度，越来越不好找到BUG
将数据从代码中分离出来配置数据是应用中写死的值
		function validate(value){
			if(!value) {
				alert("invalid value");
				location.href="/errors/invalid.php"
			}
		}
		function toggle(element){
			if(hasClass(element,"selected")){
				removeClass(element,"selected");
			}else {
				addClass(element,"selected");
			}
		}
抽离配置数据将数据从代码中抽离出来的第一步是将配置数据拿到外部
也就是说
		var config={
			MSG_INVALID_VALUE:"incalid value",
			URL_INVALID:"/errors/invalid.php",
			CSS_SELECTED:"SELECTED"
		};
将配置文件抽离出来意味着任何人都可以修改他们，而不会导致应用逻辑上的错误。
UI层的松耦合在这里，值得我们注意的一点是：在一起工作的组件无法达到“无耦合”。在所有的系统中，组件之间总是要共享一些东西来完成各自的工作。而我们的目标是----确保一个组件的修改不会经常性的影响其它的部分。
将js从CSS中分离出来在IE8以及更早的版本中，css中有个属性让人爱少恨多。这就是css表达式。
比如：
	.box{
		width:expression(document.body.offsetWidth+"px");
	}
这段代码的意思是元素的宽度匹配浏览器的宽度。
在css中嵌入js这对于维护来说简直就是一件很棘手的事情。
幸好，IE9就不在支持css表达式了。
将css从JS中分离出来有的时候，保持css和js之间清晰地分离是很有挑战的。有时，我们通过脚本直接修改DOM元素的style属性。style属性是一个对象，包含了可以读取和修改的css属性。
比如，像这样
	element.style.color="red";
这样做对后续的调试非常的困难。因为通常我们找样式的问题通常找css，知道找了很长时间最后排除了所有的可能性，才会去js中来查找样式.
再举个例子
	element.style.cssText="color:red; left:10px; top:10px;"
那我们怎样解决这样的问题来降低耦合度呢？
	.p{color:red; top:10px; left:10px;"}
原生的这样添加：element.className+="p";
HTML5中这样添加：element.classList.add("p");
YUI中这样添加：Y.one(element).addClass("p");
JQ中是这样添加：$(element).addClass("p");
DOJO中这样添加：Dojo.addClass(element,"p");
将JS从html中分离举个例子
这是一种深耦合的表现
不好的地方有这么几点：
1,当按钮点击的时候，你的doSomething()函数必须存在
2,如果要是修改了doSomething()的函数名，那么就会出现错误
同样，解决耦合度，我们只需要在JS代码上绑定addEventListener（）事件就可以了
不是你的对象你不要动那什么是我们的对象呢？
首先，我要先说一下什么是我们的。当我们的代码创建了对象的时候，我们便拥有这些对象。所以维护这些代码也是我们的责任。
YUI拥有YUI对象
jquery有jq对象
但在这里值得注意的是，当有些对象不是我们创建的时候，我们不要修改他们
我们应该保持这几个原则：
1,不覆盖方法
document.getElementById()=function() {return null; }
2,不新增方法
YUI.doSomething=function () {//}
3,不删除方法
document.getElementById()=null;
更好地方法最受欢迎的对象扩充的形式为继承
文件的精简和压缩这个就很形象化了。哈哈
当我们完成了文件的构建，验证，合并和加工，这个时候，就是我们要把文件变小的时候了。
文件精简：文件精简是指消除不必要的空格，去除注释，并对文件做一些处理使其体积尽可能的小。
精简一个javascript文件并不复杂，但是如果精简的不当就会导致错误或者产生无效的语法。
推荐精简代码的工具
YUI Compressor

以上都是个人在读<编写可维护的js>这本书后的一些小的总结。
