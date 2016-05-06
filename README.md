# js模板引擎：doT.js
doT上手比较容易，但之前熟悉了mustache，改用doT时有点不习惯，但用两次就好了。

下载doT.js（里面有个doU.js不要用，doU.js是为了测试遗留问题的）。举个简单的使用例子:

##HTML部分：
		<script id="j-tmpl" type="text/template">
		{{ if(it.success){ }}
		        <h2>results:</h2>
		        <ul>
		                {{ for (var i = 0, l = it.data.length; i < l; i++) { }}
		                        <li>
		                                <h5>{{=it.data[i].title}}</h5>
		                                <p>{{!it.data[i].message}}</p>
		                        </li>
		                {{ } }}
		        <ul>
		{{ }else{ }}
		        <h2>暂无数据</h2>
		{{ } }}
		</script>
##JS部分：
		<script>
		var obj = {
		        success: true,
		        data:[
		                {title:'item1',message:11},
		                {title:'item1',message:22}
		        ]
		}
		var tmpl = document.getElementById('j-tmpl').innerHTML;
		var doTtmpl = doT.template(tmpl);
		console.log(doTtmpl(obj ));
		</script>

看了例子，就应该会使用了。
{{=it.xx}} 取obj.xx的值
{{ }} 里面放if els / for 等表达式
{{!it.xx}} 取把obj.xx转义后的值
这些基本够用了，还有复杂的应用，可以看doT主页内的examples、docs。
并且，可以很容易把doT写成jquery插件：
		<script>
		$.extend({
		tmpl: function(template, data){
		        return doT.template(template).apply(null,[data]);
		}
		});
		</script>
