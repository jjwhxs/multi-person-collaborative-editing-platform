### 系统介绍

基于Vue和Node实现的多人协作编辑平台采用前后端分离的架构方式，平台实现了注册/登录、首页、与我共享、我的收藏、搜索、新建、导入导出、回收站、个人中心等功能模块。

### 技术选型

开发工具：Webstorm2020.3

运行环境：mysql5.7+nodejs16.0.0

服务端技术：websocket+express+md5

前端技术：vue+axios+element-plus+exceljs

### 成果展示

注册/登录
<img width="1920" height="990" alt="注册登录" src="https://github.com/user-attachments/assets/c2047a0d-076f-41dc-9dfa-378a46a21d84" />

平台首页
<img width="1920" height="990" alt="平台首页" src="https://github.com/user-attachments/assets/9d3e4243-d399-4487-8e94-07c5e17bbc0b" />

与我共享
<img width="1920" height="990" alt="与我共享" src="https://github.com/user-attachments/assets/c879fa6f-03a5-4a7c-8db1-68f636cfed97" />

我的收藏
<img width="1920" height="990" alt="我的收藏" src="https://github.com/user-attachments/assets/a2bf2a71-a967-4fde-9751-9bf64ecfa74f" />

平台搜索
<img width="1920" height="990" alt="平台搜索" src="https://github.com/user-attachments/assets/bade75c9-4a74-420c-b3ab-46f9e97d31c8" />

新建文件
<img width="1920" height="990" alt="新建文件" src="https://github.com/user-attachments/assets/46b8005b-40ef-4386-93c9-509817f16a7a" />

多人协作编辑文件
<img width="1917" height="839" alt="多人协作编辑文件" src="https://github.com/user-attachments/assets/589bdda4-b48b-4bc5-aa5c-3a757f33d07b" />

删除文件
<img width="1920" height="990" alt="删除文件" src="https://github.com/user-attachments/assets/2f5d03b8-f246-49a6-b975-39bdca6d0c1a" />

回收站
<img width="1920" height="990" alt="回收站" src="https://github.com/user-attachments/assets/d37b55ea-bf3e-41cd-922b-8328dbf2b615" />

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

<img width="436" height="166" alt="目录结构展示" src="https://github.com/user-attachments/assets/f552dcee-2e82-45e2-b6fe-0f473e3f2e21" />

4、项目结构展示

<img width="1489" height="989" alt="项目结构展示" src="https://github.com/user-attachments/assets/f9880730-78b8-4d3f-8df4-0b1505b4611d" />

5、运行步骤

1）创建数据库、导入sql脚本

2）修改base.config.js中的数据库配置文件

3）分别在Vue和Node目录下打开cmd，执行npm install下载依赖

4）下载完毕后启动前端npm run serve，启动后端node app.js，访问端口3000

### 获取方式(可远程调试)

访问链接(在浏览器中手动输入下图中的地址)：

<img width="1130" height="135" alt="链接" src="https://github.com/user-attachments/assets/08819328-dad5-4227-907a-d68bbaf4d014" />

若资源获取失败，可添加happy35596339(vx)或1204901965(qq)进行交流
