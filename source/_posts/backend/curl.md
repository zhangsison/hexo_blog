---

title: CURL
date: 2016-03-06
categories: [php]
tags: [CURL]

---

cURL 是一个用来传输数据的工具，支持多种协议，如在 Linux 下用 curl 命令行可以发送各种 HTTP 请求。PHP 的 cURL 是一个底层的库，它能根据不同协议跟各种服务器通讯，HTTP 协议是其中一种



# PHP对CURL函数的封装，支持GET/POST请求

 例：

```bash

		/**
		 * curl 函数
		 * @param string $url 请求的地址
		 * @param string $type POST/GET/post/get
		 * @param array $data 要传输的数据
		 * @param string $err_msg 可选的错误信息（引用传递）
		 * @param int $timeout 超时时间
		 * @param array 证书信息
		 * @author 勾国印
		 */
		function GoCurl($url, $type, $data = false, &$err_msg = null, $timeout = 20, $cert_info = array())
		{
		    $type = strtoupper($type);
		    if ($type == 'GET' && is_array($data)) {
		        $data = http_build_query($data);
		    }
		
		    $option = array();
		
		    if ( $type == 'POST' ) {
		        $option[CURLOPT_POST] = 1;
		    }
		    if ($data) {
		        if ($type == 'POST') {
		            $option[CURLOPT_POSTFIELDS] = $data;
		        } elseif ($type == 'GET') {
		            $url = strpos($url, '?') !== false ? $url.'&'.$data :  $url.'?'.$data;
		        }
		    }
		
		    $option[CURLOPT_URL]            = $url;
		    $option[CURLOPT_FOLLOWLOCATION] = TRUE;
		    $option[CURLOPT_MAXREDIRS]      = 4;
		    $option[CURLOPT_RETURNTRANSFER] = TRUE;
		    $option[CURLOPT_TIMEOUT]        = $timeout;
		
		    //设置证书信息
		    if(!empty($cert_info) && !empty($cert_info['cert_file'])) {
		        $option[CURLOPT_SSLCERT]       = $cert_info['cert_file'];
		        $option[CURLOPT_SSLCERTPASSWD] = $cert_info['cert_pass'];
		        $option[CURLOPT_SSLCERTTYPE]   = $cert_info['cert_type'];
		    }
		
		    //设置CA
		    if(!empty($cert_info['ca_file'])) {
		        // 对认证证书来源的检查，0表示阻止对证书的合法性的检查。1需要设置CURLOPT_CAINFO
		        $option[CURLOPT_SSL_VERIFYPEER] = 1;
		        $option[CURLOPT_CAINFO] = $cert_info['ca_file'];
		    } else {
		        // 对认证证书来源的检查，0表示阻止对证书的合法性的检查。1需要设置CURLOPT_CAINFO
		        $option[CURLOPT_SSL_VERIFYPEER] = 0;
		    }
		
		    $ch = curl_init();
		    curl_setopt_array($ch, $option);
		    $response = curl_exec($ch);
		    $curl_no  = curl_errno($ch);
		    $curl_err = curl_error($ch);
		    curl_close($ch);
		
		    // error_log
		    if($curl_no > 0) {
		        if($err_msg !== null) {
		            $err_msg = '('.$curl_no.')'.$curl_err;
		        }
		    }
		    return $response;
		}

 使用方法如下： 

		$url   = '请求地址';
		$data = array(
		            'phoneNum' => '18614064456',
		        );
		$json = GoCurl($url, $data, 'POST', $error_msg);
		
		$array = json_decode($json, true);
		
		print_r($array);

# curl 
	   $ch = curl_init();
	
	   //设置超时
	
	   curl_setopt($ch, CURLOPT_TIMEOUT,30);
	
	   //这里设置代理，如果有的话
	
	   //curl_setopt($ch,CURLOPT_PROXY, '8.8.8.8');
	
	   //curl_setopt($ch,CURLOPT_PROXYPORT, 8080);
	
	   curl_setopt($ch,CURLOPT_URL,$url);
	
	   curl_setopt($ch,CURLOPT_SSL_VERIFYPEER,FALSE);
	
	   curl_setopt($ch,CURLOPT_SSL_VERIFYHOST,FALSE);
	
	   //设置header
	
	   curl_setopt($ch, CURLOPT_HEADER, FALSE);
	
	   //要求结果为字符串且输出到屏幕上
	
	   curl_setopt($ch, CURLOPT_RETURNTRANSFER, TRUE);
	
	   //post提交方式
	
	   $all_param = 'content='.$content;
	
	   curl_setopt($ch, CURLOPT_POST, TRUE);
	
	   //开始请求
	
	   curl_setopt($ch, CURLOPT_POSTFIELDS, $all_param);
	
	   //运行curl
	
	   $data = curl_exec($ch);
	
	   curl_close($ch);

## post方式

	$data_string :要传输的数据
	
	//初始化
	
	 $ch = curl_init();
	
	 curl_setopt($ch, CURLOPT_URL, '访问的接口地址');
	
	 curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "POST");
	
	 curl_setopt($ch, CURLOPT_POSTFIELDS,$data_string);
	
	 curl_setopt($ch, CURLOPT_RETURNTRANSFER,true);
	
	 curl_setopt($ch, CURLOPT_HTTPHEADER, array('Content-Type: application/json','Content-Length: ' . strlen($data_string)));
	
	//执行并获取接口传的内容
	
	 $ret = curl_exec($ch);
	
	function http_post_json($url, $jsonStr)
	
	{
	
	  $ch = curl_init();
	
	  curl_setopt($ch, CURLOPT_POST, 1);
	
	  curl_setopt($ch, CURLOPT_URL, $url);
	
	  curl_setopt($ch, CURLOPT_POSTFIELDS, $jsonStr);
	
	  curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
	
	  curl_setopt($ch, CURLOPT_HTTPHEADER, array(
	
	      'Content-Type: application/json; charset=utf-8',
	
	      'Content-Length: ' . strlen($jsonStr)
	
	    )
	
	  );
	
	  $response = curl_exec($ch);
	
	  $httpCode = curl_getinfo($ch, CURLINFO_HTTP_CODE);
	
	  return array($httpCode, $response);
	
	}
	
	$url = "http://blog.snsgou.com";
	
	$jsonStr = json_encode(array('a' => 1, 'b' => 2));
	
	list($returnCode, $returnContent) = http_post_json($url, $jsonStr);
	
	function java_id($url,$content){
	
	$ch = curl_init();
	
	//设置超时
	
	curl_setopt($ch, CURLOPT_TIMEOUT,30);
	
	//这里设置代理，如果有的话
	
	//curl_setopt($ch,CURLOPT_PROXY, '8.8.8.8');
	
	//curl_setopt($ch,CURLOPT_PROXYPORT, 8080);
	
	curl_setopt($ch,CURLOPT_URL,$url);
	
	curl_setopt($ch,CURLOPT_SSL_VERIFYPEER,FALSE);
	
	curl_setopt($ch,CURLOPT_SSL_VERIFYHOST,FALSE);
	
	//设置header
	
	curl_setopt($ch, CURLOPT_HEADER, FALSE);
	
	//要求结果为字符串且输出到屏幕上
	
	curl_setopt($ch, CURLOPT_RETURNTRANSFER, TRUE);
	
	//post提交方式
	
	$all_param = $content;
	
	curl_setopt($ch, CURLOPT_POST, TRUE);
	
	//开始请求
	
	curl_setopt($ch, CURLOPT_POSTFIELDS, $all_param);
	
	//运行curl
	
	$data = curl_exec($ch);
	
	return $data;
	
	curl_close($ch);
	
	}
  
```

