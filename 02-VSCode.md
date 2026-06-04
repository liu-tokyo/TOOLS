# Visual Code

## 安装

下载安装，或者用如下指令安装：

```
winget install Microsoft.VisualStudioCode
```



## 1. 汉字黄色标记

- 点击左侧小齿轮（管理）；
- 点击弹出菜单中的 `Settings（设置）`；  
  下面的 3 项设置依然比较复杂，直接检索 `nonBasicASCII` 立马就可以看到选项。
- 在上方搜索框中搜索 `quick`；
- 搜索结果中点击 `Edit in settings.json`；
- 加上下图中红框标记的配置 `"editor.unicodeHighlight.nonBasicASCII": false`；

## 2. 鼠标右键显示

　发现，如果是 `winget` 安装的话，因为没有设置画面，所以不会出现在鼠标右键的菜单中。  
- 需要设置如下 3 项的 注册表：

  | 注册表项目                                            | 说明             | 备注 |
  | ----------------------------------------------------- | ---------------- | ---- |
  | `HKEY_CLASSES_ROOT\*\shell\VSCode`                    | 点击文件         |      |
  | `HKEY_CLASSES_ROOT\Directory\Background\shell\VSCode` | 文件夹的空白位置 |      |
  | `HKEY_CLASSES_ROOT\Directory\shell\vscode`            | 点击文件夹       |      |

具体设置办法，可以参照其它电脑的注册表的情况，并不复杂。



# 如何使用 SSH 工具

在 VS Code 中使用 SSH 工具，主要是通过微软官方提供的 **Remote - SSH** 扩展插件来实现的。它可以让你直接在本地的 VS Code 界面里，像修改本地文件一样，流畅地编辑和调试远程 Linux 服务器（比如你的 Ubuntu 宿主机、云服务器或虚拟机）上的代码。

整个配置和连接过程非常简单，主要分为以下几个步骤：

## 第一步：准备工作（确保服务器开启 SSH）

在连接之前，请确保你的远程服务器已经安装并开启了 SSH 服务。

以 Ubuntu/Linux 为例，可以通过以下命令检查和安装：

Bash

```
# 更新源并安装 openssh-service（如果尚未安装）
sudo apt update
sudo apt install openssh-server -y

# 检查 SSH 运行状态（应该显示 active/running）
sudo systemctl status ssh
```

*同时，请记录下远程服务器的 **IP 地址** 以及你的 **用户名** 和 **密码**。*

## 第二步：在 VS Code 中安装插件

1. 打开本地的 VS Code。
2. 点击左侧工具栏的 **Extensions（扩展）** 图标（或者按快捷键 `Ctrl + Shift + X`）。
3. 在搜索框中输入 `Remote - SSH`。
4. 找到由 **Microsoft** 官方发布的插件，点击 **Install（安装）**。

安装完成后，VS Code 的左下角会多出一个**绿色的“><”小图标（远程窗口按钮）**，左侧工具栏也会多出一个远程资源管理器（Remote Explorer）的图标。

## 第三步：添加并连接远程服务器

有两种连接方式，这里介绍最直观的“密码连接方式”：

### 1. 快捷连接

1. 点击 VS Code 左下角的绿色 **`><`** 图标，或者按 `F1` 键打开命令面板。
2. 在顶部弹出的输入框中选择 **Connect to Host... (连接到主机...)**。
3. 选择 **Add New SSH Host... (添加新的 SSH 主机...)**。
4. 输入你的 SSH 连接命令，格式为：`ssh 用户名@服务器IP`
   - *例如：`ssh ubuntu@192.168.1.100`*
5. 按回车确认，接着系统会让你选择一个配置文件来保存这个连接信息（通常选择默认的第一个 `C:\Users\用户名\.ssh\config` 即可）。

### 2. 发起连接

1. 再次点击左下角的绿色 **`><`** 图标，选择 **Connect to Host...**。
2. 这时就能看到你刚才添加的服务器 IP，点击它。
3. VS Code 会弹出一个新窗口。首次连接时，顶部会提示 `Are you sure you want to continue?`，选择 **Continue (继续)**。
4. 随后在顶部输入框中输入你远程服务器的 **登录密码**，回车。

**成功标志：** 当看到新窗口左下角变成绿色并显示 `SSH: 192.168.1.100`（你的服务器IP）时，说明你已经成功“潜入”了远程服务器！

## 第四步：像本地一样开发

连接成功后，你可以在这个 VS Code 窗口里做任何事情：

- **打开代码目录：** 点击左侧的“资源管理器” $\rightarrow$ 点击 **Open Folder（打开文件夹）**，你会直接看到远程服务器的目录树，选定你的代码文件夹（如 `/home/ubuntu/projects`）点击确定，再次输入密码即可打开。
- **使用远程终端：** 快捷键 `Ctrl + ~` 打开终端，这个终端就是远程服务器的 Bash，你运行的任何命令（如 `python`、`git status`、`docker ps`）都是直接在服务器上执行。

## 💡 进阶小贴士：免密登录（强烈推荐）

每次打开或者切换目录都要输密码会非常麻烦。你可以配置 **SSH 密钥对** 实现免密秒连：

### 1. 在本地电脑生成密钥（如果已有请跳过）

打开本地电脑的 PowerShell 或 CMD，运行：

Bash

```
ssh-keygen -t rsa -b 4096
```

一路连按回车（不要输入密码短语）。这会在你的本地电脑 `~/.ssh/` 目录下生成 `id_rsa`（私钥）和 `id_rsa.pub`（公钥）。

### 2. 把公钥拷贝到远程服务器

**最简单的方法：** 在本地命令行运行（将用户名和 IP 换成你的）：

Bash

```
ssh-copy-id 用户名@服务器IP
```

*（如果 Windows 提示没有 `ssh-copy-id` 命令，你可以手动用记事本打开本地的 `id_rsa.pub`，复制里面全部内容，粘贴到远程服务器的 `~/.ssh/authorized_keys` 文件中最后一行即可）。*

搞定免密登录后，以后在 VS Code 里点击连接，连密码都不用输，一秒就能直接进入开发状态。
