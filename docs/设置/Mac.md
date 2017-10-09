# 在Mac上使用VS Code

[原文](https://code.visualstudio.com/docs/setup/mac)

## 安装

1. [下载 Visual Studio Code](https://go.microsoft.com/fwlink/?LinkID=534106)。
2. 双击解压下载好的文件包
3. 拖动 `Visual Studio Code.app` 到 `Applications` 文件夹，使其在 `Launchpad` 中可用。
4. 通过右键单击图标并选择 `选项`, `添加到dock` 将VS Code添加到Dock。

### 命令行

你也可以在将 VS Code 添加到环境变量之后，通过在终端中输入 'code' 打开VS Code：

- 启动 VS Code。
- 打开 **Command Palette** (`kb(workbench.action.showCommands)`) 并且输入 'shell command' 查找 **Shell Command: Install 'code' command in PATH** 命令。

![Mac shell 命令](https://code.visualstudio.com/images/mac_shell-command.png)

- 重新启动终端以使新的 `$PATH` 值生效。你也可以在任何文件夹中输入 'code .' 开始编辑该文件夹中的文件。

>**注意:** 如果在 `.bash_profile` （或等效文件）中还存在之前VS Code版本中老的 `code` 别名，请删除并通过命令 **Shell Command: Install 'code' command in PATH** 替换它。

手动添加 VS Code 到环境变量中：

```bash
cat << EOF >> ~/.bash_profile
# Add Visual Studio Code (code)
export PATH="$PATH:/Applications/Visual Studio Code.app/Contents/Resources/app/bin"
EOF
```

## 更新

VS Code 每月[发布](https://code.visualstudio.com/updates)一次，当更新可用时支持自动更新。如果 VS Code 提示你更新，接受之后，它会完成更新（你不需要做其它任何事情）。如果你更喜欢手动更新，请参考 [如何停用自动更新](https://code.visualstudio.com/docs/supporting/faq#_how-do-i-opt-out-of-vs-code-autoupdates).

## 首选项菜单

你可以通过[设置](https://code.visualstudio.com/docs/getstarted/settings)、[颜色主题](https://code.visualstudio.com/docs/getstarted/themes)和[自定义按键映射](https://code.visualstudio.com/docs/getstarted/keybindings)来配置 VS Code，并且你将在我们的文档中经常看到 **文件** > **首选项** 菜单祖的提示， 在 Mac 上，**首选项** 菜单祖 在 **代码** 下面,而不是 **文件**下面。


## 接下来

一旦你安装了 VS Code，这些主题能帮助你更好地理解 VS Code：

* [附加组件](https://code.visualstudio.com/docs/setup/additional-components) - 了解如何安装Git，Node.js，TypeScript和Yeoman等工具。
* [用户界面](https://code.visualstudio.com/docs/getstarted/userinterface) - VS Code界面快速指南。
* [用户/工作区设置](https://code.visualstudio.com/docs/getstarted/settings) - 了解如何通过设置配置你的VS Code首选项。

## 常见问题

### Mono 和 El Capitan

安装 OS X 10.11 El Capitan 公共测试版后，Mono 停止在 Visual Studio code中工作。我该怎么办？

运行一下命令：

```bash
brew update
brew reinstall mono
```

### *注：翻译中的链接现在还是英文文档，当翻译到相关文章时，我会进行替换。最后全部翻译完成时，就不再有这种情况发生，到时大家可以到github上查看完整文档，现在还请大家多多谅解。*

## **What you want, Go after It.**