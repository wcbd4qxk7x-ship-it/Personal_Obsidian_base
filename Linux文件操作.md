---
title: Linux 文件操作命令行总结
tags:
  - Linux
  - 命令行
  - 文件操作
---

# Linux 文件操作命令行总结

> [!info] 说明
> 本笔记适合放在 Obsidian 里作为速查。  
> 大部分命令在 **Linux / macOS 终端** 都通用。

---

## 一、路径与目录基础

- **绝对路径**：从根目录 `/` 开始  
  - 例：`/home/user/Documents`
- **相对路径**：相对于当前目录
  - `.`：当前目录  
  - `..`：上一级目录  
  - `~`：当前用户的 home 目录（例如 `/home/user` 或 `/Users/user`）

常见写法例子：

```
cd ~/projects        # 进入 home 下的 projects
cd ../..            # 回到上两级目录
```

## **二、查看当前位置：pwd 
```
pwd
```

## **三、查看文件与目录：**

```
ls              # 列出当前目录
ls dir_name     # 列出指定目录
```

## **四、切换目录：**
```
cd /path/to/dir     # 进入指定目录（绝对路径）
cd dir_name         # 进入子目录（相对路径）
cd ..               # 返回上一级目录
cd ~                # 回到 home 目录
cd                  # 直接输入 cd 也表示回 home
```

## **五、创建与删除目录：**
```
创建目录
mkdir test          # 创建 test 目录
mkdir -p a/b/c      # 递归创建多级目录

删除空目录
rmdir empty_dir     # 只能删除**空目录**

删除非空目录
rm -r dir_name      # 递归删除目录及其内容（危险）
rm -rf dir_name     # 强制删除，不提示（非常危险）

> [!warning] 高危操作

> rm -rf / / rm -rf * 等命令可能直接删光系统文件，

> 一定要**仔细确认路径**再回车。
```

## **六、创建 / 查看文件：**
```
创建空文件
touch file.txt          # 创建一个空文件（或更新文件时间）
touch a.py b.py c.py    # 同时创建多个文件
直接输出文件内容
cat file.txt            # 一次性输出全部内容（适合小文件）
分页查看
less file.txt
# 操作：
# 空格 / PgDn：向下翻页
# b / PgUp：向上翻页
# q：退出
只看开头/结尾
head file.txt       # 默认显示前 10 行
head -n 20 file.txt # 显示前 20 行

tail file.txt       # 默认显示最后 10 行
tail -n 20 file.txt # 显示最后 20 行
tail -f file.txt    # 实时追踪文件（日志常用）
```
## **七、复制、移动与重命名：**

```
复制
cp a.txt b.txt          # 复制文件：a.txt → b.txt
cp a.txt dir/           # 把 a.txt 复制到目录 dir 下
cp -r src_dir dst_dir   # 递归复制目录

常用选项：

- -r：递归复制目录
    
- -i：覆盖前询问（安全一点）
    
- -v：显示复制过程（verbose）
移动/重命名
mv a.txt b.txt          # 重命名：a.txt → b.txt
mv a.txt dir/           # 移动文件到 dir 目录
mv dir1 dir2/           # 移动目录

同样可以加：

- -i：覆盖前询问
    
- -v：显示过程
    


> [!tip] 重命名和移动的本质

> mv 不区分“移动”还是“重命名”，

> 目标是**目录**就是移动，目标是**新文件名**就是重命名
```
## **八、删除文件：**

```
删除文件
rm file.txt         # 删除单个文件
rm file1 file2      # 删除多个文件
rm *.log            # 删除当前目录下所有 .log 文件
rm -i file.txt      # 删除前询问（安全一点）
删除目录
rm -r dir_name      # 删除目录及其内容
rm -rf dir_name     # 强制删除（危险）
```

## **九、查找文件：**
```
# 在当前目录及子目录中按文件名查找
find . -name "file.txt"

# 查找所有以 .py 结尾的文件
find . -name "*.py"

# 只查找目录
find . -type d -name "test"
```

## **十、查看权限与修改权限：**
```
查看权限：
ls -l
典型输出类似：
-rwxr-xr--  1 user group  1234 Nov 22 10:00 script.sh
- 第 1 列：-rwxr-xr--
    
    - 第 1 个字符：文件类型（- 普通文件，d 目录）
        
    - 后面 9 个字符：每 3 个一组，分别是：
        
        - 所有者（user）
            
        - 所在组（group）
            
        - 其他人（others）
            
        
    - r：可读，w：可写，x：可执行
修改权限
- r = 4，w = 2，x = 1
    
- 三位数字分别对应 **所有者 / 组 / 其他人**
chmod 755 script.sh   # 所有者：rwx，组：r-x，其他：r-x
chmod 644 file.txt    # 所有者：rw-，组：r--，其他：r--
chmod +x script.sh    # 给所有人加上可执行权限
```

## **十一、一些常见场景示例**

```
mkdir -p ~/projects/demo
cd ~/projects/demo
touch main.py README.md
ls -al

cd ~/projects
ls
rm -ri demo       # 递归删除并且每步询问

cp ~/.bashrc ~/.bashrc.backup

mkdir pics
mv *.jpg pics/        # 将当前目录所有 jpg 移动到 pics
```

## **十二、命令小抄（可贴墙）**

```
pwd                    # 显示当前路径
ls / ls -al            # 查看文件和目录
cd / cd .. / cd ~      # 切换目录
mkdir / mkdir -p       # 创建目录
rmdir / rm -r          # 删除目录（空 / 非空）
touch                  # 创建空文件
cat / less / head / tail   # 查看文件内容
cp / cp -r             # 复制文件 / 目录
mv                     # 移动 / 重命名
rm / rm -r / rm -rf    # 删除文件 / 目录
find . -name "*.py"    # 按名字查找文件
ls -l / chmod          # 查看 / 修改权限


> [!summary] 记住一条核心思路

> **所有操作都是“对路径动手”**：

> 想清楚“当前在哪、要去哪里、对哪一个路径做什么”，

> 再敲命令，出错率会低很多。
```

