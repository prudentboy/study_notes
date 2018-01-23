## awk学习 ##
### tips ###
 + 查找dict：
```
if(d in dict) {do something} ##如果存在，则操作
if(d in dict == 0) {do something} ##如果不存在，则操作
```  
 + 多文件处理：  
仅首个文件操作不同时：
```
if(NR == FNR) {file1 dealt}
else {other files dealt}
```
