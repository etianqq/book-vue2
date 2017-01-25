# API

```
// 基于全局Vue对象使用http
Vue.http.get('/someUrl', [options]).then(successCallback, errorCallback);
Vue.http.post('/someUrl', [body], [options]).then(successCallback, errorCallback);

// 在一个Vue实例内使用$http
this.$http.get('/someUrl', [options]).then(successCallback, errorCallback);
this.$http.post('/someUrl', [body], [options]).then(successCallback, errorCallback);
```

#### 1.HTTP方法

* get\(url, \[options\]\)
* head\(url, \[options\]\)
* delete\(url, \[options\]\)
* jsonp\(url, \[options\]\)
* post\(url, \[body\], \[options\]\)
* put\(url, \[body\], \[options\]\)
* patch\(url, \[body\], \[options\]\)

###### options对象

| 参数 | 类型 | 描述 |
| :--- | :--- | |
| url | string | 请求的URL |
| method | string | 请求的HTTP方法，例如：'GET', 'POST'或其他HTTP方法 |
| body | Object,FormDatastrin | request body |
| params | Object | 请求的URL参数对象 |
| headers | Object | request header |
| timeout | number | 单位为毫秒的请求超时时间 (0 表示无超时时间) |
| before | function(request)	 | 请求发送前的处理函数，类似于jQuery的beforeSend函数 |
| progress | function(event) |  ProgressEvent回调处理函数 |
| credientials | boolean | 表示跨域请求时是否需要使用凭证 |
| emulateHTTP | boolean | 发送PUT, PATCH, DELETE请求时以HTTP POST的方式发送，并设置请求头的X-HTTP-Method-Override |
| emulateJSON | boolean | 将request body以application/x-www-form-urlencoded content type发送 |





















