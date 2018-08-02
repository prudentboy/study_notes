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
> string A; A.assign("new_string_value1");
> string B; B.assign(A);
> char[20] = "new_string_value2"; B.assign(char, 17);

3. 高级
- 判断字符串是否回文
> return equal(str.begin(), str.begin() + str.length()/2, str.rbegin());

### 踩坑记录 ###
1. std::copy
- 使用copy时要注意拷贝对象的空间大小
```
std::vector<int> a(1,1);
std::vector<int> b(5,0);
std::copy(b.begin(), b.end(), a.begin()); // 出现段错误，因为a没有足够存放b的空间
```

### C++1x学习笔记 ###
#### 弃用特性（不建议再使用） ####
1. 弃用关键字/操作
- register
- export特性
- bool类型变量的自增操作(++)

2. 替换关键字/操作
- auto_ptr -> unique_ptr
- 字面值常量赋值给char *变量被弃用 -> 赋值给const char*或auto
- C语言风格类型转换 -> static_cast/reinterpret_cast/const_cast
- unexpected_handler/set_unexpected() -> noexcept
- 参数绑定 -> std::bind/std::function

3. 类操作
- 类有析构，则为其生成拷贝构造和拷贝赋值的特性被弃用

4. 兼容方式
- C++不是C的超集
- 使用extern "C"处理C语言风格代码
- 分离编译再统一链接


#### C++11新特性 ####
##### 语言优化 #####
1. NULL -> nullptr
- NULL不再等同于0
- nullptr类型为nullptr_t
- nullptr支持隐式转换为任何指针
- nullptr支持与任何指针进行相等或不等的比较

2. 使用关键字constexpr声明函数编译为常量
- 可以使用constexpr函数结果定义数组大小
- 支持函数递归
> constexpr int fibonacci(const int n) // ok in cpp11 and upper
> {
>     retrun n == 1 || n == 2 ? 1 : fibonacci(n-1) + fibonacci(n-2);
> }
> constexpr int fibonacci2(const int n) // ok in cpp14 and upper
> {
>     if (n == 1) retrun 1;
      if (n == 2) return 1;
      return fibonacci(n-1) + fibonacci(n-2);
> }

3. 类型推导auto、decltype
- 几个auto常见case
> auto i = 6.0; // 普通变量声明
> for(auto i = v.begin(); i != vec.end(); ++i) {} // 迭代器
> auto arr = new auto(10); // 动态值声明，此例推导为int *
- auto不能使用的情况
> int add(auto x, auto y); // 编译失败，不能用于参数传参
> int a[2] = {0}; auto b = a; // 错误，不能用于推导数组类型
- decltype用于解决auto只能对变量进行推导的缺陷
> auto x = 1; auto y = 2; decltype(x+y) z;
- auto与decltype配合尾返回类型实现模板
> template<typename T, typename U>
> auto add(T x, U y) -> decltype(x+y)
> {
>     return x + y;
> }
> template<typename T14, typename U14> 
> auto add(T x, U y) // ok in cpp14 and upper
> {
>     return x + y;
> }

4. 范围for循环
- cpp11可实现基于范围的迭代，类似于python语法
> std::vector<int> arr(7, 10);
> for (auto &i : arr) {++i;} // '&'符号决定变量能否修改

