---
layout: post
title: hook_methods_in_ios
date: 2018-08-14
tag: hook
site: https://zhangkn.github.io
catalog: true
author: kunnan
subtitle: Common hook methods in iOS
---



# 前言

> * iOS    中常见的hook方式
>
>   * 利用[运行时AP](https://kunnan.github.io/tags/#Runtime)I ，Method Swizzling ：  通过修改oc 函数的IMP达到替换方法实现的目的
>
>   * fishhook： 
>
>   * cydia substrate
>
>     * ios11 使用Electra 越狱之后，存放dylib的path: `/usr/lib/TweakInject`
>
>       * Framework 存放的path
>
>         ```
>             cp -r ~/Projects/_window/LatestBuild/AFNetworking.framework ~/Layout/System/Library/Frameworks/
>         
>         ```
>
>         
>
>       *  干脆给他建立个软连接算了       ` /bin/ln -s   /usr/lib/TweakInject /Library/MobileSubstrate/DynamicLibraries `
>
>         *  先备份` cp -r /Library/MobileSubstrate/DynamicLibraries ~/`，再删除，再创建ln
>
>           ```
>                # rm -rf /Library/MobileSubstrate/DynamicLibraries
>           ```
>
>           
>
>     * `/Library/MobileSubstrate/DynamicLibraries/`
>
>   

# See Also 

>* [knpost](https://github.com/zhangkn/KNBin/blob/master/knpost) 
>
```
/Users/devzkn/bin//knpost hook_methods_in_ios Common hook methods in iOS -t hook
> #原来""的参数，需要自己加上""
```
