---
layout: post
title: BugBounty-GraphQL
---

* TOC
{:toc}

## 前置知识

官方文档

+ [https://graphql.cn/](https://graphql.cn/learn/queries/#mutations)

分析工具

+ [chrome插件版Graphiql](https://chrome.google.com/webstore/detail/graphiql-extension/jhbedfdjpmemmbghfecnaeeiokonjclb?hl=en)
+ [graphdoc生成文档](https://github.com/2fd/graphdoc)

通用自省payload，graphiql默认发送

```
{"query":"\n  query IntrospectionQuery {\n    __schema {\n      queryType { name }\n      mutationType { name }\n      subscriptionType { name }\n      types {\n        ...FullType\n      }\n      directives {\n        name\n        description\n        locations\n        args {\n          ...InputValue\n        }\n      }\n    }\n  }\n\n  fragment FullType on __Type {\n    kind\n    name\n    description\n    fields(includeDeprecated: true) {\n      name\n      description\n      args {\n        ...InputValue\n      }\n      type {\n        ...TypeRef\n      }\n      isDeprecated\n      deprecationReason\n    }\n    inputFields {\n      ...InputValue\n    }\n    interfaces {\n      ...TypeRef\n    }\n    enumValues(includeDeprecated: true) {\n      name\n      description\n      isDeprecated\n      deprecationReason\n    }\n    possibleTypes {\n      ...TypeRef\n    }\n  }\n\n  fragment InputValue on __InputValue {\n    name\n    description\n    type { ...TypeRef }\n    defaultValue\n  }\n\n  fragment TypeRef on __Type {\n    kind\n    name\n    ofType {\n      kind\n      name\n      ofType {\n        kind\n        name\n        ofType {\n          kind\n          name\n          ofType {\n            kind\n            name\n            ofType {\n              kind\n              name\n              ofType {\n                kind\n                name\n                ofType {\n                  kind\n                  name\n                }\n              }\n            }\n          }\n        }\n      }\n    }\n  }\n"}
```

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

## 参考资料

+ [攻击GraphQL](https://xzfile.aliyuncs.com/upload/zcon/2018/7_%E6%94%BB%E5%87%BBGraphQL_phithon.pdf)
