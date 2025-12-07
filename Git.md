# Git

## .gitignore
* 使用.gitignore文件来忽略不需要跟踪的文件或目录。
``` bash
# 创建.gitignore文件
touch .gitignore
```
* 忽略文件
```
# 忽略所有的.log文件
*.log
# 忽略特定目录
temp/
# 忽略特定文件
secret.txt
``` 

## .gitkeep
* git中空文件夹是无效的不会被add到暂存区，可以通过创建.gitkeep文件来保留空文件夹