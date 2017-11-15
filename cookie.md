cookie是一种浏览器存储数据的方式
1. 读取
document.cookie,是一个由 分号空格 分隔的由等号连接的键值对字符串,一旦给cookie赋值,那么在浏览器关闭之前,该页面都会存储cookie数据,刷新不会丢失cookie,cookie在同一目录下的文件可以共享,**在同一目录下的不同文件夹下不可以共享**,不可以跨域,cookie会随着浏览器发送请求的时候自动发送给服务器,比较消耗性能
cookie默认是页面关闭的时候消失,但是也可以人为地设置过期时间,这样就可以改变cookie的生命周期了,有两个属性可以设置cookie的生命周期,如下

	document.cookie='key2=value2; expires= '+new Date('2017-11-8');//过期日期
      document.cookie='key3=value3; max-age='+7*24*60*60;//最长寿命,秒 ,保存七天
cookie允许共享主机,domain属性可以配置顶级域名,那么顶级域名下的子域名也可以共享其cookie



localStorage,sessionStorage以及cookie

- sessionStorage和localStorage都是用来存储客户端临时信息的对象
-  他们均只能存储字符串类型的对象
- localStorage的生命周期是永久,这意味着除非用户显示在浏览器提供的UI上清除localStorage信息,否则这些信息,否则这些信息将永远存在
- sessionStorage的生命周期为当前窗口或者标签页,一旦窗口或者标签被永久关闭,那么通过sessionStorage存储的数据就会丢失
- 不同的浏览器无法共享 sessionStorage和localStorage中的信息,相同浏览器的不同页面可以共享相同的localStorage,但是不同页面或标签间无法共享sessionStorag,但是一个标签页中包含多个iframe标签并且他们属于同源页面,那么也可以共享sessionStorag

###跨域
凡是在调用本地服务器的
反向代理
配置 apache 服务器来实现 url 映射解决 跨域问题( 反向代理功能 )
凡是在调用本地服务器数据的时候, 通过地址映射, 直接访问的就是远程服务器的数据,这样的功能就是反向代理.

		配置步骤:
		1> 找到 httpd.conf 文件
		2> 找到里面的 Proxy_modules 模块与 Proxy_http_module 模块, 将其注释去掉
		3> 找到要配置的虚拟主机
		4> 在里面添加两段代码
			ProxyRequests Off
			ProxyPass /api http://api.botue.com

