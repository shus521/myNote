1. 在当前目录下初始化新的模块`go mod init test`
2. 移除无用包并下载依赖包`go mod tidy`
3. 验证依赖项是否达到预期目的`go mod verify`
4. 打印模块需求图`go mod graph`