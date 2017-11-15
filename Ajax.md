#ajax
八字概括:异步请求,局部刷新
##get请求
```
	<!doctype html>
	<html lang="en">
	<head>
		<meta charset="UTF-8">
		<title>Document</title>
		<script type="text/javascript">
			window.onload = function () {
				var btn= document.querySelector('#btn');
				btn.onclick = function () {
					var user = document.querySelector('#username').value;
					var ps = document.querySelector('#psw').value;
					var xhr = null;
					if(window.XMLHttpRequest) {
						xhr = new XMLHttpRequest(); 
					}else {
						xhr = new ActiveXObject('Microsoft.XMLHTTP');//兼容ie6
					}
					var param = 'user='+user+'&ps='+ps;

					//open接收三个参数,第三个参数true:异步,false:同步,省略默认为true

					//get请求不可以省略问号
					xhr.open('get','./get.php?'+param);
					xhr.send(null);//get请求send里面的参数是null
					xhr.onreadystatechange = function () {
						if(xhr.readyState==4) {
							if(xhr.status==200) {
								alert(xhr.responseText);
							}
						}
					}
	
				}
			};
		</script>
	</head>
	<body>
		<form>
			用户名<input type="text" name="username" id="username"> <span id="info"></span><br>
			密码<input type="password" name="psw" id="psw"> <br>
			<input type="button" name="" value="登录" id="btn">
		</form>
	</body>
	</html>
请求的php文件get.php	
	<?php 
	
	$user = $_GET['user'];
	$ps = $_GET['ps'];
	if($user =='admini'&&$ps=='1234') {
		echo '登录成功';
	}else {
		echo 'error';
	}
	
	 ?>
```

##post请求

```
	<!doctype html>
	<html lang="en">
	<head>
		<meta charset="UTF-8">
		<title>Document</title>
		<script type="text/javascript">
			window.onload = function () {
				var btn = document.querySelector('#btn');
				var username = document.querySelector('#username');
				var ps = document.querySelector('#ps');
				var info = document.querySelector('#info');
				btn.onclick = function () {
					if(!username.classList.contains('right')) {
						alert('请填写正确的用户名');
						return ;
					}
					var xhr = null;
					if(window.XMLHttpRequest) {
						xhr = new XMLHttpRequest();
					}else {
						xhr = new ActiveXObject('Microsoft.XMLHTTP');
					}
					xhr.open('post','./4.php',true);
					var param = 'username='+username.value+'&ps='+this.value;
					xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded');
					xhr.send(param);
	
				}
				username.onblur = function () {
					var xhr = null;
					if(window.XMLHttpRequest) {
						xhr = new XMLHttpRequest();
					}else {
						xhr = new ActiveXObject('Microsoft');
					}
					var param ='username='+this.value;
					var user = this.value;
					xhr.open('post','./4.php',true);
						//一定要设置请求头
					xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded');
					xhr.send(param);
					xhr.onreadystatechange = function () {
						if(xhr.readyState==4) {
							if(xhr.status==200) {
								var data = xhr.responseText;
								if(data==1) {
									info.innerHTML = '用户名正确';
									username.classList.add('right');
								}
								else {
									info.innerHTML = '用户名错误';
									username.classList.remove('right');
								}
	
							}
						}
					}
	
	
				}
			}
		</script>
	</head>
	<body>
	<form>
		用户名<input type="text" id="username"> <span id="info"></span> <br>
		密码<input type="password" id="ps"> <br>
		<input type="button" name="" id="btn" value="提交">
	</form>
		
	</body>
	</html>
```
请求的同目录下的4.php文件
```

	<?php 
	$username = $_POST['username'];
	$ps = 
	$arr = array('jorden'=>'123','messe'=>'1234','kobe'=>'12345');
	$flag = false;
	foreach ($arr as $key => $value) {
		if($username==$key) {
			echo '1';
			$flag = true;
		}
	}
	if(!$flag) {
		echo '0';
	}	
	 ?>
```

###json
是一种数据格式
形式和对象类似,但是键值必须要用双引号包起来,键值是字符串的也需要用双引号包起来,里面的数据要求必须是常量

	var str =' {"name":"张三","hobby":["code","sing","dance"]}';
	var obj = JSON.parse(str);//将json形式的字符串解析
	var str = JSON.stringify(obj);// JSON.parse的逆运算
