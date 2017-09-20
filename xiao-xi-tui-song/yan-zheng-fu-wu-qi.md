## 验证服务器

### 明文模式

明文模式下，服务器验证方法很简单。配置完成后，AIOT服务器将发送GET请求到开发者设置的服务器地址（URL）上，GET请求将携带一个参数echostr，它是一个随机的字符串。如果第三方服务器收到该请求，请原样返回echostr参数内容，则验证服务器成功，否则验证失败。返回报文格式如下：

```
{
    "code": 0,
    "result": "echostr"
}
```

我们提供了demo和sdk，开发者可以[下载](https://cnbj2.fds.api.xiaomi.com/lumiaiot/public/message/AIOT%E6%B6%88%E6%81%AF%E6%8E%A8%E9%80%81SDK%E5%8F%8A%E7%A4%BA%E4%BE%8B.zip)供参考。

### 安全模式

安全模式下，服务器验证变得比较复杂，和微信公众号平台的方法类似。 配置完成后，AIOT服务器将发送GET请求到填写的服务器地址URL上，GET请求携带参数如下所示：

* **signature**：加密签名，signature结合了开发者填写的token参数和请求中的timestamp参数、nonce参数；
* **timestamp**：时间戳；
* **nonce**：随机数；
* **echostr**：随机字符串。

若确认此次GET请求来自绿米服务器，请原样返回echostr参数内容，则验证服务器成功，否则接入验证失败。

加密/校验流程如下：

1. 将token、timestamp、nonce三个参数进行字典序排序
2. 将三个参数字符串拼接成一个字符串进行sha1加密
3. 开发者获得加密后的字符串可与signature对比，标识该请求来源于微信


