## vim学习 ##

### 基本命令 ###
1. 关闭vim  
- q退出：改动未保存时会提示，不能退出  
- q!强制退出：不保存改动，退出  
- wq保存退出：保存改动并退出  
- qa退出所有：退出所有窗口  
2. 文字替换
- :s/Before/After/ 基础用法，将当前行的第一个Before替换为After
- s前添加%表示对所有行进行操作
- 最后一个/后可以添加g用来进行指定行的全部替换，亦可以添加gc用来确认后替换
- 命令分隔符不必为/还可用+#等其他字符

### 环境配置 ###
1. 用户可在用户根目录加建立配置文件.vimrc对vim编码等问题进行配置
2. 配置语法
- "开头的语句表示注释
3. 常见配置
```
" utf8编码
set fileencodings=utf-8,gbk,cp936,cp950,latin1                                                         
set encoding=utf-8
" 显示行号
set nu
" 智能缩排
set si
set nowritebackup
" 下划线
set cursorline
" 设置tab自动转化成空格
set expandtab
set tabstop=4
set softtabstop=4
set shiftwidth=4
" 自动缩howmatch
set cindent
" 打开光标的行列位置显示功能
set ruler

"set showcmd

"输入字符串就显示匹配点
set incsearch
""去掉有关vi一致性模式，避免以前版本的一些bug和局限
set nocp
" 设置终端为256色
"set t_Co=256
" 关闭兼容vi模式，让vim更强大
set nocompatible
```

### tip ###
- '\3'在vim中会显示为^C，'\4'则会显示为^D，以此类推