##跨域
ajax不可以跨域
同源:协议,端口和域名都相同即为同源,但是可以通过jsonp跨域,jsonp跨域的原理就是利用script标签的src请求资源不受跨域的影响,动态创建script标签,通过服务端返回调用函数,从而实现在客户端调用
以下是方法的封装
```
	function ajax(obj) {
	var defaults = {
		type:'get',
		url:'#',
		//data:{},
		dataType:'jsonp',//jquery内部默认是文本
		jsonp:'callback',
		//jsonpCallback:
		success:function (data) {
			console.log(data);
		}
	};
	for(var key in obj) {
		defaults[key]=obj[key];
	}
	//默认的回调函数的名称
	var cbName = 'jquery'+('11.1.1.0'+Math.random()).replace(/\D/g,'')+(new Date().getTime());
	if(defaults.jsonpCallback) {
		cbName = defaults.jsonpCallback;
	}
	//函数需要加在全局环境中
	window[cbName] = function (data) {
		defaults.success(data);
	};
	var param = '';
	if(defaults.data) {
		for(var attr in defaults.data) {
			param += '&'+attr+'='+defaults.data[attr];
		}	
	}
	var script = document.createElement('script');
	var url =  defaults.url+'?'+defaults.jsonp+'='+cbName+param;
	script.src=url;
	var head = document.getElementsByTagName('head');
	header.appendChild(script);
	}
```

##模仿jquery封装ajax方法和jsonp方法

```	
	function ajax(obj){
    var defaults = {
        type : 'get',
        async : true,
        url : '#',
        dataType : 'text',
        jsonp : 'callback',
        data : {},
        success:function(data){console.log(data);}
    };

    for(var key in obj){
        defaults[key] = obj[key];
    }

    if(defaults.dataType == 'jsonp'){
        ajax4Jsonp(defaults);
    }else{
        ajax4Json(defaults);
    }
	}

	function ajax4Json(defaults){
    // 1、创建XMLHttpRequest对象
    var xhr = null;
    if(window.XMLHttpRequest){
        xhr = new XMLHttpRequest();
    }else{
        xhr = new ActiveXObject('Microsoft.XMLHTTP');
    }
    // 把对象形式的参数转化为字符串形式的参数
    /*
    {username:'zhangsan','password':123}
    转换为
    username=zhangsan&password=123
    */
    var param = '';
    for(var attr in defaults.data){
        param += attr + '=' + defaults.data[attr] + '&';
    }
    if(param){
        param = param.substring(0,param.length - 1);
    }
    // 处理get请求参数并且处理中文乱码问题
    if(defaults.type == 'get'){
        defaults.url += '?' + encodeURI(param);
    }
    // 2、准备发送（设置发送的参数）
    xhr.open(defaults.type,defaults.url,defaults.async);
    // 处理post请求参数并且设置请求头信息（必须设置）
    var data = null;
    if(defaults.type == 'post'){
        data = param;
        xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded");
    }
    // 3、执行发送动作
    xhr.send(data);
    // 处理同步请求，不会调用回调函数
    if(!defaults.async){
        if(defaults.dataType == 'json'){
            return JSON.parse(xhr.responseText);
        }else{
            return xhr.responseText;
        }
    }
    // 4、指定回调函数（处理服务器响应数据）
    xhr.onreadystatechange = function(){
        if(xhr.readyState == 4){
            if(xhr.status == 200){
                var data = xhr.responseText;
                if(defaults.dataType == 'json'){
                    // data = eval("("+ data +")");
                    data = JSON.parse(data);
                }
                defaults.success(data);
            }
        }
    }
	}
	function ajax4Jsonp(defaults){
    // 这里是默认的回调函数名称
    // expando: "jQuery" + ( version + Math.random() ).replace( /\D/g, "" ),
    var cbName = 'jQuery' + ('1.11.1' + Math.random()).replace(/\D/g,"") + '_' + (new Date().getTime());
    if(defaults.jsonpCallback){
        cbName = defaults.jsonpCallback;
    }

    // 这里就是回调函数，调用方式：服务器响应内容来调用
    // 向window对象中添加了一个方法，方法名称是变量cbName的值
    window[cbName] = function(data){
        defaults.success(data);//这里success的data是实参
    };

    var param = '';
    for(var attr in defaults.data){
        param += attr + '=' + defaults.data[attr] + '&';
    }
    if(param){
        param = param.substring(0,param.length-1);
        param = '&' + param;
    }
    var script = document.createElement('script');
    script.src = defaults.url + '?' + defaults.jsonp + '=' + cbName + param;
    var head = document.getElementsByTagName('head')[0];
    head.appendChild(script);
	}
```