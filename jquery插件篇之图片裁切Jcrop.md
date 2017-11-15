# 1图片裁切插件Jcrop
官网地址[jcrop](http://jcrop.org),如果想深入学习就去看官方文档,这里只简单介绍常用的用法

1. 首先在页面引入jquery.js和jcrop.js
2. 找到需要裁切的img的id,实例化一个Jcrop对象`$('#img-id).Jcrop(options,callback)`
3. options是一个对象,里面传入配置参数,常见的有如下
 - aspectRatio:裁切的宽高比
 - minSize:设置裁切的最小尺寸,是一个数组,[w,h]
 - onChange事件,裁切区域有宽高或者位置的变化的时候连续触发
 - onSelect事件,选中裁切区域后触发,不连续
 
理论说了这么多,估计还是一脸懵逼,那就举个例子吧

html部分

```	
	<div class="pic">
	    <div class="bigPic">
	        <img id="srcPic" src="img/1.jpg" alt="">
	    </div>
	    <div class="preview">
	        <!--<img src="img/2.jpg" alt="">-->
	    </div>
	</div>
	<div>
	    <form action="">
	        <input type="hidden" name="cs_id" value="4">
	        <input type="hidden" id="x" name='x'>
	        <input type="hidden" id="y" name='y'>
	        <input type="hidden" id="w" name='w'>
	        <input type="hidden" id="h" name='h'>
	        <p><input id="submitBtn" type="submit" value="提交"></p>
	    </form>
	</div>
```

js部分
```

<script src="Jcrop-WIP-2.x/js/jquery.min.js"></script>
<script src="Jcrop-WIP-2.x/js/Jcrop.js"></script>
<script>
    $('#srcPic').Jcrop({
        aspectRatio:1,//裁切的宽高比
        onChange:showCoords,//改变坐标的时候连续触发
        onSelect:showCoords,//选中结束后触发
        minSize:[200,200] //允许裁切的最小尺寸
    },function() {
        var jcrop_api = this;
        //设置预览裁切框内图片的容器,源码生成一个class名为预览是在图片的下面,
        jcrop_api.initComponent('Thumbnailer', {
            width: 200,
            height: 200
        });
    });
    function showCoords(obj) {
        //obj是事件对象,也就是裁切对象
        $("#x").val(obj.x);
        $("#y").val(obj.y);
        $("#w").val(obj.w);
        $("#h").val(obj.h);
    }
    
</script>

```
