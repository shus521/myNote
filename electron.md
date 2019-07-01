## 主进程(Main Process)
1. 可以使用和系统进行对接的electron api(创建菜单等)
2. 创建多个渲染进程
3. 全面支持`Node.js`
4. 只有一个，作为程序入口
## 渲染进程(Rendener Process)
1. 有多个，每个对应一个窗口
2. 每个都是单独的进程
3. 全面支持`Node.js` `DOM API`
4. 可以使用一部分Electron api
## BrowserWindow(main process)
1. 创建和控制浏览器窗口
```
const { BrowserWindow } = require('electron')
let mainWindow = new BrowserWindow({
    width: 800,
    height: 600,
  })
```
2. 可以使用node api`nodeIntegration: true`
3. 加载html文件`mainWindow.loadFiel('index.html')`
4. 指定父窗口`parent: mainWindow`,随着父窗口关闭而关闭,子窗口显示在父前
## 进程间通讯IPC
main.js
```
  const {ipcMain} = require('electron')
```
```
  ipcMain.on('message', (event, arg) => {
  	//event.sender.send('reply','hello from main')
  	mainWindow.send('reply','hello from main')
  })
```
renderer.js
```
const {ipcRenderer} = require('electron')
```
```
ipcRenderer.send('message', 'hello from renderer')
ipcRenderer.on('reply', (event, arg) => {
	document.getElementById('message').innerHTML = arg;
})
```
## 备注
1. 每次修改main.js后都需要重启才能生效，可以安装模块`cnpm install nodemon --save-dev`,自动检测变化
```
"scripts": {
    "start": "nodemon --watch main.js --exec \"npm run dev\"",
    "dev": "electron ."
  },
```