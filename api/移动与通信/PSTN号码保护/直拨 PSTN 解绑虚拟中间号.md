## 1. 接口描述

功能： 直拨 PSTN 解绑虚拟中间号（APP 使用方发起）    
接口地址： `http://HOST/201511v3/delVirtualNum?id=xxx` 
请求方式：POST  

>**注意：**
>上述接口地址的 ID 值测试时由腾讯统一分配

## 2. 参数说明 
| 参数名 | 要求 | 备注 | 
|---------|---------|------------|
| appId | 必选 | xxx | 
| requestId | 可选 | session buffer，字符串最大长度不超过 48 字节，该 requestId 在后面回拨请求响应和回调中都会原样返回 | 
| bindId | 必选 | 双方号码 + 中间号绑定 ID，该 ID 全局唯一 | 
| bizId | 可选 | 应用二级业务 ID，bizId 需保证在该 appId 下全局唯一，最大长度不超过 16 个字节。 | 

## 3. 返回结果
| 参考值 | 描述 | 
|---------|---------|------------|
| 0 | 成功 | 
| -1 | 版本不支持 | 
| -2 | 参数异常 | 
| -204 | bindId 不存在 | 
| -205 | 绑定时带了 bizId，解绑时没有带 bizId 字段 | 
| -501 | 平台处理请求异常（业务做容灾处理） | 

| 变量名 | 类型 | 说明 | 
|---------|---------|------------|
| bindId | String | 绑定 ID，该 ID 全局唯一 | 
| refLeftNum | String | 中间号还剩引用计数，如果计数为 0 会解绑 | 
| requestId | String | requestId 原样返回 | 

## 4. 示例

成功： 
```
{"errorCode":"0","requestId":"vultureli123456","bindId":"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"}
```


失败： 
```
{"errorCode":"-1","msg":"version not supported"}
```

