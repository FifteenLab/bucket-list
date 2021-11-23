# WebSocket

RFC 6455 
在http协议接基础上使用`Upgrade`报文头开启WebSocket协议通讯。

## Spring WebSocket API
* `WebSocketHandler` 
* `TextWebSocketHandler` 
* `BinaryWebSocketHandler` 

* `WebSocketConfigurer`
* `ServletServerContainerFactoryBean` 服务配置，包括缓存大小、空闲时间等。

## SockJS
不支持WebSocket 的客户端，通过模拟WebSocket 的方式实现通讯。