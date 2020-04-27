# npm

- npm config set prefix "D:\nodejs\node_global" 设置全局包路径
- npm config set cache "D:\nodejs\node_cache" 设置全局缓存路径

- npm config set registry=http://registry.npm.taobao.org 配置镜像站

- C:\Users\Administrator\.npmrc 此文件就是配置文件，配置过的东西在这里

## 常用命令

- 安装到全局 npm install 模块名 -g | npm i 模块名 -g  i是简写，有时候会删除不了；；如果没有 -g会在当前文件夹下生成node_modules文件夹下载模块放入其中

    -  npm install juery@latest  安装最新稳定版

    - npm install juery@5.21.5   安装指定版

    - npm install juery   安装最新

    - npm install webpack --save-dev  安装开发或者测试环境，不会到生产环境

- 初始化项目 npm init -y 使用默认配置，生成项目的配置文件

-   npm config list 显示所有的配置信息

- 删除 npm uninstall 模块名

- 更新 npm update juery 

- 老版本需要加 --save 才会更改package.json 文件的值；新版本不需要

``
npm install jquery --save  （安装删除）
``