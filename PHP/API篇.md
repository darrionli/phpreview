1. Restful是什么？

   REST全名Representational State Transfer，中文可以译为：表现层状态转化，是一种软件设计风格

   http://www.ruanyifeng.com/blog/2011/09/restful.html

2. 如何在不支持 `DELETE` 请求的浏览器上兼容 `DELETE` 请求

   通过服务器读取隐藏表单字段通过POST隧道传递给其他方法，并相应的分派请求。

   但是，在所有主要的Web浏览器(IE，Firefox，Safari，Chrome，Opera)中，XMLHttpRequest(即AJAX调用)

   的实现支持GET，POST，PUT和DELETE。

3. 常见 API 的 `APP_ID` `APP_SECRET` 主要作用是什么？阐述下流程

4. API如何保证数据不被篡改？

   https://zhuanlan.zhihu.com/p/33272881

   https://cloud.tencent.com/developer/article/1165284

   非对称加密（RSA）、MD5摘要、以及令牌机制

   - 使用https进行通信
   - 请求签名，防止参数被篡改
   - 身份确认机制，每次请求都要验证合法性
   - 对敏感的请求和响应进行加解密操作

5. JSON和JSONP的区别

   JSON是一种数据交换格式，JSONP是一种非官方的跨域数据交换协议

   https://www.cnblogs.com/dowinning/archive/2012/04/19/json-jsonp-jquery.html

6. 数据加密和验签的区别

7. RSA是什么

8. API版本兼容怎么处理

   - url参数带上版本号，例如：api.XXX.com/user?v=1.0，这种方法容易实现，但是后期逻辑多维护很麻烦，不建议使用。
   - 每个版本放在不同的文件夹下，例如：api.XXX.com/v1/user、api.XXX.com/v2/user，优点：版本逻辑分开维护，缺点：需要维护多个版本，大部分是重复代码

9. 限流（木桶、令牌桶）

10. OAuth主要用在哪种场景下

11. JWT

12. PHP中`json_encode(['key'=>123])`与`return json_encode([])`的区别，会产生什么问题，如何解决？