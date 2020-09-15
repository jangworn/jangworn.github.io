---
title: 使用腾讯云Serverless Framework搭建静态网站
date: 2020-01-10 16:16:05
tags: serverless
---

1. 访问https://serverless.cloud.tencent.com/

2. 点击快速部署组件的按钮 website,创建一个应用，复制该应用的 bucketName，比如： sls-cloudfunction-website-动态变化的值-code

3. 安装 serverless  
   npm i -g serverless 或 curl -o- -L https://slss.io/install | bash

4. 创建静态网站  
   mkdir website && vi website/index.html,增加内容 helloworld

5. 增加 serverless 配置文件  
   vi serverless.yml

```
website:
  component: "@serverless/tencent-website"
  inputs:
    code:
      src: website
      index: index.html
      error: 404.html
    region: ap-guangzhou
    bucketName: sls-cloudfunction-website-动态变化的值-code
```

6. 执行 sls --debug ,可以看到运行情况，看到二维码就用微信扫码验证

7. 在我的应用里访问部署的 website 服务
