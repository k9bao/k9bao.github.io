# 1. TCP问题集

## 1.1. 服务端关闭后，客户端继续发送数据

服务端返回Reset。详见 ../test/serverClose.cap

## 1.2. 连接一个不存在的IP和端口

## 1.3. 连接一个存在的IP，但是端口没有监听

## 1.4. 单机最多建立多少tcp连接

## 1.5. 使用tcp实现Demo

详见 TCP-IP/test/SimpleNetwork

## 1.6. 实现服务端主动发起连接的例子

## 1.7. 实现同时关闭的例子(含方法)

是否可以通过拔网线来模拟？

## 1.8. `socket.listen(__backlog:int)` 的参数 __backlog 为什么不生效(python3)

## 1.9. 抓包常见错误

- TCP 抓包常见错误
- TCP out-of-order（tcp有问题）                   #多数是网络拥塞引起的
- TCP segment of a reassembled PDU                 #TCP 分片标识
- TCP previous segment lost（tcp先前的分片丢失）
- TCP acked lost segment（tcp应答丢失）
- TCP window update（tcp窗口更新）
- TCP dup ack（tcp重复应答）
- TCP keep alive（tcp保持活动）
- TCP retransmission（tcp 重传）
