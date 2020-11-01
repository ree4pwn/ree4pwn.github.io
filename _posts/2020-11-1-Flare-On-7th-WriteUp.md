---
layout: post
title: 2020 Flare-On 7th Write up
---

由于在我开始做题目时比赛仅剩一周，导致没有在比赛期间完成所有的题目，现将其补完。

## Ch1

## Ch3 Wednesday

该程序用sdl2库编写，简单看了一下网上的介绍，属于事件驱动模式的游戏。

拖入ida中查看，可以看到程序的函数名依旧保留，简单翻阅我们可以窥见一个叫做`resetEverything__Q1G0gjmnsnF8mVSgZnKS4w_3@4`的函数，在运行程序后我们在入口`00433A50`下断点。

故意与石块发生碰撞，可以看到栈回溯

```
0069FD2C  00433FD7  return to mydude.00433FD7 from mydude.00433A50   <-----------------update__Arw3f6ryHvqdibU49aaayOg@12
0069FD30  47AE147B  
0069FD34  3F847AE1  
0069FD38  0069FD48  
0069FD3C  00437BBF  return to mydude.00437BBF from mydude.0040C500   <-----------------update__giAKdkRYJ1A0Qn9asB8s9ajA@12
0069FD40  63D0F33D  
0069FD44  0000000A  
0069FD48  63D0F351  
0069FD4C  0000000A  
0069FD50  0069FD68  
0069FD54  74BFC2C3  return to sdl2.74BFC2C3 from ???
0069FD58  47AE147B  
0069FD5C  3F847AE1  
0069FD60  0000000F  
0069FD64  00000000  
0069FD68  0016A028  
0069FD6C  0042CCD7  return to mydude.0042CCD7 from mydude.00437AD0   <------------------@run__E9cSjWeb4G6NszYRcpo6sLA_2@4
```

以上栈回溯到`update`函数，`update`函数一般出现在事件的`callback`中，本题中则是游戏运行的主要`callback`。

尝试将`update__Arw3f6ryHvqdibU49aaayOg@12`中对`resetEverything__Q1G0gjmnsnF8mVSgZnKS4w_3`的调用patch，发现当发生碰撞后，不会重新开始，而是会继续游戏

patch位置如下，全部`nop`

```c
  if ( *(_BYTE *)(v3[10] + 249) == 1 )
    resetEverything__Q1G0gjmnsnF8mVSgZnKS4w_3((int)v3);
```

```asm
.text:00433FD0                 mov     ecx, ebx
.text:00433FD2                 call    @resetEverything__Q1G0gjmnsnF8mVSgZnKS4w_3@4
.text:00433FD7                 jmp     loc_433D62
```

![patch1](../images/2020-11-1-Flare-On-7th-WriteUp/path1.png)

但是游戏运行到胜利分数`296`时，程序缺直接崩溃，没有将flag打印出来。猜测是应为flag是根据每一个石块的上下跳跃是否正确来作为输入，如果直接nop，会产生不正确的输入，需要将每一个石块都判断为对。

回到`resetEverything__Q1G0gjmnsnF8mVSgZnKS4w_3`中，发现符号名`score__h34o6jaI3AO6iOQqLKaqhw`的变量，该变量用来存储分数，查看交叉引用

![]()

存在函数名为`onCollide__9byAjE9cSmbSbow3F9cTFQfLg`函数，推测为发生碰撞的处理函数（事实上发生石块上下均有碰撞体积，按F10可以看到），其中对`score__h34o6jaI3AO6iOQqLKaqhw`的处理可以明显看到如果判断正确则分数加1。

```c
            if ( *(char *)(v3 + 248) == *(unsigned __int8 *)(v24 + 248) )
            {
              v16 = score__h34o6jaI3AO6iOQqLKaqhw + 1;
              if ( __OFADD__(1, score__h34o6jaI3AO6iOQqLKaqhw) )
                raiseOverflow(v22);
              *(_BYTE *)(v3 + 24) = 1;
              score__h34o6jaI3AO6iOQqLKaqhw = v16;
              if ( !(unsigned __int8)isObj(*(_DWORD *)v3, (int)&NTI__bc9cIRpcNby7Dj3TH0kx9cWA_) )
                raiseObjectConversionError();
              v17 = incrSeqV3(*(int **)(v24 + 252), (int)&NTI__pxbIse2JUQkJU0n9blV9bY5g_);
```

那么将以下跳转改为`jmp`即可强制判断每次都正确。

```asm
.text:00432356                 cmp     edx, eax
.text:00432358                 jz      loc_432261
```

最终分数为296后，得到flag

![]()
