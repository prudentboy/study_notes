## C++学习笔记 ##

### 注释 ###
1. 单行注释//
- 注意反斜线换行符号后不允许后边跟注释或空格
2. 多行注释/**/
- 注意下面语法是正确的
> std::cout << "/**";
> std::cout << "**/";

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

2. 赋值
- assign
  + clear + set_new_value
    string A; A.assign("new_string_value1");
    string B; B.assign(A);
    char[20] = "new_string_value2"; B.assign(char, 17);

3. 高级
- 判断字符串是否回文
    return equal(str.begin(), str.begin() + str.length()/2, str.rbegin());

### C++1x学习笔记 ###
#### 弃用特性（不建议再使用） ####
1. 弃用关键字/操作
- register
- export特性
- bool类型变量的自增操作(++)

2. 替换关键字/操作
- auto_ptr -> unique_ptr
- 字面值常量赋值给char \*变量，
- unexpected_handler/set_unexpected() -> noexcept

3. 类操作
- 类有析构，则为其生成拷贝构造和拷贝赋值的特性被弃用

1. long long int
- 正式纳入标准库，至少64比特

2. noexcept
- 函数名后使用
> void no_err_throw() noexcept; // 不允许抛出异常
- 修饰函数使异常不扩散，若被noexcept修饰的函数抛出异常则系统会调用std::terminate()终止程序
- 可以做操作符使用
> noexcept(*express*); // 无异常返回true，反之返回false

3. 字符串字面量
- 新增R括号语法避免转义符的使用，类似python中的r用法
> std::string str = R"(C:\\What\\The\\Fxxk)"; //大写R，字符串用括号包裹
- 新增整型、浮点型、字符串、字符字面量拼接，通过重载双引号操作符实现
> std::string	operator"" _rank (unsigned long long i)
> {
>     return std::to_string(i)+"th";
> }
> // useage:
> auto num_rank = 5_rank; // num_rank = "5th"

### C++17特性 ###
1. 非类型模板参数auto
- 允许在模板中使用auto进行类型推断

2. std::variant()
- 集合，内部可容纳各种类型

3. 结构化绑定
- 允许类似python的多返回语法
> std::tuple<int, double, std::string> f() // 函数定义
> {
>     return std::make_tuple(1, 2.3, "456");
> }
> // useage:
> auto [x,y,z] = f(); // x,y,z自动推断为相应类型

4. 变量声明强化
- 允许在if和switch语句中声明临时变量，类似之前for循环声明临时迭代器的语法
> if (auto p = map_container.try_emplace(key,value); !p.second) {;} // allow in c++17

### 未加入特性 ###
1. concepts
- 类似python语言中的sortable、countable概念声明，用来优化模板编程不能在编译期间检查的体验
