
**能不用图形界面，只靠终端把自己一天的工作搞定的人，大致就可以叫“熟悉 Linux 系统”了。**

---

## **一、什么水平才叫“熟悉 Linux 系统”？**

  

可以用下面这份“能力清单”自检——大部分都做到，就算熟悉了：

1. **文件 & 目录操作全靠命令行**
    
    - 会用 cd、ls、cp、mv、rm、mkdir、find、grep、less 等命令
        
    - 能在命令行里轻松地：新建/移动/删除文件夹和文件，查找文件内容
        
    
2. **懂用户、权限和 sudo**
    
    - 知道什么是 root、普通用户、用户组
        
    - 看得懂 ls -l 的权限位（rwxr-xr-x 这串东西）
        
    - 知道什么时候该用 sudo，知道乱用 sudo rm -rf / 是作死
        
    
3. **会安装和管理软件**
    
    - 在 Ubuntu 下会用 apt：
        
        - sudo apt update && sudo apt upgrade
            
        - sudo apt install xxx
            
        
    - 知道“软件仓库”“包管理器”的概念
        
    
4. **能查看和管理进程 / 服务**
    
    - 会用 ps、top/htop、kill 找出哪个程序在占 CPU / 内存
        
    - 会用 systemctl 管理服务：start/stop/status/enable 等
        
    
5. **基本网络排查没问题**
    
    - 知道 IP、端口这些概念
        
    - 会用 ping、curl 或 wget、ss/netstat 等看网络是否通、端口是否在监听
        
    
6. **看得懂大部分错误提示，能自己排错一轮**
    
    - 出错时会：看日志 (journalctl / /var/log/)、用 grep 搜关键字
        
    - 知道怎么把报错复制去搜索，而不是直接换电脑 :)
        
    
7. **会写简单 shell 脚本自动化**
    
    - 能写几十行以内的 bash 脚本：循环、条件、变量、重定向、管道
        
    - 比如：自动备份、批量改名、批量处理文件
        
    
8. **能独立搭一个小环境**
    
    - 比如：在一台新的 Ubuntu 上，从零开始装好 Python/C++ 开发环境或 ROS
        
    - 碰到依赖问题、缺包问题，能自己查文档、尝试解决
        
    

  

达到这程度，再说“我熟悉 Linux”，就非常合理了。

---

## **二、小白学习顺序指南（按阶段走）**

  

你现在：Mac + Ubuntu 虚拟机，非常适合 Linux 学习。

**建议原则：日常命令可以在 Mac 练，涉及 apt / systemd 这些就用 Ubuntu。**

  

下面按阶段给你一个学习路线，你可以当成“顺序任务清单”来过关：

---

### **第 0 阶段：准备环境（0～1 天）**

  

**目标：有一个“敢乱搞”的 Linux 环境。**

1. 确认虚拟机里是 Ubuntu（LTS 版本优先，比如 22.04）
    
2. 在 Ubuntu 里：
    
    - 能打开 Terminal
        
    - 能切换输入法、打中文
        
    
3. 学会拍快照 / 备份虚拟机
    
    - 这样哪怕把系统玩坏了，也能一键回滚，不怕尝试
        
    

  

> 完成标志：

> 你敢在 Ubuntu 里试着乱删一个测试文件夹，而不担心“整个电脑坏掉”。

---

### **第 1 阶段：基本概念 + 终端入门（1～3 天）**

  

**目标：知道自己身在何处、敲的是什么。**

  

要理解的名词：

- Linux 内核 vs 发行版（Ubuntu、Debian、CentOS…）
    
- Shell（bash）是什么
    
- 命令行 vs 图形界面（GUI）
    
- 路径：绝对路径 /home/xxx / 相对路径 ./ ../
    

  

要学的命令：

- pwd：我在哪
    
- ls：列目录
    
- cd：切换目录
    
- clear：清屏
    
- man、xxx --help：查命令帮助
    
- Tab 自动补全、方向键调用历史命令
    

  

**练习建议：**

- 每次开机：只用终端在你的 Home 目录里来回走一圈
    
- 尝试用 man ls 看说明，随便试一试几个参数（比如 ls -l、ls -a）
    

---

### **第 2 阶段：文件 & 目录操作（3～7 天）**

  

**目标：不用文件管理器，只用命令就能打理文件。**

  

