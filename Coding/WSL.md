# **Windows下WSL+Ubuntu环境配置**
适用于 Linux 的 Windows 子系统WSL（Windows Subsystem for Linux）是 Windows 的一项功能，可用于在 Windows 计算机上运行 Linux 环境，而无需单独的虚拟机或双重启动。 WSL 旨在为想要同时使用 Windows 和 Linux 的开发人员提供无缝高效的体验。
## 安装WSL
1. 安装wsl2之前，首先要配置系统设置，在“控制面板”>“程序”>“程序和功能”>“启用或关闭Windows功能”，勾选“适用于Linux的Windows子系统”和“虚拟机平台”；
2. 重启计算机以生效；
3. 打开cmd或powershell，在命令行中输入如下命令<br>
`wsl --install`

## Ubuntu系统安装及配置
1. 在Microsoft Store中下载ubuntu
2. 下载完成后打开Ubuntu，需要配置用户名称和密码
3. 如果C盘不够用，可以迁移到D盘，powershell下运行以下命令
```
# 导出
wsl --export Ubuntu-22.04 "D:\linux\Ubuntu-22.04\export.tar"
# 注销
wsl --unregister Ubuntu-22.04
# 导入
wsl --import Ubuntu-22.04 "D:\linux\Ubuntu-22.04" "D:\linux\Ubuntu-22.04\export.tar" --version 2
# 从root转为XXX（你设置的用户名）
Ubuntu2204 config --default-user XXX
```
## WSL2的常用命令
```
wsl  //进入子系统
exit  //退出子系统或者使用ctrl+d
wsl -l -o  //列出可用的 Linux 发行版
wsl -l -s  //列出已安装的发行版
wsl --set-default-version <Version>  //设置wsl的默认版本，<Version>可替换为数字 1 或 2。 例如wsl --set-default-version 2。
wsl --status  //检查 WSL 状态
wsl --shutdown   //关闭WSL
wsl --version  //检查 WSL 版本
wsl -l -v  //查看已经安装的发行版
wsl --unregister <DistributionName>  //<DistributionName>为要注销的发行版名称
```
## VScode连接Linux子系统
1. 更新ubuntu子系统，powershell输入wsl命令进入子系统，输入以下命令更新
```
sudo apt-get update
```
2. VScode搜索WSL并安装
3. 重启计算机

## WSL使用
1. 点击VScode左下角，选择“Connect to WSL”
2. 选择文件或目录，开始使用;
3. 新建 Terminal，使用命令行执行指令。