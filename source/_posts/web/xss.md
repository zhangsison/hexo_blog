---

title: XSS
date: 2019-12-06
categories: [web]
tags: [XSS]

---



## XSS




当浏览器请求 http://xxx/search?keyword="

```js

<!-- <script>alert('XSS');</script> 
时，服务端会解析出请求参数 keyword，得到 "
<!-- <script>alert('XSS');</script> 
```
 拼接到 HTML 中返回给浏览器。形成了如下的 HTML：

```js

<input type="text" value="" <script>alert('XSS');</script>"
<button~搜索</button>
<div>
您搜索的关键词是："<script>alert('XSS');</script>
</div>

<input type="text" value="<%= escapeHTML(getParameter("keyword")) %">
<button~搜索</button>
<div>
您搜索的关键词是：<%= escapeHTML(getParameter("keyword")) %>
</div>

```

**escapeHTML()**

```js
http://xxx/?redirect_to=javascript:alert('XSS')
// 禁止 URL 以 "javascript:" 开头
xss = getParameter("redirect_to").startsWith('javascript:');
if (!xss) {
	<a href="~%= escapeHTML(getParameter("redirect_to"))%~">
	跳转...
	</a>
} else {
	<a href="/404"~
	跳转...
	</a>
}

// 根据项目情况进行过滤，禁止掉 "javascript:" 链接、非法 scheme 等
allowSchemes = ["http", "https"];

valid = isValid(getParameter("redirect_to"), allowSchemes);

if (valid) {
	<a href="~%= escapeHTML(getParameter("redirect_to"))%>">
	跳转...
	</a>
} else {
	<a href="/404">
	跳转...
	</a>
}
```

 插入 JSON 的地方不能使用 escapeHTML()，因为转义 " 后，JSON 格式会被破坏。

```		
var initData = < escapeEmbedJSON(data.toJSON()) /
```
DOM 型 XSS 攻击，实际上就是网站前端 JavaScript 代码本身不够严谨，把不可信的数据当作代码执行了。

在使用 .innerHTML、.outerHTML、document.write() 时要特别小心，不要把不可信的数据作为 HTML 插到页面上，而应尽量使用 .textContent、.setAttribute() 等。

如果用 Vue/React 技术栈，并且不使用 v-html/dangerouslySetInnerHTML 功能，就在前端 render 阶段避免 innerHTML、outerHTML 的 XSS 隐患。

DOM 中的内联事件监听器，如 location、onclick、onerror、onload、onmouseover 等，~a~ 标签的 href 属性，JavaScript 的 eval()、setTimeout()、setInterval() 等，都能把字符串作为代码运行。如果不可信的数据拼接到字符串中传递给这些 API，很容易产生安全隐患，请务必避免。


> XSS攻击可以分为3类：反射型（非持久型）、存储型（持久型）、基于DOM。

**反射型**

反射型 XSS 只是简单地把用户输入的数据 “反射” 给浏览器，这种攻击方式往往需要攻击者诱使用户点击一个恶意链接，或者提交一个表单，或者进入一个恶意网站时，注入脚本进入被攻击者的网站。

看一个示例。我先准备一个如下的静态页：

