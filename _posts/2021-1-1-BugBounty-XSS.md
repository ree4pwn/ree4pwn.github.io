---
layout: post
title: BugBounty-XSS
---

* TOC
{:toc}

大学读书的时候，接触的第一个漏洞就是XSS，现在学习XSS则是从实战的角度来从头学习。实战中，更多以[Dompurity](https://github.com/cure53/DOMPurify)一样，对xss防御的绕过。

## 前置知识

## Vuln

+ [Dompurity](https://github.com/cure53/DOMPurify)
  + [DomPurity漏洞库](https://snyk.io/vuln/npm:dompurify)
  + [xss<2.2.2](https://vovohelo.medium.com/from-svg-and-back-yet-another-mutation-xss-via-namespace-confusion-for-dompurify-2-2-2-bypass-5d9ae8b1878f)

## 攻击面

## CTF

## 漏洞报告

## Template/Fuzzer

## 缓解措施

owasp的[cheatsheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)列出了多种缓解措施，事实上无论是CTF还是实战，都是围绕此类缓解措施进行绕过。

## 参考资料

+ [Vulnerability DB](https://snyk.io/vuln/)
+ [通过混淆命名空间绕过DOMPurify实现XSS](https://www.anquanke.com/post/id/219089#h2-4)
