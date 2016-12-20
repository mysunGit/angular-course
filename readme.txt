1、angular是什么
2、优势
	依赖注入
	双向数据绑定
	测试
	控制器
	指令
	过滤器
	。。。。
3、入门案例
 	1）在需要的地方添加指令ng-app，
 		标识的就是程序的一个入口，在它所包含的内部，如果符合angular的语法，那么就按照angular的语法解析
 		必不可少-------语法导致
 		也是唯一的------一个程序只有一个入口
 	2)不同的数据类型的展示
 	            基本的数据类型
 		引用类型
4、MVC思想
	M---model----数据-----module---模型
	V---view-----视图
	C---controller---连接视图和数据的
	
	写法：
		html节点添加ng-app="myApp"
		在js中
			var app = angular.module("myApp",[]);//和html ng-app = "myApp"一一对应，[] 指代的意思是我们后期需要注入的各个模块
		在body上添加了一个ng-controller="myCtrl"
		在js中
		    app.controller("myCtrl",function($scope){
//		    	$scope其实相当于我们的this,但是不能替换，我们变量、对象挂载到$scope上
		    	$scope.userName="zz1611";
		    })
		html中
			{{userName}}
		运行即可显示
		
		问题：1、一个页面只能有一个入口？------是的
			2、一个页面可以有多个控制器吗？-----是的
				结合js中的作用域的概念去理解
5、ng-src
	一般图片展示
	$scope.src = "img/banner1.jpg"
	
	<img ng-src="{{src}}"/>
	
	src
		因为进行了两步操作：
		1.表达式直译，没做网络请求；
		2.再进行网络请求，然后显示图片；
		
		利用ng-src解决此问题
6、MVVM
	数据双向绑定
	输入框、select、textarea结合
	<input ng-model="userName"/>
	{{userName}}
	$scope.userName = "zz1611"
	
	数据驱动视图更新
7、ng-repeat
	循环
	user可以随便写，表示的是users一个对象，也就是数组当中每一个对象的实例  in  users不能更改
	<ul>
		<li ng-repeat="user in users">{{user.name}}</li>
	</ul>
	$scope.users=[{
		name:"wxx"
	},
	{
		name:"wxx01"
	}]
	

	循环的嵌套
		我们将每一个对象的中的一个属性作为其中另一个循环的原始数据model
		ng-repeat = "city in provice.cities"
		
		{{city.name}}
8、引入bootstrap进行结合使用
	bootstrap.css
	jquery.js
	bootstrap.min.js
	angular.js
9、ng-click
	angular中点击事件
	ng-click="addLikeNum(user)"
	
	$scope.addLikeNum = function(user){
		user.likeNum++;
	}
	
	此时更改的就是$scope.users里面的点击的那个数据，所以说数据改变了，视图我们也发生了改变

	如果我们要储存到本地，
	我们存储的可以死$scope.users
	localStrage.setItem("users",$scope.users);//注意格式转换
	
	取数据
	if(loacalStorage.getItem("users")){
		$scope.users = loacalStorage.getItem("users");
	}else{
		//ajax
		
		sucess:function(data){
			$scope.users = data
		}
	}
10、过滤器 filters

	过滤器可以写在表达式或者指令中
	1）、基本的过滤器 -----表达式
		uppercase：大写
		lowercase：小写
		currency:货币       {{ price | currency : "￥" }}
		date: 日期   {{ date | date : "yyyy-MM-dd"}}
		number：数值 {{salary|number:2}}-----保留两位有效数字
		。。。
	2）、limitTo:2 ---- 指令
		显示2条数据
		MVVM  select 结合 ----每页显示的条数----ng-model="selectNum"
		
		<tr ng-repeat="user in users | limitTo : selectNum"></tr>
