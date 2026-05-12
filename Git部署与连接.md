**git本地部署（Mac）**
基本步骤：
1.检查是否安装git
```
git --version

#如果你需要安装git
bash
brew install git

#Git 必须知道你是谁，这样你的每次提交都会记录作者信息。
git config --global user.name "Xiangzi"
git config --global user.email "你的GitHub邮箱"


```
2.生成ssh key
	私钥（存本地）：相当于身份证，不能泄露
	工钥（放GitHub）：让GitHub确定对象是你

```
ssh-keygen -t ed25519 -C "你的GitHub邮箱"

```


3.将ssh公钥添加到GitHub
查看公钥内容
```
cat ~/.ssh/id_ed25519.pub
```

复制输出内容，然后：
GitHub → 右上角头像 → **Settings** → **SSH and GPG keys** → **New SSH key**
这是为了让GitHub认识你的电脑，之后所有操作无需密码


4.测试SSH是否连接成功
```
ssh -T git@github.com
```
若成功，会出现
```
Hi Xiangzi! You've successfully authenticated.
```
5.设置git告诉他默认使用Git
```
git config --global url."git@github.com:".insteadOf "https://github.com/"
```
6.设置Git的常用习惯（可选）
	默认使用main作为主分支
	```
	git config --global init.defaultBranch main
	```
	每次显示彩色输出
	```
	git config --global color.ui auto
	```
	显示提交图
	```
	git config --global alias.lg "log --graph --oneline --all"
	```
**git连接本地仓库**
1.在GitHub上新建一个新仓库
2.选择SSH URL
3.在本地新建一个项目目录并初始化git
```
mkdir my-project
cd my-project
git init
```
4.添加文件并提交
```
echo "# My Project" > README.md
git add .
git commit -m "Initial commit"
```
5.将本地仓库绑定到Github远程仓库
```
git remote add origin git@github.com:Xiangzi/my-project.git
```

6.推送到GitHub（第一次必须加-u）
```
git push -u origin main
```
如果你的 Git 报错没有 main 分支，可以创建：
```
git branch -M main
git push -u origin main
```

7.打开 GitHub 检查结果
现在你刷新 GitHub，会看到：

- README.md
    
- 提交记录
    
- 代码已同步