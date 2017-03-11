---
title: play初探及一些问题总结
tags: [技术]
date: 2014-06-07
---

直接官网，看一遍Play 2.0 for Scala developers，就会让人心动的

intellij装好play插件，新建项目就可运行起个hello world了。

练习下get返回json数据的操作

配置mongo，redis插件

这样写api就足够了

不过网上说到的发布方式没提到：

	java -Dhttp.port=8088 -jar /home/duane/playTest/target/scala-2.10/playTest-assembly-1.0.jar

这样一条命令就搞定的，整个过程主要就sbt assembly配置里冲突的解决有点麻烦，

所以比较有点价值的感觉就build.sbt的这个文件

```scala

import AssemblyKeys._

import play.Project._

assemblySettings

name := "playTest"

version := "1.0"

scalaVersion := "2.10.4"

playScalaSettings

resolvers += "seids" at "http://pk11-scratch.googlecode.com/svn/trunk"


libraryDependencies ++= Seq(
  ("play" %%  "play" % "2.1.1" % "provided")
    .exclude("org.apache.logging.log4j","og4j-core")
    .exclude("org.apache.logging.log4j","log4j-to-slf4j")
    .exclude("org.slf4j","jcl-over-slf4j")
    .exclude("org.scala-stm", "scala-stm_2.10.0"),
  "mysql" % "mysql-connector-java" % "5.1.18",
  "org.reactivemongo" %% "play2-reactivemongo" % "0.10.2",
  //"net.debasishg" %% "redisclient" % "2.12",
  "org.sedis" % "sedis_2.10.0" % "1.1.1",
  "com.typesafe" %% "play-plugins-redis" % "2.1.1"
)

libraryDependencies ~= { _ map {
  case m if m.organization == "com.typesafe.play" =>
    m.exclude("commons-logging", "commons-logging")
      .exclude("org.apache.logging.log4j","og4j-core")
      .exclude("org.apache.logging.log4j","log4j-to-slf4j")
  case m => m
}}

mergeStrategy in assembly <<= (mergeStrategy in assembly) { (old) =>
{
  case PathList("play", "core", xs @ _*) => MergeStrategy.first
  case PathList("META-INF", xs @ _*) => MergeStrategy.discard
  case PathList(ps @ _*) if ps.last endsWith ".html" => MergeStrategy.first
  case "application.conf" => MergeStrategy.concat
  case "unwanted.txt"     => MergeStrategy.discard
  case x => old(x)
}
}

test in assembly := {}

run in Compile <<= Defaults.runTask(fullClasspath in Compile, mainClass in (Compile, run), runner in (Compile, run))

```

