## iframe使用
* 通过src给ifame下的页面进行传值
> eg:index.html?ticker=userID&contentID=contentID
### iframe页面中接受参数的方法
```javascript
function GetJRequest() {
		var urlinfo = window.location.href; //获取当前页面的url
		var len = urlinfo.length; //获取url的长度
		var offset = urlinfo.indexOf("?"); //设置参数字符串开始的位置
		if(offset <= 0)
			return;
		var newsidinfo = urlinfo.substr(offset + 1, len) //取出参数字符串 这里会获得类似“id=1”这样的字符串
		var values = newsidinfo.split('&');
		len = values.length;
		var valHash = new Array();
		if(values.length > 0) {
			for(var i = 0; i < len; i++) {
				var keys = values[i].split('=');
				if(keys.length > 1) {

					valHash[keys[0]] = keys[1];
				}
			}
		}
		return valHash;
    }
    // 通过调用该方法 获得iframe中src路径传过来的参数的数组
```
### 父页面获取iframe页面的元素
```javascript
    window.onload=function(){
    var test = document.getElementById('iframe的id').contentWindow.document.getElementById('iframe里要获取的元素的id');
    console.log(test);
    test.style.height=0;
    }
```

