# Linux
## Linux目录结构
![Linux目录](pic/Linux/linux_catalog.png)
*在linux中根目录的子目录结构相对是固定的(名字固定), 不同的目录功能是也是固定的*
* bin: binary, 二进制文件目录, 存储了可执行程序, 今天要将的命令对应的可执行程序都在这个目录中
* sbin: super binary, root用户使用的一些二进制可执行程序
* etc: 配置文件目录, 系统的或者用户自己安装的应用程序的配置文件都存储在这个目录中
* lib: library, 存储了一些动态库和静态库，给系统或者安装的软件使用
* media: 挂载目录, 挂载外部设备，比如: 光驱, 扫描仪
* mnt: 临时挂载目录, 比如我们可以将U盘临时挂载到这个目录下
* proc: 内存使用的一个映射目录, 给操作系统使用的
* tmp: 临时目录, 存放临时数据, 重启电脑数据就被自动删除了
* boot: 存储了开机相关的设置
* home: 存储了普通用户的家目录，家目录名和用户名相同
* root: root用户的家目录
* dev: device，设备目录，Linux中一切皆文件, 所有的硬件会抽象成文件存储起来，如：键盘，鼠标
* lost+found: 一般时候是空的, 电脑异常关闭/崩溃时用来存储这些无家可归的文件, 用于用户系统恢复
* opt: 第三方软件的安装目录
* var: 存储了系统使用的一些经常会发生变化的文件， 比如：日志文件
* usr: unix system resource, 系统的资源目录
  - /usr/bin: 可执行的二进制应用程序
  - /usr/games: 游戏目录
  - /usr/include: 包含的标准头文件目录
  - /usr/local: 和opt目录作用相同, 安装第三方软件
## 命令行
* 环境变量PATH
```bash
# 通过 echo 命令可以查看环境变量 PATH 中的值, 在shell中变量名前加 $ 就是取值
# $:普通用户 #:root用户
xrhu@xrhu:~$ echo $PATH
```
* 快捷键
    - Tab 命令自动补全，如果有多个候补再按一次Tab
    - ↑/↓ 显示输入的上/下一个历史命名
## 用户管理
* \\
## 文件管理
* touch 创建一个新文件
* ls -a：显示全部文件，包括隐藏文件（文件名前加. 如 .a.txt）
* ls -l: 以列表形式显示文件的详细信息
![file info](pic/Linux/file_info.png)
* 创建/删除文件目录
  - mkdir 创建目录，-p 删除多层目录<br>
    ` mkdir parent/child/baby1/baby2 -p`
  - rm 删除目录，-r 递归删除子目录 -f 强制删除<br>
    `rm file_name -rf`
* 复制/移动
    - cp 拷贝，-r 如果拷贝到的目录不存在则创建该目录
    - mv 移动/重命名
* 软/硬链接（相当于快捷方式，软连接一般用于目录，硬链接只用于文件）
  - ln -s 源文件路径 软链接文件的名字(可以带路径)
  - ln 源文件 硬链接文件的名字(可以带路径)
  ```bash
  # WSL下在Linux home目录下创建一个windows DeskTop的软链接
  xrhu@xrhu:~$ ln -s /mnt/c/Users/xrhu/Desktop WindowsDesktop
  ```
* 查看文件内容
  - cat 将文件内容显示到终端(适合小文件)
  - more 比cat要高级一点, 可以翻屏查看文件中的内容
    - 回车: 显示下一行
    - 空格: 向下滚动一屏
    - b: 返回上一屏
    - q: 退出more
  - less 比more更好用一些，可用上下键滚动查看
    - b: 向上翻页
    - 空格: 向后翻页
    - 回车: 显示下一行
    - 上下键: 上下滚动
    - q:退出
* 输出重定向
  - \>: 将文件内容写入到指定文件中, 如果文件中已有数据, 则会使用新数据覆盖原数据
  - \>>: 将输出的内容追加到指定的文件尾部
  ```bash
  # 将当前日期覆盖式写入test.txt文件中，若没有该文件则会自动创建该文件
  xrhu@xrhu:~$ date > test.txt
  xrhu@xrhu:~$ cat test.txt
  Tue Sep  9 11:18:41 CST 2025
  # 将当前日期追加到test.txt文件中
  xrhu@xrhu:~$ date >> test.txt
  xrhu@xrhu:~$ cat test.txt
  Tue Sep  9 11:18:41 CST 2025
  Tue Sep  9 11:20:27 CST 2025
  ```
## 解压缩文件
*Linux自带压缩工具gzip和bzip2, 但明显的缺点是不能打包压缩文件, 每个文件都会生成一个单独的压缩包, 并且压缩之后不会保留原文件。需要配合打包工具tar使用。使用tar进行压缩和解压缩的时候, 只需要指定相对用的参数, 在其内部就会调用对应的压缩工具gzip或者bzip2完成指定的操作。*
* 压缩文件：tar 参数 生成的压缩包的名字 要压缩的文件(文件或者目录)
    - tar文件压缩涉及的参数如下, 没有先后顺序
      - c: 创建压缩文件
      - z: 使用gzip的方式进行文件压缩
      - j: 使用bzip2的方式进行文件压缩
      - v: 压缩过程中显示压缩信息
      - f: 指定压缩包的名字
  - 生成的压缩包的名字, 建议使用标准后缀, 方便识别:
	- 压缩使用 gzip 方式,  标准后缀格式为: .tar.gz
	- 压缩使用 bzip2 方式, 标准后缀格式为: .tar.bz2