要学的命令：

- 新建 / 删除
    
    - mkdir、touch、rm、rm -r
        
    
- 复制 / 移动 / 重命名
    
    - cp、mv
        
    
- 查看内容
    
    - cat、less、head、tail
        
    
- 查找
    
    - find 查文件
        
    - grep 查内容
        
    

  

**练习任务（建议你真做一遍）：**

1. 在 Home 里建个 playground 目录，进去后：
    
    - 一条命令创建 file1.txt ~ file5.txt
        
    - 把其中两个移动到一个子目录 subdir
        
    - 把剩下的删掉
        
    
2. 写几行文字到 notes.txt（可以用 nano 或 echo "..." >> notes.txt）
    
    用 grep 搜索某个单词出现在哪几行。
    

  

> 完成标志：

> 你能在一个完全“陌生”的目录里，仅靠命令完成：

- > 新建 / 删除 / 找回 / 查内容
    
- > 不再需要图形界面来帮忙。
    

---

### **第 3 阶段：用户 & 权限 & sudo（第 1～2 周）**

  

**目标：理解“谁能干什么”，不再害怕 Permission denied。**

  

要理解的概念：

- 用户（whoami）、用户组（groups）
    
- root 用户 vs 普通用户
    
- 权限 9 位：rwxr-xr-- 分别是谁的权限
    
- chmod、chown 干什么用
    
- 为什么有些命令要 sudo 才能跑
    

  

要学的命令：

- id、whoami、groups
    
- ls -l
    
- chmod、chown
    
- sudo、sudo -i
    

  

**练习：**

1. 用 touch 创建一个脚本文件 test.sh，给它执行权限 chmod +x test.sh
    
    看看加不加 +x 有什么区别。
    
2. 找一个系统目录（比如 /etc）去创建文件，看看会不会权限不够；
    
    再用 sudo 重试，感受一下差异。
    

  

> 完成标志：

> 看到 -rwxr-xr-x 你能大致说出：

- > 哪部分是所有者/用户组/其他人
    
- > 哪个字母代表读/写/执行
    
    > 碰到权限错误知道用哪些命令去排查。
    

---

### **第 4 阶段：软件安装 & 包管理（第 2～3 周）**

  

**目标：可以自己在新系统上装常用软件。**

  

在 Ubuntu 中：

- 知道 apt 是包管理器（Ubuntu 用 apt）
    
- 命令：
    
    - 更新：sudo apt update
        
    - 升级：sudo apt upgrade
        
    - 安装：sudo apt install xxx
        
    - 卸载：sudo apt remove xxx
        
    
- 懂大概：
    
    - 什么是“仓库 / 源”
        
    - .deb 包是啥（像 Windows 的安装包，但托管在仓库里）
        
    

  

**练习：**

1. 用 apt 安装一个你真会用的软件，比如 htop、git、curl
    
2. 用 which 看看它安装到哪里：which htop
    
3. 卸载掉再装一遍
    

  

> 完成标志：

> 换一台新的 Ubuntu，只要有网络，你能：

- > 更新系统
    
- > 安装终端工具、编辑器、开发环境
    

---

### **第 5 阶段：进程、服务与系统状态（第 3～4 周）**

  

**目标：系统卡了、端口被占用时，你能查出是谁干的。**

  

要学的命令：

- 查看进程：
    
    - ps aux、top（或装个 htop）
        
    
- 杀进程：
    
    - kill PID、kill -9 PID
        
    
- 后台任务：
    
    - 命令后加 &，jobs、fg、bg
        
    
- 服务 & 开机启动（systemd）：
    
    - systemctl status xxx
        
    - systemctl start/stop/restart xxx
        
    - systemctl enable/disable xxx
        
    

  

**练习：**

1. 开几个 sleep 1000 或者 yes 之类的程序，让 CPU 飙一点
    
    用 top 找出来并杀掉。
    
2. 用 sudo systemctl status ssh 看看 ssh 服务状态（如果有），
    
    尝试 start / stop 一下观察变化。
    

  

> 完成标志：

> 电脑一卡，你知道用 top 或 htop 去看是谁占资源，而不是重启。

---

### **第 6 阶段：网络基础与排错（第 4～5 周）**

  

**目标：网页打不开时，知道大致是哪一层出问题。**

  

