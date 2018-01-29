# git学习笔记
## 常用命令
- 安装:  
Debian/Ubantu: sudo apt-get install git(-core)  
Mac: 可以使用brew或Xcode安装  
Windows: Git官网下载安装程序安装即可，使用时用Git Bash  
- 应用:  
git init: 创建本地仓库  
git add File_list: 添加文件至仓库  
git commit File_list: 提交文件至仓库  
	-m: 添加相关提交说明  
git status: 查看本地仓库状态  
git diff: 查看本地仓储修改
git log: 查看本地仓库提交日志
git reset --hard Ci_id: 回退至Ci_id版本
- 配置config：  
git config --global user.name "Name"
git config --global user.email "Email"
