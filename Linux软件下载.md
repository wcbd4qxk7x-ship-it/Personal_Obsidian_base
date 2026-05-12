| **特性**   | **apt (Advanced Package Tool)** | **dpkg (Debian Package)** |
| -------- | ------------------------------- | ------------------------- |
| **层级**   | 高级前端工具                          | 底层后端工具                    |
| **依赖处理** | **自动解决**（最强优势）                  | **不解决**（若缺依赖则报错）          |
| **软件来源** | 远程仓库（互联网软件源）                    | 本地文件（硬盘上的 `.deb` 包）       |
| **主要用途** | 日常安装、更新、系统升级                    | 安装手动下载的包、查询系统底层信息         |
| **底层逻辑** | 调用 `dpkg` 来执行实际操作               | 直接操作文件系统                  |
### `apt` 的常用指令 (日常推荐)

`apt` 是 `apt-get` 的现代简化版，更适合人类阅读和使用。除非你是写脚本，否则推荐日常直接用 `apt`。

#### 基本操作

- **更新软件列表（去服务器问问有没有新货）：**
    
    Bash
    
    ```
    sudo apt update
    ```
    
- **升级所有已安装的软件（把旧货换成新货）：**
    
    Bash
    
    ```
    sudo apt upgrade
    ```
    
- **安装软件（自动解决依赖）：**
    
    Bash
    
    ```
    sudo apt install <软件名>
    # 例如: sudo apt install git
    ```
    
- **卸载软件（保留配置文件）：**
    
    Bash
    
    ```
    sudo apt remove <软件名>
    ```
    
- **彻底卸载（删除软件和配置文件）：**
    
    Bash
    
    ```
    sudo apt purge <软件名>
    ```
    

#### 查询与清理

- **搜索软件：**
    
    Bash
    
    ```
    apt search <关键词>
    ```
    
- **查看软件详细信息：**
    
    Bash
    
    ```
    apt show <软件名>
    ```
    
- **清理不再需要的依赖包（自动清理垃圾）：**
    
    Bash
    
    ```
    sudo apt autoremove
    ```
### `dpkg` 的常用指令 (特定场景)

通常你只有在**从网页手动下载了某个 `.deb` 文件**（例如下载 Chrome 或 VS Code 的安装包），或者需要调试系统时，才会用到 `dpkg`。

#### 安装与卸载

- **安装本地的 `.deb` 文件：**
    
    Bash
    
    ```
    sudo dpkg -i <文件名.deb>
    # i = install
    ```
    
    > **注意：** 如果安装报错提示 "dependency problems"（依赖缺失），你需要紧接着运行 `sudo apt --fix-broken install` 来让 apt 帮你补齐缺少的依赖。
    
- **卸载软件：**
    
    Bash
    
    ```
    sudo dpkg -r <软件名>
    # r = remove
    ```
    

#### 强大的查询功能 (dpkg 的强项)

- **列出系统内所有已安装的包：**
    
    Bash
    
    ```
    dpkg -l
    # 通常配合 grep 使用，例如: dpkg -l | grep mysql
    ```
    
- **查询某个软件把文件都装到哪里去了：**
    
    Bash
    
    ```
    dpkg -L <软件名>
    # L = List files
    ```
    
- **反向查询：查看某个文件属于哪个软件包：**
    
    Bash
    
    ```
    dpkg -S <文件路径>
    # 例如: dpkg -S /bin/ls 会告诉你这个文件属于 coreutils 包
    ```