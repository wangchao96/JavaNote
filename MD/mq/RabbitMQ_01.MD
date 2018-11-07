## 0.写在前面
RabbitMQ 是一个消息代理:它接受和转发消息。你可以把它想象成一个邮局:当你把你想要投寄的邮件放在一个邮箱里时，你可以确定收信人先生或女士最终会把邮件寄给你的收件人。在这个类比中，RabbitMQ是一个邮箱、一个邮局和一个邮递员。

RabbitMQ 与邮局的主要区别在于它不处理纸张，而是接收、存储和转发二进制数据块——消息。

## 1.Producer

![producer](https://user-gold-cdn.xitu.io/2018/11/5/166e330995471e0d?w=71&h=51&f=png&s=1558)

生产就是发送，发送消息的程序是生产者。

## 2.Queue

![queue](https://user-gold-cdn.xitu.io/2018/11/5/166e334160ff66b6?w=130&h=91&f=png&s=885)

队列是位于 RabbitMQ 内的邮箱的名称。尽管消息流经 RabbitMQ 和应用程序，但它们只能存储在队列中。队列只受主机的内存和磁盘限制，它本质上是一个大的消息缓冲区。许多生产者可以向一个队列发送消息，许多消费者可以尝试从一个队列接收数据。

## 3.Consumer

![consumer](https://user-gold-cdn.xitu.io/2018/11/5/166e3397ba1dd954?w=71&h=51&f=png&s=2176)

消费与接受有着相似的含义。消费者是一个主要等待接收消息的程序。

## 4.Exchange

![exchange](https://user-gold-cdn.xitu.io/2018/11/5/166e347b6ace98e4?w=63&h=41&f=png&s=2305)

交换器必须确切地知道如何处理接收到的消息。它应该附加到特定的队列吗?它应该附加到许多队列中吗?或者它应该被丢弃。这些规则由 Exchange Types 类型定义。

    Exchange Types：direct, topic, headers，fanout
    
## 5.Bindings

绑定是用于将消息路由到队列的交换规则。为了指示Exchange E将消息路由到队列Q，Q必须绑定到E。某些 `Exchange Type` 可以使用一个可选的路由键属性。`routing key` 的目的是指定这个消息的路由规则。换句话说，`routing key` 键就像一个过滤器。

如果AMQP消息不能路由到任何队列(例如，因为它发布到的交换器没有绑定)，那么它要么被删除，要么返回给发布者，这取决于发布者设置的消息属性。

## 6.Routing Key
生产者在将消息发送给 Exchange 的时候，一般会指定一个 routing key，来指定这个消息的路由规则，而这个 routing key 需要与 Exchange Type 及 binding key 联合使用才能最终生效。在 Exchange Type 与 binding key 固定的情况下（在正常使用时一般这些内容都是固定配置好的），我们的生产者就可以在发送消息给 Exchange 时，通过指定 routing key 来决定消息流向哪里。RabbitMQ 为 routing key 设定的长度限制为255 bytes。
