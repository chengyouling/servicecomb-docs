# REST over HTTP2（Vert.x)

## 开发介绍

参考 [Spring Boot集成Java Chassis介绍](../spring-boot/introduction.md) ，高性能模式使用 REST over HTTP2（Vert.x）。

application.yaml 文件中的配置示例：

```yaml
servicecomb:
  rest:
    address: 0.0.0.0:8080?protocol=http2
    server:
      verticle-count: 8
```

* 启用h2\(Http2 + TLS\)进行通信  
  服务端在配置服务监听地址时，可以通过在地址后面追加`sslEnabled=true`开启TLS通信，具体介绍见[使用TLS通信](../security/tls.md)章节。然后再追加`protocol=http2`启用h2通信。示例如下：

        servicecomb:
            rest:
              address: 0.0.0.0:8080?sslEnabled=true&protocol=http2

* 启用h2c\(Http2 without TLS\)进行通信  
  服务端在配置服务监听地址时，可以通过在地址后面追加`protocol=http2`启用h2c通信。示例如下：

        servicecomb:
            rest:
              address: 0.0.0.0:8080?protocol=http2

* 客户端会通过从服务中心读取服务端地址中的配置来使用http2进行通信。 


## 配置参考

| 配置项                                                         | 默认值               | 含义                                                                       | 注意                                                        | 
|-------------------------------------------------------------|-------------------|--------------------------------------------------------------------------|-----------------------------------------------------------|
| servicecomb.rest.server.http2.useAlpnEnabled                | true              | 是否启用 ALPN                                                                |                                                           |
| servicecomb.rest.server.http2.concurrentStreams             | 100               | 一条连接中，同时支持的最大的stream并发量                                                  | 以server端的concurrentStreams和client端的multiplexingLimit较小值为准 |
| servicecomb.rest.server.http2.HeaderTableSize               | 4096              |                                                                          |                                                           |
| servicecomb.rest.server.http2.pushEnabled                   | true              |                                                                          |                                                           |
| servicecomb.rest.server.http2.initialWindowSize             | 65535             |                                                                          |                                                           |
| servicecomb.rest.server.http2.maxFrameSize                  | 16384             |                                                                          |                                                           |
| servicecomb.rest.server.http2.maxHeaderListSize             | Integer.MAX_VALUE |                                                                          |                                                           |
| servicecomb.Provider.requestWaitInPoolTimeout${op-priority} | 30000             | 在同步线程中排队等待执行的超时时间，单位为毫秒                                                  |                                                           |
| servicecomb.rest.server.requestWaitInPoolTimeout            | 30000             | 同servicecomb.Provider.requestWaitInPoolTimeout${op-priority}, 该配置项优先级更高。 |                                                           |

## 客户端配置

参考 [REST Transport Client 配置项](../config-reference/rest-transport-client.md)
