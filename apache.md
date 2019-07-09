1. 安装目录`apache\bin\ab.exe`,一般apache自带，如无自行下载
2. 参数说明

|  参数 | 说明  |
| --- | --- |
|  -n   | 指定请求数 |
| -c| 并发数，一次发送多少请求|
| -T | post发送的数据类型，也就是header中content-type的值  如-T application/json 说明发送的是json数据 |
| -p| 使用post方式发送数据|
| -H | 在header中添加信息 |