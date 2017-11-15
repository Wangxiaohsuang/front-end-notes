###栅格系统
bootstrap中采用`栅格系统`实现响应式布局
栅格系统可以设置元素占据容器的12等分的几等分

bootstrap中的容器

container容器的宽度:

- 100%      (<768px)   xs
- 950       786-992   sm
- 992-1200   950      md
- >1200     1170     lg

container-fluid(100%)

	<div class="container">
		<div class="row">
			<div class='col-xs-12 col-sm-6 col-md-4 col-lg-2'></div>
		</div>
	</div>
###less环境安装
首先安装好node和npm
1在线安装
复制less的npm里面的文件到
c>>-administrator>>-appData>>-roaming>>-npm中,在cmd里面输入lessc -v检测less是否安装成功
离线安装
cmd命令行   npm install -g less

###将less编译成css文件
首先要找到less文件所在的目录下,从命令行进入
用命令行工具执行 lessc demo.less demo.css
###常见的命令行命令
1. cd\  '返回到根目录 
2. cd..  '返回到上一级目录
3. cd 显示当前目录名或改变当前目录。
4. dir 显示目录中的文件和子目录列表。
5. md 创建目录。 
6. del 删除一或数个文件。
7. 盘符跳转直接输入C:回车即可

###后台管理系统
h+ 后台主题框架
icheck 可以改变表单的样式,单选,多选按钮的样式改变
微信支付,支付宝支付,银联,以及百度地图,都需要调接口
###11国庆作业
弹窗的高度要写死,超出部分用滚动条,设置overflow:auto;
###jq中width()方法
1. width() content 
2. innerWidth() content+padding
3. outerWidth() content+padding+border
4. outerWidth(true) content+paddding+border+margin
 
在html中通过data自定义的属性如data-index-value,在js中通过obj.dataset.在jq中使用obj.data('indexValue')方法获取


###微金所响应式开发项目总结
1. `伪元素after,before如果宽高要设置百分比.那么父元素必须要有具体的宽高值,不能是子元素撑出来的宽高`
2. 栅格系统里面的col是浮动并且相对定位的
3. iscroll插件的使用注意点:首先结构要符合要求,ul外围要包含一层盒子,不需要自己在样式里给ul设置定位,插件已经集成了,但是需要用js给ul设置宽度,ul的父盒子要设置overflow:hidden,,默认的滑动方向是垂直,如果要水平滑动的话需要设置参数
     var myScroll = new IScroll('.tabs_parent',{
    /*设置水平滑动，不允许垂直滑动*/
    scrollX: true, scrollY: false
    });
4. bootstrap的定制
###rem
###APIcloud开发App流程
1. 网上创建应用
2. 然后按照流程 端设置 代码 添加模块 编译
3. 在APIcloud里面把自己创建的远程应用的代码拉到本地(SVN)
4. 

