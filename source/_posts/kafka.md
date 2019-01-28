---
title: kafka
date: 2017-03-14 16:14:19
tags: [技术]
---
[Kafka ---用途、系统架构与应用](https://conndots.github.io/2015/05/17/kafka-readnotes/)
Kafka的消息存储有着非常简单的存储布局。一个Topic下的每个partition对应一个逻辑上的日志文件。物理上，一个partition对应一个文件夹，包含了消息的信息，还包含了其对应的索引文件。每次Producer向一个partition发布一条消息，Broker简单地把它添加到最后一个段文件的尾部。每个日志文件包含了一个序列的log entrie，每个entry都有一个当前partition下唯一的64字节offset，指明了这条消息的起始位置。

