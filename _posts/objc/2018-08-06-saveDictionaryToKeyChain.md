---
layout: post
title: saveDictionaryToKeyChain
date: 2018-08-06
tag: objc
site: https://zhangkn.github.io
catalog: true
author: kunnan
subtitle: 保存字典字符串到钥匙串
---





# 前言



#### *** Terminating app due to uncaught exception 'NSInvalidArgumentException', reason: '-[__NSCFConstantString count]: unrecognized selector sent to instance 0x63b2490' 

由于保存到到KeychainItemWrapper 的value是字符串，因此采用保存json 格式的字符串保存到其中，间接的相当于保存字典数据到钥匙串



# 例子



```objc
- (NSMutableDictionary *)Wrapperdic {
    
    //
    if (_Wrapperdic == nil) {
        
        CMPayKeychainItemWrapper *wrapper = [[CMPayKeychainItemWrapper alloc] initWithIdentifier:keyChainwrapinitWithIdentifierkey accessGroup:nil];
        
        NSString *strtmpwrapper = [wrapper  objectForKey:(__bridge id)kSecValueData];// 这个保存的只能字符串。 因此我要使用 字典转字符串，到时候再转一次回字典
        //2018-08-06 14:33:22.689 WeChat[4790:562979] *** Terminating app due to uncaught exception 'NSInvalidArgumentException', reason: '-[__NSCFConstantString count]: unrecognized selector sent to instance 0x63b2490'
//        NSDictionary *tmp =
        NSMutableDictionary * tmpwrapper = nil;
        
        NSLog(@"strtmpwrapper :%@ strtmpwrapperlength:%d",strtmpwrapper,strtmpwrapper.length);
        if (strtmpwrapper == nil ) {
            tmpwrapper = nil;
            
        }else {
            //2018-08-06 15:02:05.432 WeChat[4918:567786] *** Terminating app due to uncaught exception 'NSInternalInconsistencyException', reason: '-[__NSCFDictionary setObject:forKey:]: mutating method sent to immutable object'

            tmpwrapper  = [NSMutableDictionary dictionaryWithDictionary:[KNconvertHexStrToString dicWithJsonstr:strtmpwrapper]];
        }
        
        NSLog(@"读出tmpwrapper:%@",tmpwrapper);
        
        if (tmpwrapper == nil ||  tmpwrapper.count == 0)
        {
            
            // 如果是模拟器
            if (TARGET_IPHONE_SIMULATOR){
            }else{
                
                // 保存字段对象
                tmpwrapper = [NSMutableDictionary dictionaryWithCapacity:2];
                // 转为json 字符串
                [tmpwrapper setValue:@"ss" forKey:@"test"];// 防止//2018-08-06 16:01:55.264 WeChat[5121:581395] json 解析错误: --- error Error Domain=NSCocoaErrorDomain Code=3840 "The operation couldn’t be completed. (Cocoa error 3840.)" (No value.) UserInfo=0x1959bb00 {NSDebugDescription=No value.}

                NSLog(@"保存一个null 字典 tmpwrapper:%@",tmpwrapper);
                [wrapper setObject:[KNconvertHexStrToString dictionnaryObjectToString:tmpwrapper] forKey:(__bridge id)kSecValueData];// reason: '*** setObjectForKey: key cannot be nil'
            }
            
            NSLog(@"写入tmpwrapper :%@",tmpwrapper);
            
        }
        
        
        _Wrapperdic = tmpwrapper;
        
    }
    
    NSLog(@"_Wrapperdic:%@", _Wrapperdic);
    
    return _Wrapperdic;
}

```



#### initWithIdentifier

这个值不能随便修改，最好和bid 一致。获取xx+bid: UVXCYJX.KNcom.tencent.xin 

推荐： teamid+ bid

> * 想保存更多信息，除了采用json 字符串，当然好可以使用更多的`initWithIdentifier `
>
>   ![image](https://wx4.sinaimg.cn/large/af39b376gy1fu025a8z5gj20w206cjrr.jpg)

# See Also 

>* [knpost](https://github.com/zhangkn/KNBin/blob/master/knpost) 
>
```
/Users/devzkn/bin//knpost saveDictionaryToKeyChain 保存字典字符串到钥匙串 -t objc
> #原来""的参数，需要自己加上""
```

