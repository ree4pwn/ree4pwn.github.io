---
layout: post
title: 2020 Flare-On 7th Write up
---

由于在我开始做题目时比赛仅剩一周，导致没有在比赛期间完成所有的题目，现将其补完。

## Ch1

## Ch3

```c
  if ( *(_BYTE *)(v3[10] + 249) == 1 )
    resetEverything__Q1G0gjmnsnF8mVSgZnKS4w_3((int)v3);
```

```asm
.text:00433FD0                 mov     ecx, ebx
.text:00433FD2                 call    @resetEverything__Q1G0gjmnsnF8mVSgZnKS4w_3@4
.text:00433FD7                 jmp     loc_433D62
```

```c
            if ( *(char *)(v3 + 248) == *(unsigned __int8 *)(v24 + 248) )
            {
              v16 = score__h34o6jaI3AO6iOQqLKaqhw + 1;
```

```asm
.text:00432356                 cmp     edx, eax
.text:00432358                 jz      loc_432261
```
