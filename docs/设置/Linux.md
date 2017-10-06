# 在Linux上使用VS Code

[原文](https://code.visualstudio.com/docs/setup/linux)

## 安装

### Debian和Ubuntu的发行版

Debian/Ubuntu的发行版最容易的安装方法是通过软件中心或命令行[下载](https://go.microsoft.com/fwlink/?LinkID=760868)并安装：

```bash
sudo dpkg -i <file>.deb
sudo apt-get install -f # 安装依赖
```

安装.deb包将自动安装apt库和签名密钥，以使用常规系统机制启用自动更新。请注意，[下载页面](https://code.visualstudio.com/Download)上也提供了32位和.tar.gz的二进制文件。

库和密钥也可以使用以下脚本手动安装：

```bash
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'
```

然后更新软件包缓存并使用以下命令安装软件包：

```bash
sudo apt-get update
sudo apt-get install code # 或者 code-insiders
```

### RHEL，Fedora和CentOS的发行版

我们目前在yum库中提供稳定的64位VS Code，以下脚本将安装密钥和库：

```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
```

然后更新包缓存并使用`dnf`（Fedora 22及以上版本）安装包：

```bash
dnf check-update
sudo dnf install code
```

旧版本使用 `yum`:

```bash
yum check-update
sudo yum install code
```

### openSUSE和SLE的发行版

上面的yum库也适用于基于openSUSE和SLE的系统，以下脚本将安装密钥和库：

```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ntype=rpm-md\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/zypp/repos.d/vscode.repo'
```

然后更新软件包缓存并使用以下命令安装软件包：

```bash
sudo zypper refresh
sudo zypper install code
```

### Arch Linux的AUR包

一个社区维护Arch用户库（AUR）[VS Code包](https://aur.archlinux.org/packages/visual-studio-code)

### 手动安装.rpm包 

.[rpm包（64位）](https://go.microsoft.com/fwlink/?LinkID=760867)也可以手动下载安装，但是如果没有安装上面的库，自动更新将无法正常工作。下载完之后可以使用你的包管理器安装，比如`dnf`：

```bash
sudo dnf install <file>.rpm
```

请注意，[下载页面](https://code.visualstudio.com/Download)上也提供了32位和.tar.gz的二进制文件

## 更新

VS Code每月更新一次，您可以通过检查[更新](https://code.visualstudio.com/updates)来查看新版本是否可用。如果VS Code库被正确安装，那么你的系统软件包管理器应该以与系统上其他软件包相同的方式自动处理软件更新。

## Node.js

Node.js是一个流行的平台和运行时，用于轻松构建和运行JavaScript应用程序。它还包括Node.js模块的包管理器[NPM](https://www.npmjs.com/)。你将在我们的文档中经常看到Node.js和NPM，并且一些可选的VS代码工具需要Node.js（例如，VS Code [扩展生成器](https://code.visualstudio.com/docs/extensions/yocode)）

如果您想在Linux上安装Node.js，请参考[通过软件包管理器安装Node.js](（https://nodejs.org/en/download/package-manager)来查找Node.js软件包和适合你的Linux发行版的安装说明。

要了解有关JavaScript和Node.js的更多信息，请参考我们的[Node.js教程](https://code.visualstudio.com/docs/nodejs/nodejs-tutoria)，您将学到如何使用VS Code运行和调试Node.js应用程序。

## 设置VS Code为默认编辑器

### xdg-open

您可以使用以下命令为`xdg-open`使用的文本文件（`text/plain`）设置默认文本编辑器：

```bash
xdg-mime default code.desktop text/plain
```

### Debian发行版

Debian的发行版允许使用[替代系统](https://wiki.debian.org/DebianAlternatives)设置默认*编辑器*，而不用担心mime类型。您可以通过运行以下命令并选择VS Code作为默认编辑器。

```bash
sudo update-alternatives --set editor /usr/bin/code
```

## 接下来

一旦安装了VS Code，这些主题将帮助你了解更多VS Code的信息：

* [附加组件](https://code.visualstudio.com/docs/setup/additional-components) - 了解如何安装Git，Node.js，TypeScript和Yeoman等工具。
* [用户界面](https://code.visualstudio.com/docs/getstarted/userinterface) - VS Code界面快速指南。
* [用户/工作区设置](https://code.visualstudio.com/docs/getstarted/settings) - 了解如何通过设置配置你的VS Code首选项。

## 常见问题

### Azure VM 问题

遇到”运行没有SUID的沙箱“的错误？

您可以安全放心地忽略此错误。

### Debian和移动文件到垃圾桶

如果在Debian操作系统上从VS Code中删除文件时出现错误，可能是因为VS Code使用的垃圾实现不存在。

运行这些命令来解决这个问题：

```bash
sudo apt-get install gvfs-bin
```

### ENOSPC 错误

当您看到此错误时，它表示VS Code文件监视器用完了句柄。通过运行一下命令可以查看当前限制：

```bash
cat /proc/sys/fs/inotify/max_user_watches
```

通过编辑`/etc/sysctl.conf`并将这一行添加到文件的末尾可以将限制增加到最大值：

```bash
fs.inotify.max_user_watches=524288
```

然后可以通过运行`sudo sysctl -p`来加载新值。 请注意，[Arch Linux](https://www.archlinux.org/)的工作方式略有不同，[查看此页面以获取建议](https://github.com/guard/listen/wiki/Increasing-the-amount-of-inotify-watchers)。

虽然524288是可以监视的文件的最大数量，但如果您处于特殊的内存限制的环境中，则可能希望降低数量。每个文件监视[占用540字节（32位）或〜1kB（64位）](https://stackoverflow.com/a/7091897/1156119)，所以假设所有524288监视都被使用，导致一个大约256MB（32位）或512MB（64位）的上限。

### 在Ubuntu中看不到汉字

我们正在努力解决问题。在此期间，打开应用程序菜单，然后选择**文件**> **首选项**> **设置**。然后设置`editor.fontFamily`，显示：

```json
    "editor.fontFamily": "Droid Sans Mono, Droid Sans Fallback"
```

### git未安装

安装过程中可能会出现此错误，通常是由于软件包管理器过期而导致的。 尝试更新并重新安装：

```bash
# 对于 .deb
sudo apt-get update

# 对于.rpm（Fedora 21及更低版本）
sudo yum update

# 对于.rpm（Fedora 22及以上版本）
sudo dnf update
```

### VS Code 的code命令不会将窗口显示在Ubuntu的前台

当VS Code已经在当前目录打开，在Ubuntu上运行`code .`时，VS Code不会显示在前台。这是一个系统功能，可以使用`ccsm`禁用。

```bash
# 安装
sudo apt-get update
sudo apt-get install compizconfig-settings-manager

# 运行
ccsm
```

在**一般**> **常规选项**> **焦点和提升行为**下，将“焦点防范等级”设置为“关”。记住这是一个适用于所有应用程序的操作系统级设置，而不仅仅适用于VS代码。

### *注：翻译中的链接现在还是英文文档，当翻译到相关文章时，我会进行替换。最后全部翻译完成时，就不再有这种情况发生，到时大家可以到github上查看完整文档，现在还请大家多多谅解。*

## **What you want, Go after It.**