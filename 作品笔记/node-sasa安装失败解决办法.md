# 安装 node-sass 快捷解决办法

**先要知道的是，安装 node-sass 时在 node scripts/install 阶段会从 github.com 上下载一个.node 文件，大部分安装不成功的原因都源自这里，因为 GitHub Releases 里的文件都托管在 s3.amazonaws.com 上面，而这个网址在国内总是网络不稳定，所以我们需要通过第三方服务器下载这个文件。**

## 第一步

**在项目目录根目录中新建 .npmrc 文件 加入以下代码**

```js
sass_binary_site=https://npm.taobao.org/mirrors/node-sass/
phantomjs_cdnurl=https://npm.taobao.org/mirrors/phantomjs/
electron_mirror=https://npm.taobao.org/mirrors/electron/
registry=https://registry.npm.taobao.org

```

**这样使用 npm install 安装 node-sass、electron 和 phantomjs 时都能自动从淘宝源上下载，但在使用 npm publish 的时候要把 registry 这一行给注释掉，否则会发布到淘宝源上去**


