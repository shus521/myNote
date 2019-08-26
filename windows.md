1. 查看端口占用情况`netstat -ano |findstr 端口号`
![](images/screenshot_1561629738028.png)
2. 账号密码明明正确却远程不到别的电脑，可能是域有问题，域\用户名登陆
![](https://i.vgy.me/YjsJOV.png)
3. 注册组件`regsvr32 xxx.dll`
4. 复制文件夹
```
    xcopy promotion dist\promotion\ /e
```
     注:必须带\
## 计划任务schtasks
 ```
         /Create         创建新计划任务。  
        /Delete         删除计划任务。  
        /Query          显示所有计划任务。  
        /Change         更改计划任务属性。  
        /Run            按需运行计划任务。  
        /End            中止当前正在运行的计划任务。  
        /ShowSid        显示与计划的任务名称相应的安全标识符。  
        /?              显示帮助消息。
```
创建计划任务参数
```
/sc 指定执行频率(如onstart)
/tr 指定计划任务名称
/tn 指定计划任务将运行的程序
```
示例`schtasks /create /sc onstart /tn memcached /tr "'g:\memcached\memcached.exe' -m 512"`