5. 初始化列表
- 允许绝大多数类型用{}的统一初始化方式进行初始化
> struct A {int a; float b;};
> struct B
> {
>     B(int _a, float _b): a(_a),b(_b) {}
> private:
>     int a;
>     float b;
> };
> A a {5, 5.0};
> B b {7, 7.0};
- 更详细说明详见链接(https://blog.csdn.net/hailong0715/article/details/54018002)

6. 外部模板
- 允许使用extern关键字显示告知编译器实例化时机
> extern template class std::vector<SelfDefClass>; // 声明不在当前文件实例化

7. 模板默认类型
- 新增置顶模板默认类型的功能支持
> template<typename T = int, typename U = double>
> auto add(T x, U y) -> decltype(x + y) {return x + y;}

8. 变长参数模板
- 支持类似printf函数参数的情况
> template<typename Require, typename... Args>
- 使用sizeof...关键字可获取变长参数个数
> template<typename... Args>
> void Count<Args... arg>
> {
>     std::cout << sizeof...(args) << std::endl;
> }
- 递归模板函数和初始化列表展开是两种常见参数解包方法（详见26-27页）

9. typedef -> using
- using写法拥有比typedef更强的功能
> using pfun = int(*)(void *); // 提高可读性
> template<typename T, typename U>
> class ExampleType;
> using TempType = ExampleType<int, double>; // 支持实例化模板别名

10. 构造函数增强
- 支持委托构造
> class A
> {
> public:
>     int a, b;
>     A() {a = 1;}
>     A(int _b) : A() // 先调用委托函数，再执行函数体
>     {
>         b = _b;
>     }
> };
- 支持继承构造
> class B : public A
> {
> public:
>     using A::A; // 继承基类A的所有构造函数
> };

11. 虚函数重载增强
- override关键字用于显式告知编译器重载
> struct A {virtual void func(int)};
> struct B : A {virtual void func(int) override;} // 编译器会检查基类是否存在对应虚函数，不存在会编译失败
- final关键字防止子类重载虚函数
> struct C {virtual void func() final;} // 子类不可再重载该函数
- final关键字另一个用法是防止类被继承
> struct D final : C {}; // D类不可再被继承

12. 类的默认函数强化
- 使用default关键字显式声明使用默认函数
- 使用delete关键字显示声明拒绝默认函数
> class E
> {
> public:
>     E() = default; // 使用默认函数
>     E& operator=(const E&) = delete; // 拒绝默认函数
> };

13. 强类型枚举
- 支持使用enum class声明枚举类
- 枚举类类型安全，不能隐式转换为数字，必须显式类型转换
- 枚举类类型可以指定枚举值类型（默认int）
- 枚举类类型可以赋值
- 枚举类类型可以为枚举值赋相同值
> enum class SuperiorEnum : unsigned int
> {
>     a, // = 0
>     b, // = 1
>     c = 100,
>     d = 100
> };

#### 运行期强化 ####
1. lambda表达式
- 提供匿名函数的功能
- 基本语法：
> \[捕获列表\](参数列表) mutable(可选项) 异常属性 -> 返回类型 {函数体}
- 捕获列表的几种形式
> [] //空捕获列表
> [v1, v2, ...] //捕获变量值，相当于函数传值
> [&v1, &v2, ...] //捕获变量引用，相当于函数传引用
> [&] //引用捕获，编译器自动推导变量列表
> [=] //值捕获，编译器自动推导变量列表
- 表达式捕获(cpp14以上支持)
> auto pa = std::make_unique<int>(1);
> auto add = \[v1 = 1, v2 = std::move(pa)\](int x, int y) -> int
> {
>     return x + y + v1 + (*v2);
> }
- 泛型lambda(cpp14以上支持)
> auto add = [](auto x, auto y) {return x + y;}; // 定义泛型lambda
> add(1.1, 2.2); // 使用泛型函数

2. 函数的容器std::function
- 相对函数指针类型安全
> int func(int a) {return a * a;}
> std::function<int(int)> f = func; // 定义了func函数的一个封装
> std::cout << f(2) << std::endl; // 输出4

3. 函数调用参数绑定std::bind
- 常配合占位符std::placeholder进行使用
> int f(int a, int b, int c) { return a / b + c; }
> auto subf = std::bind(f, std::placeholders::\_1, 2, 1); //subf被绑定了第2、3参数分别为2、1的函数
> std::cout << subf(5) << std::endl; //输出3

4. 右值引用
- 左值：表达式处理后依然存在的持久对象
- 右值：纯右值 + 将亡值
- 纯右值：字面量、匿名临时变量、非引用返回的临时变量、运算表达式产生的临时变量、原始字面量、Lambda表达式
> 10 true 1+2
- 将亡值：即将被销毁，能被移动的值
- 使用T &&（T是类型）可通过右值引用拿到将亡值，临时延长其生命周期
- 使用std::move将左值无条件转换为右值
> std::string str = "string";
> //std::string&& rf1 = str; // 错误，右值引用不能引用左值
> std::string rf2 = std::move(str); // ok
- 右值引用解决了旧C++不区分移动和拷贝的问题。
- 使用std::forward实现完美转发

#### 杂项 ####
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

4. 尖括号 >
- 处理了嵌套模板>>导致被当做右移符编译出错的问题
> std::vector<std::vector<int>> a; // ok in cpp11 and upper

#### C++17特性 ####
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

#### 未加入特性 ####
1. concepts
- 类似python语言中的sortable、countable概念声明，用来优化模板编程不能在编译期间检查的体验
