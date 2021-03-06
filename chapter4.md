# 第四篇：Tracker 协议

Tracker 是一个基于 HTTP(S) 的服务器，通过 HTTP GET 的方法提供服务。**BT客户端**通过 HTTP GET 请求，发送上传、下载相关的信息到 Tracker，以助于 Tracker 统计**种子**的数据信息。请求的返回数据中，包括当前参与该种子上传、下载的**伙伴**信息列表。

Tracker 的 URL 被包含在种子文件中，即 announce 字段，而请求携带的参数则添加到 URL 的 queryString 中。

> 注意：二进制参数必须转义为 URL 标准编码格式。这意味着除 `[-0-9A-Za-z\._~]` 之外的字符都将被转义为形同 `%nn` 的十六进制格式。参考 [RFC1738](http://www.faqs.org/rfcs/rfc1738.html)。

## Tracker 请求参数说明

- **info_hash** 种子文件的 info 字段的 SHA-1 校验值。
- **peer_id** 表示请求者（**BT客户端**）的唯一 ID，一般是客户端在启动时生成的 20 字节字符串。此值不限制格式，任意二进制值都是可以的。但由于 **peer_id** 没有相关的产生准则，因此它仅被假定在您的本地计算机上是唯一的。
- **port** **BT客户端** 监听的网络端口号，一般是 `6881-6889`，当然也可以监听其它的端口。
- **uploaded** 自上一次向 Tracker 发送 `event=start` 请求之后，**BT客户端** （对于该种子）的总上传字节数，以十进制整数 ASCII 字符串表示。
- **downloaded** 自上一次向 Tracker 发送 `event=start` 请求之后，**BT客户端** （对于该种子）的总下载字节数，以十进制整数 ASCII 字符串表示。

（未完待续）

