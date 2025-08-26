# VS Code 教程
   VSCode（全称：Visual Studio Code）是一款由微软开发且跨平台的免费源代码编辑器。该软件支持语法高亮、代码自动补全（又称 IntelliSense）、代码重构、查看定义功能，并且内置了命令行工具和 Git 版本控制系统。用户可以更改主题和键盘快捷方式实现个性化设置，也可以通过内置的扩展程序商店安装扩展以拓展软件功能。
VS Code 使用 Monaco Editor 作为其底层的代码编辑器。Visual Studio Code 被认为是最受开发者欢迎的开发环境。
***
*以下简称 Code*
***
## 安装
* **VS code 下载安装** 
   1. 下载地址 https://code.visualstudio.com/
   2. 直接安装即可
   2. 打开Code，在Extensions中安装C/C++、Cmake、CMake Tools这三个插件
<br/><br/>
* **MinGW-64 编译器下载安装**
   1. 下载地址 https://sourceforge.net/projects/mingw-w64/files/mingw-w64/mingw-w64-release/
   2. 解压后将mingw-64文件下的bin目录添加到环境变量Path中
   3. 打开Windows的PowerShell，输入g++，查看是否安装成功 
<br/><br/>
* **CMake下载安装**
   1. 下载地址 https://cmake.org/
   2. 解压后将cmake文件下的bin目录添加到环境变量Path中
   3. 打开Windows的PowerShell，输入cmake，查看是否安装成功 
***

## g++命令
* g++ -g ./my1.cpp ./my2.cpp -o my.exe
   * -g 生成可调式的exe文件（不带-g生成不可调试的exe）
   * -o 指定exe文件名（不指定的话默认为a.exe）

**改天再写。。。**:joy:
