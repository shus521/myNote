## 合并某几个commit到其他分支
`git cherry-pick <commit id>`
`git cherry-pick 4e934f4`
`git cherry-pick <start-commit-id>..<end-commit-id>`左开右闭
`git cherry-pick <start-commit-id>^..<end-commit-id>`闭区间
`git cherry-pick 4e934f4^ .. 2578705`
## gitlab服务器系统重装报错
![](https://i.vgy.me/Ia4CkA.png)
原因: 服务器登录标识证书记录下来，下次登录时会去比对之前的记录，由于系统重装标识变了导致不能继续登录
方案:`ssh-keygen -R 192.168.0.40`
## 添加ssh
`ssh-keygen -t rsa -C "youremail@example.com"`
## 本地commit多次的仓库关联新的远程仓库报错
`git pull origin master --allow-unrelated-histories`
## 忽略已经提交过的文件
```
git update-index --assume-unchanged test/test.txt
```
## 合并两个不同的开始提交的仓库，会报错`refusing to merge unrelated histories`
`git pull origin master --allow-unrelated-histories`