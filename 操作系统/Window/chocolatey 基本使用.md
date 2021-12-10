## 介绍

Chocolatey 是一款专门为Windows系统开发的、基于NuGet的包管理器工具，类似于Node.js 的npm，MacOS 的 brew，Ubuntu的apt-get，简称choco。

官方网址：https://chocolatey.org



## 安装&卸载

### 安装

cmd 窗口以管理员身份运行，执行以下命令：

~~~shell
@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
~~~

验证

~~~shell
choco -v
~~~

## 常用命令

~~~shell
# 查看版本
choco -v
# 帮助
choco -?
# 搜索包
choco search pandoc
# 列出本地已安装的包
choco list --local-only
# 列出系统已安装的软件
choco list -li
# 安装
choco install <pkg-name> 
# 卸载
choco uninstall <pkg-name>
~~~

### choco install

自定义安装目录

~~~shell
choco install pandoc --install-directory="D:/Software"
~~~

