## 代码解释
1. `DNSPacket(data)` 根据传入的数据初始化为数据包类；
2. 开始先查看`dns_package.QR`确认是否为查询报文；
3. `self.url_ip` 为字典类型，存储了已知的网址与IP，通过`get`进行查找，如果查找到的IP为`0.0.0.0`就调用父类提供的`generate_response`函数生成一个报错报文，否则就产生一个正常报文；
4. 如果在字典中未寻找到，调用`generate_request`生成查询报文，`self.server_socket.connect(self.name_server)`通过套接字连接到`public DNS server`，发送查询报文并且接受应答报文；
5. 最后调用`send`将报文发送回客户端；