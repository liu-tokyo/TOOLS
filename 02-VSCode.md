# Visual Code

## 1. 汉字黄色标记

- 点击左侧小齿轮（管理）；
- 点击弹出菜单中的Settings（设置）；  
  下面的 3 项设置依然比较复杂，直接检索 `nonBasicASCII` 立马就可以看到选项。
- 在上方搜索框中搜索“quick”；
- 搜索结果中点击“Edit in settings.json”；
- 加上下图中红框标记的配置“"editor.unicodeHighlight.nonBasicASCII": false”；

## 2. 鼠标右键显示

　发现，如果是 `winget` 安装的话，因为没有设置画面，所以不会出现在鼠标右键的菜单中。  
- 需要设置如下 3 项的 注册表：

  | 注册表项目                                            | 说明             | 备注 |
  | ----------------------------------------------------- | ---------------- | ---- |
  | `HKEY_CLASSES_ROOT\*\shell\VSCode`                    | 点击文件         |      |
  | `HKEY_CLASSES_ROOT\Directory\Background\shell\VSCode` | 文件夹的空白位置 |      |
  | `HKEY_CLASSES_ROOT\Directory\shell\vscode`            | 点击文件夹       |      |

具体设置办法，可以参照其它电脑的注册表的情况，并不复杂。
