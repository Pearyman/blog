<h1>SVG和animation配合使用（入门）</h1>

这个当然是废话少说，直接上步骤：

<h3>1，首先你要有个svg的图形</h3>

 <img src="../images/svg-shape.png"/>

<h3>2，这个svg的形状必须有个 stroke </h3>

 <img src="../images/svg-path.png"/>

<h3>3,这个线要能够设置成虚线</h3>

	  我们可以用Illustrator把它变成虚线，同样我们也能用css来实现。

	  在HTML中我们这样写：

	  <svg ...>

	  	<path class="path" stroke="#000" ...>

	  </svg>

	  css中这样写：

	  .path{stroke-dasharray:20}

	  这样 我们就得到了长度为20px的虚线。

 <img src="../images/dashed-shape.png"/>

 <h3>4,这些虚线的长度可以更长</h3>

 	css：

 	.path{stroke-dasharray:100;}

 <img src="../images/long-dashes.png"/>

 <h3>5,我们同样可以给它加上offset属性，真能够让这些虚线移动位置</h3>

   那我们用什么来移动他们的位置呢 正如我们用了animation这个属性

  <img src="../images/animate-stroke.gif"/>

	  .path {

		  stroke-dasharray: 100;

		  animation: dash 5s linear;
		}

		@keyframes dash {

		  to {

		    stroke-dashoffset: 1000;

		  }
		  
		}




























































