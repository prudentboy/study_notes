## shell命令 ##

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
