---
title: 记录使用hexo+vercel+mongodb搭建博客的过程
date: 2021-05-11 10:27:14
cover: /images/watergirl.png
coverWidth: 1200
coverHeight: 750
tags: 
 - 经验
---
#####   记录使用hexo+nexmoe+vecel+mongodb搭建博客过程中遇到的问题
<!--more-->

### 首先是安装hexo与使用主题nexmoe的过程

这里[折影清梦](https://nexmoe.com/)大佬(nexmoe作者)有专门的安装教程 （偷个懒~）

传送门 https://docs.nexmoe.com/meng-xin-jiao-cheng



tips：若安装hexo，如果提示hexo' 不是内部或外部命令，也不是可运行的程序，那就需要添加环境变量，具体路径为你安装hexo所在node_modules\\.bin文件夹，比如我安装的目录为 G:\Go\hexo\node_modules\\.bin，然后将此路径添加到你的系统变量path中即可，若还是无效，就重启电脑即可



### 接下来是部署的过程这里也是沿用大佬的教程

传送门 https://zhuanlan.zhihu.com/p/347990778

**tips1**：

当你复制了连接字符串之后直接可粘贴到navicat编辑连接中的url...此时navicat会自动帮你配置，你只需要填写密码即可

**tips2**: 安装完vercel之后，如果使用时提示vercel ‘不是内部或外部命令‘，这个时候也需要添加环境变量，可以

npm root  -g 来查看包的全局安装路径

我的安装路径为 C:\Users\HP\AppData\Roaming\npm 然后将其添加到环境变量path中，若无效重启电脑即可

tips3：在最后在getUsername.api测试连接mongodb的时候，可能会出现vercel报500的错误，此时可以参考如下代码：

```typescript
`import { NowRequest, NowResponse } from '@vercel/node';`
`import { MongoClient } from 'mongodb'`
`const CONNECTION_STRING = "mongodb+srv://你的mongodb用户名:你的密码@cluster0.5sfar.mongodb.net/test?retryWrites=true&w=majority"`
`module.exports = async (req: NowRequest, res: NowResponse) => {`
    `console.log(CONNECTION_STRING);`
    `const client = await MongoClient.connect(CONNECTION_STRING, { useNewUrlParser: true, useUnifiedTopology: true });`
    `console.log(client);`
    `const db = await client.db('你的navicat的数据库名称');`
    `var result = await db.collection("你的navicat的集合名称").find().toArray();`
    `res.status(200).json(result);`
`}`
```



至此博客搭建完成