* 解压缩文件到当前目录：tar 参数 压缩包名<br>
  解压缩文件到指定目录：tar 参数 压缩包名 -C 解压目录
    - x: 释放压缩文件内容
    - z: 使用gzip的方式进行文件压缩, 压缩包后缀为.tar.gz
    - j: 使用bzip2的方式进行文件压缩, 压缩包后缀为.tar.bz2
    - v: 解压缩过程中显示解压缩信息
    - f: 指定压缩包的名字

## Linux指令大全

1. ls：列出当前目录中的文件和子目录<br>
`ls`
2. pwd：显示当前工作目录的路径<br>
`pwd`
3. cd：切换工作目录<br>
`cd /path/to/directory`
4. mkdir：创建新目录<br>
`mkdir directory_name`
5. rmdir：删除空目录<br>
`rmdir directory_name`
6. rm：删除文件或目录<br>
`rm file_name`<br>
`rm -r directory_name  # 递归删除目录及其内容`
7. cp：复制文件或目录<br>
`cp source_file destination`<br>
`cp -r source_directory destination  # 递归复制目录及其内容`
8. mv：移动或重命名文件或目录<br>
`mv old_name new_name`
9. touch：创建空文件或更新文件的时间戳<br>
`touch file_name`
10. cat：连接和显示文件内容<br>
`cat file_name`
11. more/less：逐页显示文本文件内容<br>
`more file_name`<br>
`less file_name`
12. head/tail：显示文件的前几行或后几行<br>
`head -n 10 file_name  # 显示文件的前10行`<br>
`tail -n 20 file_name  # 显示文件的后20行`
13. grep：在文件中搜索指定文本<br>
`grep search_term file_name`
14. ps：显示当前运行的进程<br>
`ps aux`
15. kill：终止进程<br>
`kill process_id`
16. ifconfig/ip：查看和配置网络接口信息<br>
`ifconfig`<br>
`ip addr show`
17. ping：测试与主机的连通性<br>
`ping host_name_or_ip`
18. wget/curl：从网络下载文件<br>
`wget URL`<br>
`curl -O URL`
19. chmod：修改文件或目录的权限<br>
`chmod permissions file_name`
20. chown：修改文件或目录的所有者<br>
`chown owner:group file_name`
21. tar：用于压缩和解压文件和目录<br>
`tar -czvf archive.tar.gz directory_name  # 压缩目录`<br>
`tar -xzvf archive.tar.gz  # 解压文件`
22. df/du：显示磁盘使用情况<br>
`df -h  # 显示磁盘空间使用情况`<br>
`du -h directory_name  # 显示目录的磁盘使用情况`
23. mount/umount：挂载和卸载文件系统<br>
`mount /dev/sdX1 /mnt  # 挂载分区到指定目录`<br>
`umount /mnt  # 卸载挂载的文件系统`
24. psql/mysql：用于与PostgreSQL或MySQL数据库交互的命令行工具<br>
`psql -U username -d database_name  # 连接到PostgreSQL数据库`<br>
`mysql -u username -p  # 连接到MySQL数据库`
25. top/htop：显示系统资源的实时使用情况和进程信息<br>
`top`<br>
`htop`
26. ssh：远程登录到其他计算机<br>
`ssh username@remote_host`
27. scp：安全地将文件从本地复制到远程主机，或从远程主机复制到本地<br>
`scp local_file remote_user@remote_host:/remote/directory`
28. find：在文件系统中查找文件和目录<br>
`find /path/to/search -name "file_pattern"`
29. grep：在文本中搜索匹配的行，并可以使用正则表达式进行高级搜索<br>
`grep -r "pattern" /path/to/search`
30. sed：流编辑器，用于文本处理和替换<br>
`sed 's/old_text/new_text/' file_name`
31. awk：用于文本处理和数据提取的文本处理工具<br>
`awk '{print $1}' file_name  # 提取文件中的第一列数据`
32. ssh-keygen：生成SSH密钥对，用于身份验证远程服务器<br>
`ssh-keygen -t rsa`
33. date：显示或设置系统日期和时间<br>
`date`
34. echo：将文本输出到标准输出<br>
`echo "Hello, World!"`
35. ln：创建硬链接或符号链接<br>
`ln source_file link_name  # 创建硬链接`<br>
`ln -s source_file link_name  # 创建符号链接`
36. uname：显示系统信息<br>
`uname -a`
37. shutdown/reboot：关闭或重新启动系统<br>
`shutdown -h now  # 立即关闭系统`<br>
`reboot  # 重新启动系统`
38. who/w：显示当前登录的用户信息<br>
`who`<br>
`w`
39. curl：用于与网络资源进行交互，支持各种协议<br>
`curl -X GET http://example.com`
40. zip/unzip：用于压缩和解压ZIP文件<br>
`zip archive.zip file1 file2  # 压缩文件`<br>
`unzip archive.zip  # 解压ZIP文件`
41. chmod/chown：修改文件或目录的权限和所有者<br>
`chmod permissions file_name  # 修改文件权限`<br>
`chown owner:group file_name  # 修改文件所有者`
42. useradd/userdel：用于添加和删除用户账户<br>
`useradd new_user  # 添加用户`<br>
`userdel username  # 删除用户`
43. passwd：更改用户密码<br>
`passwd username`
44. cron：定时任务管理器，用于自动执行计划任务<br>
`crontab -e  # 编辑用户的定时任务`
45. uptime：显示系统的运行时间和负载情况<br>
`uptime`
46. hostname：显示或设置计算机的主机名<br>
`hostname  # 显示主机名`
47. iptables/ufw：用于配置防火墙规则<br>
`iptables -A INPUT -p tcp --dport 80 -j ACCEPT  # 允许HTTP流量`<br>
`ufw enable  # 启用Uncomplicated Firewall`
48. netstat/ss：显示网络连接信息<br>
`netstat -tuln  # 显示所有TCP和UDP端口`<br>
`ss -tuln  # 使用Socket Stat查看网络连接`
49. ps/top/htop：显示进程信息和系统资源使用情况<br>
`ps aux  # 显示所有进程`<br>
`top  # 实时监视系统资源`<br>
`htop  # 更友好的进程监视器`
50. history：查看命令历史记录<br>
`history`
51. free：显示系统内存使用情况<br>
`free -m  # 以MB为单位显示内存使用情况`
52. lsblk/fdisk：查看磁盘分区信息和管理磁盘<br>
`lsblk  # 显示块设备信息`<br>
`fdisk /dev/sdX  # 打开磁盘分区工具`
53. nc：用于网络连接测试和数据传输<br>
`nc -vz host_name_or_ip port  # 测试主机的端口是否可达`
54. stat：显示文件或目录的详细信息<br>
`stat file_or_directory`
55. nmcli：用于管理网络连接的命令行工具<br>
`nmcli connection show  # 显示网络连接信息`
56. tailf：实时追踪文件的末尾，类似于tail -f<br>
`tailf file_name`
57. scp：安全地将文件从本地复制到远程主机，或从远程主机复制到本地<br>
`scp local_file remote_user@remote_host:/remote/directory  # 从本地到远程`<br>
`scp remote_user@remote_host:/remote/file local_directory  # 从远程到本地`
58. rsync：用于在本地和远程系统之间同步文件和目录<br>
`rsync -avz source_directory/ remote_user@remote_host:/remote/directory/`
59. dd：用于复制和转换文件<br>
`dd if=input_file of=output_file bs=block_size`
60. sudo：以超级用户权限运行命令<br>
`sudo command_to_run_as_superuser`
61. alias：为命令创建别名<br>
`alias ll='ls -alF'`
62. unalias：删除命令别名<br>
`unalias ll`
63. env：显示当前环境变量<br>
`env`
64. export：设置或导出环境变量<br>
`export PATH=$PATH:/new/path`
65. xargs：将标准输入转换为命令参数<br>
`cat files.txt | xargs rm  # 删除files.txt中列出的文件`
66. man：查看命令的帮助文档<br>
`man ls`
67. tee：从标准输入读取并写入到标准输出和文件<br>
`echo "Log entry" | tee -a log.txt`
68. trap：定义脚本中接收到信号时执行的动作<br>
`trap 'echo "Script interrupted!"' INT`
69. watch：周期性执行命令并显示输出<br>
`watch -n 5 df -h  # 每5秒显示一次磁盘使用情况`
70. basename：从路径中提取文件名<br>
`basename /path/to/file.txt  # 输出 file.txt`
71. dirname：提取文件路径中的目录部分<br>
`dirname /path/to/file.txt  # 输出 /path/to`
72. yes：持续输出字符串，通常用于自动确认<br>
`yes | apt install package_name`
73. sleep：延迟指定时间后再继续执行<br>
`sleep 5  # 暂停5秒`
74. seq：生成指定范围的数字序列<br>
`seq 1 5  # 输出 1 2 3 4 5`
75. cut：按列提取文本内容<br>
`cut -d ':' -f1 /etc/passwd  # 提取第1列用户名`
76. tr：替换或删除字符<br>
`echo "hello" | tr 'a-z' 'A-Z'  # 输出 HELLO`
77. uniq：去除重复行（通常配合 sort 使用）<br>
`sort file.txt | uniq`
78. sort：对文本内容排序<br>
`sort file.txt`
79. wc：统计文件中的行数、单词数和字节数<br>
`wc -l file.txt  # 统计行数`
80. file：查看文件类型<br>
`file filename`





