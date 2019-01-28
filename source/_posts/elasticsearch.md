---
title: elasticsearch
date: 2017-03-14 16:14:08
tags: [技术]
---

[boosting documents in has_parent query](http://widequestion.com/question/elasticsearch-boosting-documents-in-has_parent-query/)
elasticSearch 组合查询

elasticsearch的查询有两部分组成：query and filter
 query查询器会计算出每份文档对于某次查询有多相关（relevant），然后分配文档一个相关性分数：_score。而这个分数会被用来对匹配了的文档进行相关性排序。相关性概念十分适合全文搜索（full-text search），这个很难能给出完整、“正确”答案的领域。
filter过滤器在性能上对比：filter是不计算相关性的，同时可以cache，因此，filter速度要快于query。

