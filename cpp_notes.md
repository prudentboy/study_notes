## C++学习笔记 ##

### 字符串 ###
1. 初始化
- 默认初始化为空字符串
- 直接初始化
> string A("A is a string.");  
> string B(A); // 用字符串A初始化B  
> string C(100, ‘6’); // 字符串C被初始化为100个6  
> string D(A, 7, 6); // 字符串D被初始化为A的第7位开始的6字符长字符串
- 拷贝初始化
> string a = "A is a string";
> string b = a;
> string c = string(100, '6');  

2. 操作