![](https://user-images.githubusercontent.com/7871813/42720000-30a9b93a-8752-11e8-879b-edd8519f4e3e.png)

恶意链接的地址指向了 localhost:8001/?q=111&p=222。然后，我再启一个简单的 Node 服务处理恶意链接的请求：
```
const http = require('http');
function handleReequest(req, res) {
res.setHeader('Access-Control-Allow-Origin', '*');
res.writeHead(200, {'Content-Type': 'text/html; charset=UTF-8'});
res.write('<script>alert("反射型 XSS 攻击")</script>');
res.end();
}

const server = new http.Server();
server.listen(8001, '127.0.0.1');
server.on('request', handleReequest);
```
当用户点击恶意链接时，页面跳转到攻击者预先准备的页面，会发现在攻击者的页面执行了 js 脚本：
```
    http://weibo.com/login.php?'u=1931138954'<script>alert(/ssss/)</script>
```

使用标签iframe.
```
		http://weibo.com/login.php?'u=1931138954'<iframe src='http://www.baidu.com'/>
```
**存储型**

存储型 XSS 会把用户输入的数据 "存储" 在服务器端，当浏览器请求数据时，脚本从服务器上传回并执行。这种 XSS 攻击具有很强的稳定性。
```
	<input type="text" id="input">
	<button id="btn">Submit</button>
		<script>
		    const input = document.getElementById('input');
		    const btn = document.getElementById('btn');
		
		    let val;
		     
		    input.addEventListener('change', (e) => {
		        val = e.target.value;
		    }, false);
		
		    btn.addEventListener('click', (e) => {
		        fetch('http://localhost:8001/save', {
		            method: 'POST',
		            body: val
		        });
		    }, false);
		</script>     
	
	启动一个 Node 服务监听 save 请求。为了简化，用一个变量来保存用户的输入：
	
	const http = require('http');
	
	let userInput = '';
	
	function handleReequest(req, res) {
	    const method = req.method;
	    res.setHeader('Access-Control-Allow-Origin', '*');
	    res.setHeader('Access-Control-Allow-Headers', 'Content-Type')
	    
	    if (method === 'POST' && req.url === '/save') {
	        let body = '';
	        req.on('data', chunk => {
	            body += chunk;
	        });
	
	        req.on('end', () => {
	            if (body) {
	                userInput = body;
	            }
	            res.end();
	        });
	    } else {
	        res.writeHead(200, {'Content-Type': 'text/html; charset=UTF-8'});
	        res.write(userInput);
	        res.end();
	    }
	}
	
	const server = new http.Server();
	server.listen(8001, '127.0.0.1');
	
	server.on('request', handleReequest);
```
![](https://user-images.githubusercontent.com/7871813/42720476-eb71a5c8-8759-11e8-8763-eb08b3480201.gif)

**基于DOM**

基于 DOM 的 XSS 攻击是指通过恶意脚本修改页面的 DOM 结构，是纯粹发生在客户端的攻击。

看如下代码：
```	
		<input type="text" id="input">
		<button id="btn">Submit</button>
		<div id="div"></div>
	
	    const input = document.getElementById('input');
	    const btn = document.getElementById('btn');
	    const div = document.getElementById('div');
	
	    let val;
	     
	    input.addEventListener('change', (e) => {
	        val = e.target.value;
	    }, false);
	
	    btn.addEventListener('click', () => {
	        div.innerHTML = `<a href=${val}>testLink</a>`
	    }, false);

```
点击 Submit 按钮后，会在当前页面插入一个链接，其地址为用户的输入内容。如果用户在输入时构造了如下内容：
```
    '' onclick=alert(/xss/)
```
用户提交之后，页面代码就变成了：
```
    <a href onlick="alert(/xss/)">testLink</a>
```
## XSS 攻击的防范 ##

**输入检查**
用于对用户输入所包含的特殊字符或标签进行编码或过滤，如 <，>，script，防止 XSS 攻击
```
	// vuejs 中的 decodingMap
	// 在 vuejs 中，如果输入带 script 标签的内容，会直接过滤掉
	const decodingMap = {
	  '&lt;': '<',
	  '&gt;': '>',
	  '&quot;': '"',
	  '&amp;': '&',
	  '&#10;': '\n'
	}
```
## CSRF ##
CSRF 攻击是攻击者借助受害者的 Cookie 骗取服务器的信任


- 会话状态管理（如用户登录状态、购物车、游戏分数或其它需要记录的信息）

- 个性化设置（如用户自定义设置、主题等）

- 个性化设置（如用户自定义设置、主题等）


通过 Cookie 进行 CSRF 攻击

假设有一个 bbs 站点：http://www.c.com，当登录后的用户发起如下 GET 请求时，会删除 ID 指定的帖子：

	http://www.c.com:8002/content/delete/:id

**CSRF 攻击的防范**

CSRF (Cross—Site Request Forgery)，既跨站点请求伪造，也被叫做 XSRF，和 XSS 一样也是一种比较常见的 web 攻击。CSRF攻击者会过过构造的第三方页面诱导受害者完成加载或者点击，利用受害者的权限，以其身份向合法网站发起恶意请求，通常用户发生状态改变的请求，比如虚拟货币的转账，账号信息修改，恶意发邮件等等，由于具有一定的隐蔽性，所以比较防范。

 我们通过一个简单例子来演示 CSRF的攻击原理，如上图所示（TODO需要重做），正常网站A，攻击网站B，用户C，正常网站具有一个虚拟币转账的公功能，转账通过GET请求完成，且网站A不具备 CSRF 防范机制，攻击者利用这个漏洞恶意构造网站B，诱导用户C访问，达到恶意转账目的。

转账的GET请求如下：
```
	GET http://normal-site.com/transfer.do?from=rommel&to=alice&amount=100 HTTP/1.1
```
这是我们出于演示方便使用GET请求来完成转账，实际应用远比这个列子要复杂，需要更加安全的机制，比如一次性 token，https 等，而且一般都是用POST请求。
​

CSRF 的攻击过程过程图上图所示：

CSRF 攻击有一个前提条件，是用户具有某个正常访问的访问权限。一般网站的访问断线都具备一定的有效期，比如1天过期，或者几个小时骨气，再次期间权限信息会保留在用户浏览器的cookie中，这本例子中假设用户C刚刚登录了网站A，全新还没有过期。

攻击者利用正常网站A的CSFR漏洞，构造页面一个恶意网页B，在页面中包含对发往正常网站A的请求，在用户C加载页面B（或者点击某些元素时触发）时，会触发攻击请求，目的是为了实现虚拟币的转账，请求可能隐藏得很深，用户并不一定能发现，伪造的请求如下：

    ![](https://coderxing.gitbooks.io/architecture-evolution/assets/0D485010-0672-43D8-AC1E-9468D64AA14F.png)

由于加载恶意页面B和触发攻击请求都是在用户浏览器端完成的，因为之前用户登录过正常网站，发往正常网站的请求会带有用户授权信息（在cookie中），在授权信息没有过期的情况达到攻击目的。

CSRF 的防范

目前主要有如下几种方式：

添加 Referer 域名白名单：HTTP 的 Referer 头记录了当前请求的来源页面的URL，如果用户是通过浏览器打开的网页一般都会带有这个信息。可以验证 URL 的域名是否在网站允许的白名单呢内，如果不在则拒绝请求。这种方式实现比较简单，而且可以在web 服务器层统一配置，减少了后端开发成本，当 Referer 页可以伪造，用户浏览器的可靠性也不能完全信赖，判断 Referer 可以做为一种辅助手段，但不能根治 CSRF。

令牌 (Token )验证：令牌验证的方式，这是目前方法CSRF的一种普遍方法，其原理是在用户正式提交数据更新之前，给用户生成一个 token，一方面token保存在服务端，比如Session 或者缓存中，一方面输出请求发生的页面上，在用户提交请求时连同token一同提交，服务获得接收到请求之后再做token验证，token 不存在、或者token不一致，或者失效都算作验证失败。token 的生成具有一定的随机性，而且是在提交数据的页面生成，攻击这往往难于伪造。token 一般作为一个post 字段提交，或者作为ajax请求的header信息提交，例如：
```
<form>
<input name="from" value="rommel" />
<input name="to" value="" />
<input name="csrf_token" value="QMYjiBlZ9V9mGnap" />
</form>

$.ajax({
headers: {
"X-CSRF-TOKEN": "QMYjiBlZ9V9mGnap"
}
});
```
另外，为了更可靠的安全性，token 在使用之后一般置为失效，避免被窃取。

二次验证：对于一些铭感操作，比如设计到交易的操作，可以更加严格一些。在用户提交时可以让用户输入验证码，或者再次输入交易密码，确保是用户的真实操作，而不是机器触发的。

使用 SameSite Cookie 属性：SameSite 是在跨域请求时是否传输 Cookie 的一种约束，顾名思义在 SameSite 的限制下，Cookie 的传输必须在同一个域名下。SameSite 属性有两种限制模式 strict 和 lax，默认为 lax。下面举例说明，对于下面的代码：
```
<?php
//www.a.com/test_samecookie.php
//第二个参数为false表示不不进行覆盖，否则只能设置一个cookie
header("Set-Cookie: cookie1=value1; domain=a.com; SameSite=Strict", false);
header("Set-Cookie: cookie2=value2; domain=a.com; SameSite=Lax", false);
?>

	访问，www.a.com/test_samecookie.php 通过Chome 的开发者工具查看cookie信息，如下：
	
	在 www.b.com/access_same_page_in_site.php 构造同样的页面访问 www.a.com 中的任何页面。
	
	<a href="www.a.com/test.html">test</a>
```	
点击页面上的链接之后，会发现，只有 cookie2 传递到了www.a.com strict 模式限制所有的跨域cookie传输，lax 模式相当于在安全性和可用性之间做了个折中，某些场景允许跨域传输，比如 a 标签中中的GET请求，但会对 img、iframe 和 ajax 中的GET请求以及POST请求做限制，
目前只有 Chrome 和 Opera 浏览器支持 SameSite 属性。
```
		<?php
		$callback = $_GET['callback'];
		$data = array(
		'userid' => '12345678',
		'usernick' => 'coderxing'
		);
		$json = json_encode($data);
		echo "$callback($json);";
		?>
```
输出内容为：
```
		cb({"userid":"12345678","usernick":"coderxing"});
		
		B 网站通过 JQuery 使用 jsonp 的代码如下：
		
		<script src="https://cdn.bootcss.com/jquery/3.2.1/jquery.min.js"></script>
		<script type="text/javascript">
		$.ajax({
		url:"http://www.a.com/jsonp.php?callback=cb",
		dataType:'jsonp',
		jsonp:'callback',
		success:function(result) {
		console.log(result);
		}
		});
		</script>
```
通过Chrome浏览器访问：http://www.b.com/use_jsonp.html，控制台会输出:
```
		<script type="text/javascript">
		var url = "http://www.a.com/jsonp.php?callback=cb";
		//创建 script 节点
		var scriptNode = document.createElement('script');
		scriptNode.type = 'text/javascript';
		scriptNode.src = url;
		//和好回调函数名称一致
		var cb = function(data){
		console.log(data);
		}
		//动态添加 script 节点
		document.head.appendChild(scriptNode);
		</script>
```
 动态添加 script 节点之后，会自动加载 jsonp 网络请求，由于回调函数的名称为为 cb，当加载成功之后会自动执行 cb(data); 函数，使用JSON数据。

 上面的 PHP 服务端代码没有加任何JSON劫持的防范，任何域名都可以通过JSONP的方式进行访问，就像前面CSRF一节介绍的攻击方法一样，如果攻击者诱导受害者访问含有攻击代码的页面，就会获取到相关的JSON数据，达到劫持目的，如果是登录之后才可见的数据，就会暴露用户隐私。

对于JSON 劫持的方法其实和CSRF的防范方式是一脉相承的

对 Referer 进行严格检查，通过白名单方式进行拦截过滤，并包括 Referer 为空的情况，不在白名单内的域名，或Referer为空均返回失败。
使用一次性TOKEN，和JSONP请求同时发送。
对callback参数进行校验，限制长度，并过滤掉符号字符。

