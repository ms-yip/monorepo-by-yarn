# monorepo by yarn
全局安装yarn
npm install yarn --global // 全局安装

目标： 
1. 组织项目架构：
根项目@monorepo/root 、 packages（子项目）包含 @monorepo/package-a 、@monorepo/package-b、@monorepo/package-c
2. package-b 引入@monorepo/package-a、@monorepo/package-c


具体步骤：
1. 根项目创建
```
  mkdir @monorepo/root
  cd monorepo
  yarn init
```
修改package.json
```
{
  "name": "@monorepo/root",
  "version": "1.0.0",
  "main": "index.js",
  "license": "MIT",
  "private": true,
  "workspaces": [
    "packages/*"
  ],
  "scripts": {
    "dev": "node index.js",
  }
}
```
2. 创建子项目
```
mkdir packages
cd packages
mkdir package-a
cd package-a
yarn init
```

修改package.json
```
{
  "name": "@monorepo/package-a",
  "version": "1.0.0",
  "main": "index.js",
  "license": "MIT",
  "scripts": {
    "dev": "node index.js"
  }
}
```
新增index.js 文件 添加内容：
```
// index.js
console.log('这是 package-a')
```

其他子项目雷同。

3. @monorepo/package-b 引入 @monorepo/package-a、 @monorepo/package-c
```
{
  "name": "@monorepo/package-b",
  "version": "1.0.0",
  "main": "index.js",
  "license": "MIT",
  "scripts": {
    "dev": "node index.js"
  },
  "dependencies": {
    "@monorepo/package-a": "1.0.0",
    "@monorepo/package-c": "1.0.0",
    "vue": "2.7"
  }
}
```

安装依赖
根目录下：yarn [isntall]

只有子项目中版本有差异 才会安装在子项目目录中node_modules

yarn add prettier -W // 来让 yarn workspace 在根目录下安装依赖。
Eg:cd projects/app1 & yarn add hello-world@1.0.0 # 指定version，确保准确命中
or
yarn workspace app1 add hello-world@1.0.0 # 在root中指定workspace，进行安装


yarn workspace <workspace_name> <command>

yarn workspaces info [--json] // 作用：此命令将显示当前项目的工作空间依赖关系树。

yarn workspaces run <command> // 遍历所有workspace执行command命令