要学的命令：

- ip addr 或 ip a：看 IP
    
- ping：连不连得上某个地址
    
- curl 或 wget：测试 HTTP 请求
    
- ss -tulpn：查看端口占用（旧一点用 netstat）
    

  

**练习例子：**

1. ping baidu.com 看看能否连通
    
2. 用 Python 或 python3 -m http.server 8000 在本地起一个简单 web 服务器
    
    然后用 curl localhost:8000 访问
    
    再用 ss -tulpn | grep 8000 看看哪个程序占了这个端口
    

  

> 完成标志：

> 至少能区分：

- > 是自己机器没网
    
- > 还是服务器连不上
    
- > 还是服务没起来 / 端口没监听
    

---

### **第 7 阶段：常用工具 & 编辑器（过程贯穿始终）**

  

**目标：能在纯终端环境下正常工作。**

  

推荐工具：

- 编辑器：nano（上手简单）、vim（后期再慢慢学）
    
- 文件压缩：
    
    - tar、gzip、zip、unzip
        
    
- 远程登录：
    
    - ssh、scp
        
    
- 常用增强：
    
    - tmux 或 screen（会话保持）
        
    
- 查找 & 批处理：
    
    - find、grep、xargs
        
    

  

**练习：**

- 尝试用 nano 或 vim 完整写一个小脚本
    
- 打包一个目录成 .tar.gz 再解压
    
- 用 ssh 登录到虚拟机或另一台机器（后面你玩服务器、ROS 都要用）
    

---

### **第 8 阶段：Shell 脚本入门（第 5～6 周）**

  

**目标：把重复劳动交给脚本。**

  

要掌握的点：

- 脚本基本结构：#!/bin/bash
    
- 变量：name="Xxx"、$name
    
- 条件：if ... then ... fi
    
- 循环：for、while
    
- 参数：$1、$2、$@
    
- 重定向与管道：>、>>、|、2>
    

  

**练习项目示例：**

1. 写一个“批量改名脚本”：
    
    把某个目录下所有 .txt 文件改成 前缀_原文件名.txt
    
2. 写一个“简单备份脚本”：
    
    每次运行就把某个目录打包成 backup_日期.tar.gz
    

  

> 完成标志：

> 遇到“每天都要重复做的事情”，你会自然想到：

> “我写个脚本吧”。

---

### **第 9 阶段：综合实践（长期）**

  

你后面还要学 ROS、嵌入式，所以可以选一些**贴近自己目标**的小项目，比如：

1. **搭建一个开发环境**
    
    - 在 Ubuntu 里：
        
        - 用 apt 安装 build-essential、cmake、python3-pip 等
            
        - 装好 VS Code / Neovim
            
        
    - 写文档记录“从裸机到可开发”的完整步骤
        
    
2. **写一个系统信息小工具**
    
    - 一个 bash 脚本，输出：
        
        - 系统版本、CPU 信息、内存占用、磁盘占用、网络状态
            
        
    - 练习综合使用 uname、lscpu、free、df、ip、top 等命令
        
    
3. **为未来的 ROS 做准备**
    
    - 熟悉 apt 安装 ROS 的流程（先不深学 ROS 本身）
        
    - 在 Ubuntu 上创建工作空间、跑简单示例时，注意你用到了哪些 Linux 知识（权限、网络、服务等）
        
    

---

## **三、关于 Mac 终端 & Ubuntu 的配合**

  

结合你现在的环境，给一点具体建议：

- **在 Mac 终端练：**
    
    - 基本命令：ls、cd、cp、mv、rm、grep、find、cat、less
        
    - shell 脚本语法（bash 在 Mac 也有）
        
    
- **在 Ubuntu VM 里练：**
    
    - apt 包管理
        
    - systemctl 服务管理
        
    - 安装开发环境、搭服务
        
    - 后面与 ROS 相关的一切东西
        
    

  

可以给自己定一个小目标：

**平时用 Mac 做日常事时，尽量少用 Finder，多用终端操作文件。**

很快你就会发现，Linux 命令行其实也就那回事，只是最开始不习惯。

---

如果你愿意，我可以按“每天学什么 + 做什么练习”帮你排一个**28 天 Linux 入门打卡计划**，直接照着完成就能达到“比较熟悉”的水平。