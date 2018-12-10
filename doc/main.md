# 服务器端提供的url

## /connect 提供长连接
## /send 发送消息
## /disconnect 断开连接


# 客户端主要做的事情

1. 建立长连接。
2. 发送消息。
3. 接收消息。
4. 断开长连接。

# 连接状态

- connecting  正在连接状态
- connected   连接成功
- disconnected  断开连接


# 频道

- im-connect  监听长连接是否创建成功
- im-send  监听消息发送
- im-unsuccessful 监听 unsuccessful 事件
- im-receive  监听服务器返回的消息
- im-callbackConnect  监听长连接的状态
- im-disconnect  监听消息断开


# 消息队列

- 发送消息队列
- 接收消息队列
- 接收缓存队列
- 回调方法缓存队列
- 消息包超时缓存队列(作用于断开连接的时候，要清除超时处理)


# 时间

- 心跳超时时间
- 网络传输超时时间
- 上一次长连接的时间（预防机器睡眠了之后，js被堵塞住了，然后睡眠好了之后，告知连接失败）

# ID

- 客户端消息id
- 发送的信封id

# 唯一值

- s 服务器端链接唯一标识（一次长连接过程中s不会改变）
- v 服务器端保证连接合法性的锁（每次都会改变）
- currentSendingRequestNum 当前与服务器端连接http 个数。

# 状态
- 连接状态
- 上一次连接状态

# 其他

- 最大通道个数 ：四个

# 通道

通道的概念主要是用于客户端与服务器端进行连接。

通道一：用于建立长连接请求，和接收服务器端的消息  消息类型 connect

通道二：用于发送消息回执。  消息类型 preview

通道三：用于发送聊天消息，保证序列化发送  chat

通道四：发送其他消息报文。  others

# 对外提供的API

## init(options)
初始化

### options参数

- debug  是否开启debug模式，开启了之后，会有运行日志。

- transportType  选择传输的类型 ["long-polling","polling"]

## connect(callback)
创建连接

## send(message,cmd,callback);
发送消息

## receive(callback);
监听服务器端的消息


## disconnect(callback);
断开连接


## listen(cmd,callback)
监听

## removeListen(cmd)
移除监听

