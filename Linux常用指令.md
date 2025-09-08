# Linux 常用指令

1. ls：列出当前目录中的文件和子目录<br>
`l`
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
