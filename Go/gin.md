## 特性
1. **快速**：路由不使用反射，基于Radix树，内存占用少。
    
2.  **中间件**：HTTP请求，可先经过一系列中间件处理，例如：Logger，Authorization，GZIP等。这个特性和 NodeJs 的`Koa`框架很像。中间件机制也极大地提高了框架的可扩展性。
    
3.   **异常处理**：服务始终可用，不会宕机。Gin 可以捕获 panic，并恢复。而且有极为便利的机制处理HTTP请求过程中发生的错误。
    
4.  **JSON**：Gin可以解析并验证请求的JSON。这个特性对`Restful API`的开发尤其有用。
    
5.  **路由分组**：例如将需要授权和不需要授权的API分组，不同版本的API分组。而且分组可嵌套，且性能不受影响。
    
6.  **渲染内置**：原生支持JSON，XML和HTML的渲染
## 安装
````
go get -u -v github.com/gin-gonic/gin
````
## 使用
```
package main

import "github.com/gin-gonic/gin"

func main() {
   //生成一个实例
   r := gin.Default()
   //定义一个路由，当用户访问/test时，返回显示"I'm ok"
   r.GET("/test", func(c *gin.Context) {
      c.String(200, "I'm ok")
   })
   //运行,且指定在1111端口运行
   r.Run(":1111")
}
```
## 路由`Route`
### 请求方法
`GET`、`POST`、`DELETE`、`PUT`、`PATCH`、`OPTIONS`、`ANY`(`ANY`可以匹配任意请求方法)
### 解析路径参数(http://localhost:1111/hello/tianyuan)
```
r.GET("/hello/:name", func(c *gin.Context) {
   name := c.Param("name")
   c.String(http.StatusOK, "Hello %s", name)
})
```
`:name`必须传入`name`参数
`*sex`可选传入`sex`参数
### 解析query参数(http://localhost:1111/hello?name=tianyuan&sex=男)
```
r.GET("/hello", func(c *gin.Context) {
   name := c.Query("name")
   //sex为可选参数，默认男
   sex := c.DefaultQuery("sex", "男")  
   c.String(http.StatusOK, "%s的性别是%s", name, sex)
})
```
### 解析POST参数
```
r.POST("/form", func(c *gin.Context) {
   username := c.PostForm("username")
   password := c.DefaultPostForm("password", "123456")
   c.JSON(http.StatusOK, gin.H{
      "username": username,
      "password": password,
   })
})
```
### Map参数
```
ids := c.QueryMap("ids")
names := c.PostFormMap("names")
```
### 重定向
```
func main() {
   //生成一个实例
   r := gin.Default()
   r.GET("/test", func(c *gin.Context) {
        //方案1
      c.Redirect(http.StatusMovedPermanently, "/index")
        //方案2
      c.Request.URL.Path = "/index"
      r.HandleContext(c)
   })
   r.GET("/index", func(c *gin.Context) {
      c.String(http.StatusOK, "index")
   })
   //运行,且指定在1111端口运行
   r.Run(":1111")
}
```
### 路由分组
```
func main() {
   //生成一个实例
   r := gin.Default()
   defaultHandler := func(c *gin.Context) {
      c.JSON(http.StatusOK, gin.H{
         "path": c.FullPath(),
      })
   }

   v1 := r.Group("/v1")
   {
      v1.GET("posts", defaultHandler)
      v1.GET("series", defaultHandler)
   }

   v2 := r.Group("/v2")
   {
      v2.GET("/posts", defaultHandler)
      v2.GET("/series", defaultHandler)

   }
   //运行,且指定在1111端口运行
   r.Run(":1111")
}
```
### 上传文件
```
//单文件
file, _ := c.FormFile("file")
// 多文件
form, _ := c.MultipartForm()
	files := form.File["upload[]"]

	for _, file := range files {
		log.Println(file.Filename)
		// c.SaveUploadedFile(file, dst)
	}
```
### HTML模板
### 中间件
```
r.Use(gin.Logger())
```
### 热加载调试`Hot Reload`
加载库
```
go get -v -u github.com/pilu/fresh
```
运行`fresh`