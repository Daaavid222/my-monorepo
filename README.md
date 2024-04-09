## 基于lerna+pnpm构建的monorepo项目
### 1、全局安装pnpm、lerna
>npm i -g pnpm

>npm i -g lerna
### 2、创建项目目录monorepoTest，并初始化
>lerna init

（lerna工具会默认使用npm进行项目搭建）
### 3、删除初始的node_modules文件夹，手动创建pnpm配置文件pnpm-workspace.yaml
pnpm-workspace.yaml内容：
>packages:
  -'packages/*'
  ### 4、执行pnpm i安装环境依赖，并创建文件夹packages
>pnpm i
### 5、在packages/下创建项目common、pck1、pck2进行测试
5.1 创建common文件夹，在文件夹中执行pnpm init，创建index.js执行文件
>module.exports = function (v) {
  return v + '===---';
}

在package.json中添加指令
>"dev": "node index.js"

5.2 pck1、pck2同理，index.js内容分别为
>const common = require('common');
>console.log(common('pck1'))

>const common = require('common');
>console.log(common('pck2'))
 
 ### 6、回到monorepoTest目录下，将公共组件库和公共js库安装到根环境中，使其可以被所有项目程序调用
 >pnpm i -w common

### 7、执行pck1、pck2项目
>pnpm run dev

可以分别看到打印结果‘pck1===---’ 和 ‘pck2===---’

### 8、移除软连接，可以使用pnpm remove xxx
>pnpm remove common