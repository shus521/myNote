## 合并某几个commit到其他分支
`git cherry-pick <commit id>`
`git cherry-pick 4e934f4`
`git cherry-pick <start-commit-id>..<end-commit-id>`左开右闭
`git cherry-pick <start-commit-id>^..<end-commit-id>`闭区间
`git cherry-pick 4e934f4^ .. 2578705`