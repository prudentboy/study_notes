## C++学习笔记 ##

### 变量类型 ###
1. 枚举
- 注意每个枚举项后边用逗号分隔
> enum EM_NAME
> { EM_VALUE = 0, ...}

### 内置变量 ###
1. 变量类型的最大最小值
- C++:  
> #include <limits>
> *Type* min = std::numeric_limits<*Type*>::min();
> *Type* max = std::numeric_limits<*Type*>::max();
- C:  
> #include <limits.h>
> int min = INT_MIN, max = INT_MAX;
> float fmin = FLT_MIN, fmax = FLT_MAX;
> double dmin = DBL_MIN, dmax = DBL_MAX;

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

3. 高级
- 判断字符串是否回文
> return equal(str.begin(), str.begin() + str.length()/2, str.rbegin());
