---
layout: post
title: BugBounty-GraphQL
---

* TOC
{:toc}

## 攻击面

## CTF

### hackone101 BugDB v1

题目提供了GraphiQl的界面，通过右侧的Docs可以得到所有接口信息

![](../images/bugDB_v1_1.png)

使用Query嵌套查询查询

![](../images/bugDB_v1_2.png)

### hackone101 BugDB v2

考点是`Mutation`的使用

需要将`victim`用户的`Bugs`的`privite`属性设置为`false`

```
mutation {
  modifyBug(id: 2, private: false) {
    ok
    bug {
      id
    }
  }
}
```

### hackone101 BugDB v3

## 漏洞报告

## template
