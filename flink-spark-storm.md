

![GitHub Logo](./images/spark_flink_storm.png)
##实时计算框架Storm,Spark和Flink

目前主流的实时计算框架有如下几个：
1. [Storm][StormLink]
1. [Spark][SparkLink]
2. [Flink][FlinkLink]

####一、实时计算框架比较
下面我们从实时性, 吞吐量, 延迟, 和易用性这几个维度来比较这几个计算框架。

1. **实时性**: 
   Storm和Flink从原生上支持了实时流计算, 而Spark是通过“微批量”(Micro-Batch)来模拟实时流计算的。因此Spark的实时性不如Storm和Flink。

2. **吞吐量**:
   影响吞吐量的一个重要因素是消息确认机制，Storm对每一条消息都进行确认，如果失败则从源头重发。 而Flink引入了CheckPoint概念，可以批量的对处理失败的消息进行重新处理。从下图可以看出，Flink的吞吐是Storm的10倍+。
   ![Storm VS Flink](./images/storm_vs_flink.png)

   Spark和Flink的吞吐能力相差不大。
3. **延迟**:
    Spark本质上是一个批量计算框架。Spark Streaming是Spark对流式计算的扩展，通过微批量来模拟实时流计算。实时性上比Storm和Flink要低，秒级高延迟。而Storm和Flink, 原生支持实时流计算，具有毫秒级延迟的特性。
4. **易用性**:
    使用Storm开发实时计算任务，就好像写一个多线程的java程序，只不过这些线程跑在了不同的机器上。Storm从框架层面对实时计算任务的支持比较少，而Spark和Flink对实时计算任务进行了抽象，从框架层面上提供了高阶API，例如对数据流的抽象，对时间窗口的抽象，和SQL查询支持。

下表展示了三种实时计算框架的比较:



|        | Storm      | Spark Streaming | Flink      |
| ------ | ---------- | --------------- | ---------- |
| 实时性 | 原生支持   | Micro-Batch     | 原生支持   |
| 吞吐量 | 低         | 高              | 高         |
| 延迟   | 毫秒级延迟 | 秒级高延迟      | 毫秒级延迟 |
| 易用性 | 低         | 高              | 高         |

可以看出，Flink在实时性，吞吐量，延迟和易用性上相对Storm和Spark具有优势。

####二、各厂商使用情况

我们看看几家大厂的实时计算框架使用情况：
* 今日头条使用Flink取代Storm ,2017年开始构建基于Flink的流计算平台，**2018年中旬**完成了所有实时业务Storm向Flink迁移。[^1]
*  阿里巴巴绝大多数的技术部门都在使用Blink（Flink），2018双11当天数据处理全部实时化，峰值处理能力超过4亿条记录每秒。[^2]
* 饿了么Flink成为实时计算框架首选，逐步取代Storm/Spark。[^3]
* 美团从Storm迁移到Flink 。[^4]

在Flink还没有成熟之前，各大厂商的实时计算框架主要使用Storm， 例如今日头条算法构架师曹欢欢博士在**2018年1月**分享的《今日头条算法原理》[^5]，使用了Storm作为实时计算框架。几个月后的**2018年中旬**，今日头条完成了所有实时业务从Storm到Flink的迁移。

![JRTT STORM](./images/jrtt_storm.jpeg)

目前各大厂商主流的实时计算框架已经从Storm迁移到Flink。

####三、总结
我们从实时性, 吞吐量, 延迟, 和易用性这几个维度比较，发现Flink在各个维度上都优于其他两个框架， 从各大厂商的技术迁徙上发现目前Flink是主流的，最流行和通用的实时流计算框架。


[^1]: https://www.chainnews.com/articles/610462266264.htm
[^2]: https://zhuanlan.zhihu.com/p/27141199
[^3]: https://mp.weixin.qq.com/s/q1ZclPMsFCLogFO0-A8D3w
[^4]: https://zhuanlan.zhihu.com/p/47146538
[^5]: http://www.sohu.com/a/216961197_114778

[StormLink]: https://storm.apache.org/  "Apache Storm"
[SparkLink]: https://spark.apache.org/  "Apache Spark"
[FlinkLink]: https://flink.apache.org/  "Apache Flink"
