### 系统介绍

基于Vue和Node实现的多人协作编辑平台采用前后端分离的架构方式，平台实现了注册/登录、首页、与我共享、我的收藏、搜索、新建、导入导出、回收站、个人中心等功能模块。

### 技术选型

开发工具：Webstorm2020.3

运行环境：mysql5.7+nodejs16.0.0

服务端技术：websocket+express+md5

前端技术：vue+axios+element-plus+exceljs

### 成果展示

注册/登录 输入图片说明

平台首页 输入图片说明

与我共享 输入图片说明

我的收藏 输入图片说明

平台搜索 输入图片说明

新建文件 输入图片说明

多人协作编辑文件 输入图片说明

删除文件 输入图片说明

回收站 输入图片说明

### 源码展示

module.exports = () => {

const wss = new WebSocketServer({ port: ws_port }); // ws server

logger.success(WS 服务初始化成功，连接地址：ws://localhost:${ws_port});

// 需要在 req.url 中解析 type 识别是 yjs 还是 luckysheet

wss.on("connection", (conn, req) => {

// 解析地址 type 参数

try {

  let type = req.url.split("?")[1];
  
  type = type.toString().includes("/")
  
    ? type.split("/")[0]
    : type.split("&")[0].split("=")[1];

  conn.type = type;

  switch (type) {
  
    case "yjs":
      return yjsHandle(wss, conn, req); // 当前未关联 文件！！

    case "luckysheet":
      return luckysheetHandle(wss, conn, req);

    case "canvas-editor":
      return canvasEditorHandle(wss, conn, req); // 当前未关联 文件！！
    default:
      logger.error("未解析到Type类型");
      break;
      
  }
  
} catch (error) {

  logger.error("未解析到Type类型");
  
}

});

wss.on("close", () => {});

wss.on("error", () => {}); };

### 账号地址及其它说明

1、地址说明

登录页：localhost:3000

2、账号说明

用户：zhangsan/123456

3、目录结构展示

输入图片说明

4、项目结构展示

输入图片说明

5、运行步骤

1）创建数据库、导入sql脚本

2）修改base.config.js中的数据库配置文件

3）分别在Vue和Node目录下打开cmd，执行npm install下载依赖

4）下载完毕后启动前端npm run serve，启动后端node app.js，访问端口3000

### 获取方式(可远程调试)

访问链接(在浏览器中手动输入下图中的地址)：

输入图片说明

若资源获取失败，可添加happy35596339(vx)或1204901965(qq)进行交流
