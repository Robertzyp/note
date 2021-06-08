# rabbitmq

## 基本组件

1、vhost 虚拟主机，默认用第一个就可以了
2、connection 客户端连接到rabbitmq 的连接
3、channel 一个connection 对应多个channel 实现单连接复用
4、message 消息体 消息体里面包含 payload 和 label（exchange name、topic tag）
    - 没有consumer 消息在队列里面堆积
    - ack 确认机制 异步处理
    - 事务机制，同步处理 一般选择ack方式
5、queue 队列 （持久化、自动删除）
6、route key 路由key
7、binding 把route key 和exchange 绑定
8、exchange 交换机 （相当于路由器），消息首先选择 交换机 和routing key 推送


### excahnge
1、fanout 发布订阅 发送到当前exchange 的所有队列中 忽略routing key
2、direct exchange queue  直连 （特殊的direct） 多个消费者，轮询消费，可设置每次只拿一个
3、direct routing key 队列主动选择 可以自主筛选需要的队列数据 
4、 header 根据header 的x-match 进行匹配 一般不用
5、topic  模糊匹配 好像也没有用过

