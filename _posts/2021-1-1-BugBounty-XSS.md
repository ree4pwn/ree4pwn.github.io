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

+ 邮箱类服务的XSS导致邮件泄漏
+ Electron的桌面软件导致RCE

### Electron

鉴于Electron内的XSS可能导致RCE，所以单独列为一类

参考资料

+ [【技术分享】奇淫技巧：看我如何将XSS转化成了RCE](https://www.anquanke.com/post/id/86592)
+ [Modern Alchemy: Turning XSS into RCE](https://blog.doyensec.com/2017/08/03/electron-framework-security.html)
+ [Electron Security Checklist](https://www.blackhat.com/docs/us-17/thursday/us-17-Carettoni-Electronegativity-A-Study-Of-Electron-Security-wp.pdf)
+ [Electron hack —— 跨平台 XSS](https://paper.seebug.org/370/)
+ [Awesome Electron.js hacking & pentesting resources](https://github.com/doyensec/awesome-electronjs-hacking)
+ [Electron程序开启DevTools](https://rce.today/posts/Electron%E5%BC%80%E5%90%AFDevTools/)

## CTF

## 漏洞报告

+ [Another XSS in Google Colaboratory](https://blog.bentkowski.info/2018/09/another-xss-in-google-colaboratory.html?view=sidebar)

## Template/Fuzzer

## 缓解措施

owasp的[cheatsheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)列出了多种缓解措施，事实上无论是CTF还是实战，都是围绕此类缓解措施进行绕过。

## 参考资料

+ [Vulnerability DB](https://snyk.io/vuln/)
+ [通过混淆命名空间绕过DOMPurify实现XSS](https://www.anquanke.com/post/id/219089#h2-4)
+ [Cross-site scripting (XSS) cheat sheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet)
