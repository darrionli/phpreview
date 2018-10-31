1. Restful是什么？

   REST全名Representational State Transfer，中文可以译为：表现层状态转化，是一种软件设计风格

   http://www.ruanyifeng.com/blog/2011/09/restful.html

2. 如何在不支持 `DELETE` 请求的浏览器上兼容 `DELETE` 请求

   通过服务器读取隐藏表单字段通过POST隧道传递给其他方法，并相应的分派请求。

   但是，在所有主要的Web浏览器(IE，Firefox，Safari，Chrome，Opera)中，XMLHttpRequest(即AJAX调用)

   的实现支持GET，POST，PUT和DELETE。

3. 常见 API 的 `APP_ID` `APP_SECRET` 主要作用是什么？阐述下流程

4. API如何保证数据不被篡改？

5. JSON和JSONP的区别

6. 数据加密和验签的区别

7. RSA是什么

8. API版本兼容怎么处理

9. 限流（木桶、令牌桶）

10. OAuth主要用在哪种场景下

11. JWT

12. PHP中`json_encode(['key'=>123])`与`return json_encode([])`的区别，会产生什么问题，如何解决？

    ​