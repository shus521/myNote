## 建立用户
`create user angeos identified by angeos;`建立了用户：angeos，密码为：angeos

## 对用户授权
`grant connect,resource to angeos;`对用户angeos授予了连接数据库和访问资源的权限

## 对用户授权
`grant create session,dba to angeos;`
## 删除用户
`drop user angeos cascade;`