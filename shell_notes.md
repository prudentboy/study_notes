## shell命令 ##

### 脚本技巧 ###
01. #!/bin/bash  
在脚本文件具有可执行权限x时，脚本首部的该行化可使脚本能够直接执行。

02. PWD=`/usr/bin/dirname $0`;cd $PWD  
dirname命令用于获取路径，$0指向当前（脚本文件所在）路径。  
脚本中增加这行话能确保在crontab中运行脚本时不会因为路径问题导致运行失败。

### 系统命令 ###
01. passwd: 修改用户密码
```
passwd *user* #修改用户*user*的密码，需要root权限
```
02. 修改用户主目录的方法
```
vim /etc/passwd #修改对应用户的响应行即可，需要root权限，需要重新登录该用户生效
```
03. 修改网络连接参数  
详情没有特别理解，需要root权限
```
/sbin/sysctl -w net.ipv4.tcp_timestamps=1
/sbin/sysctl -w net.ipv4.tcp_tw_recycle=1
```
04. ifconfig：查看本机ip地址
```
ip=$(/sbin/ifconfig |grep "inet addr" |awk '{split($2,array,":");print array[2];exit}')
```

### 常用命令 ###
01. ps: 查看进程  
```
ps -o etime   ##查看进程已运行时间
```
02. tail: 查看文件尾部
```
tailf dir   ##查看文件（显示变化）
```
03. wc: 计数  
```
$(ls $file_path |wc -l)   ##统计文件数
```
04. bc: 计算器  
```
echo "scale=0; $file_num/$process_num" | bc   ##输出$file_num/$process_num，保留整数
```
05. tar: 打包/拆包、压缩/解压
```
tar zcvf filename.tar.gz dir  ##文件压缩
tar zcvf filename.tar.gz   ##文件解压
tar cvf filename.tar dir   ##文件打包（不压缩）
tar xvf filename.tar   ##文件解包
```
06. sort: 排序  
-t指定分隔符；-n按数值排序；-o结果存入原文件  
-r降序；-u去重；-k n按某字段n排序；-f忽略大小写
```
sort filename -k2rn ##按第二字段数值降序排列
```
07. seq: 生成序列
-w: 按位补零
```
seq -w 100 ##生成001、002……100的序列，无-w则为1、2……100
```
08. 重定向>和>>  
\>>表示以追加方式进行重定向

09. cut: 截取  
-f按域截取，配合-d设置分隔符  
可以结合rev实现截取倒数第几个字符。
```
tail log | rev | cut -f 1 | cut -d'&' -f 1 | rev ##依次按\t和&分割，取最后一字段
```

10. time: 获取过程运行时间  
使用时直接在原命令或函数过程前加上time 即可  
默认显示为real、user、sys三行，以xmxxx.xxxs的格式输出

11. 数组遍历的使用
```
history_filename="textname videoname"
for file in ${history_filename[@]}
do
    #action
done
```
详细数组的使用方法参见：[数组、关联数组和别名使用](http://www.1987.name/164.html)

12. pwd  
打印当前工作目录，对于链接文件使用-P参数可以显示软链后的目标文件路径。  

13. mkdir  
注意熟悉使用-p参数直接生成所有的父目录，使用-m参数可指定目录的权限。  

14. dirname/basename  
获取路径名/获取文档名

15. cat/tac/nl/more/less/head/tail/od  
查看文件命令，分别为：正向显示、反向显示、按行号显示、向后翻页显示、前后翻页显示、显示前几行、显示后几行、二进制显示  

16. curl
请求指定网址，无附加参数时curl命令会直接返回网页返回结果。
可通过-I参数查看返回参数信息；可通过-L参数查看所有跳转信息。

17. 进制转换
- n进制转十进制
```
n_radix_num=111;
((num=n#n_radix_num))
```

### 目录结构 ###
1. 特殊目录表达  
- .：当前目录  
- ..：上层目录（根目录的上层目录仍为根目录）  
- -：上次访问的目录  
- ~：当前用户home目录（cd的默认目录）  
- ~*user*：用户*user*的home目录  
