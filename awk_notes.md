## awk学习 ##
### 使用技巧 ###
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

### 注意事项 ###
- awk中字符串不支持+=运算符
```
ans="add"
ans+=" more chars" #ans!=add more chars
ans=ans" more chars" #ans=add more chars
```
