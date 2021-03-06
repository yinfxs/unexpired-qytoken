# 自动更新的企业微信令牌

本模块只干一件事，定期自动获取企业微信令牌并缓存至Redis。

## 全局安装

```bash
npm i wwtoken -g
```

## 新建配置文件

```json
{
  "redis": "redis://127.0.0.1:6379",
  "logsDir": "wwtoken-logs",
  "configs": [
    {
      "corpid": null,
      "corpsecret": null,
      "token_key": "wwtoken_access_tokenA",
      "token_expires": 7000,
      "ticket_key": "wwtoken_jsapi_ticketA",
      "ticket_expires": 7000
    },
    {
      "corpid": null,
      "corpsecret": null,
      "token_key": "wwtoken_access_tokenB",
      "token_expires": 7000,
      "ticket_key": "wwtoken_jsapi_ticketB",
      "ticket_expires": 7000
    }
  ]
}
```

> Tips: 支持JavaScript和JSON两种配置，当不指定配置文件参数时，会自动识别当前执行目录下的`config.js`、`config.json`、`wwtoken.config.js`、`wwtoken.config.json`或`.wwtokenrc`这几个文件名作为配置文件。

### 支持的配置项

* redis：Redis的连接地址，按照`ioredis`的规范指定配置即可
* logsDir：日志存放目录，执行目录下的相对路径或绝对路径皆可
* configs：配置数组部分
* corpid：企业ID
* corpsecret：应用的凭证密钥，每个应用有独立的secret，所以每个应用的access_token应该分开来获取
* token_key：令牌数据缓存在Redis的键，必填参数，默认wwtoken_access_token
* token_expires：令牌自动刷新的间隔秒数，可选参数，目前企业号令牌过期时间为7200秒，默认7000秒获取一次接口并刷新缓存
* ticket_key：JSAPI票据数据缓存在Redis的键，可选参数
* ticket_expires：JSAPI票据自动刷新的间隔秒数，可选参数，默认7000秒获取一次接口并刷新缓存

## 启动模块


```bash
wwtoken -c` <config_path>
```

## 使用令牌

当每次需要使用令牌时，直接通过上面设置的`key`从Redis中获取即可，获取的值即为令牌数据。

## 传送门

* [PM2](https://www.npmjs.com/package/pm2)
* [Redis](https://redis.io/)
* [ioredis](https://www.npmjs.com/package/ioredis)
* [企业微信API文档](https://work.weixin.qq.com/api/doc)
* [企业微信获取access_token](https://work.weixin.qq.com/api/doc#10013/第三步：获取access_token)
* [企业微信获取jsapi_ticket](https://work.weixin.qq.com/api/doc#10029/附录1-JS-SDK使用权限签名算法)
