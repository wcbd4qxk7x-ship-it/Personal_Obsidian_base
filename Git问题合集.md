[[Git问题合集]]
**在GitHub上更改了代码怎么同步到本地？**
进入本地项目目录:
`git pull`
**可能会遇到：**
	如果你本地有修改，最好commit之后pull
	若不想提交，用stash暂存
	```
	git stash
	git pull
	git stash pop
	```
	本地和远程都改了相同文件
		选择保留本地
		选择GitHub
		合并两者
		然后：```
		git add .
		git commit -m "Resolve conflict"
		```
**本地修改怎么上传到本地**
三步走：
```
#将修改加入暂存区
git add .
#创建一次提交
git commit -m "本地更新的说明"
推送到Github（push）
git push
第一次 push 时如果提示没有上游分支，则用：
git push -u origin main
```
**分支操作**
创建一个本地分支：
```
git switch -c feature-login
```
让这个分支出现在GitHub上：
```
git push -u origin feature-login
```
功能测试成功，合并到main：
先切换到main：
```
git switch main
```
再merge：
```
git merge feature-login
```
如果分支删除了一些代码怎么恢复？
答：在git里的每次commit都会留下记录，只需要找到那次删除代码提交的哈希值，切换到主分支执行 git_revert _哈希 即可将上次删除的操作反向再做一次。（cd到代码所在的根目录）
