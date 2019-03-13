
Cpp-基础
==

# 语言

## 自然语言

### 有声

    语音
    语调

### 无声

    语法
    语义
    语境

    字
        关键字
        标点
    词
        组合
    句
        基本句式

## 编程语言

```
编程语言分类

低级
    机器语言
    汇编语言
高级
    说某种语言是高级语言其实是相对计算机语言来说的，机器语言最低级，汇编次之，结构化，面向对象。对计算机而言，抽象的层度越来越高。但是，这种抽象其实对人来说是越来越具体的。因为：学习计算机编程语言和学习自然语言一样，变得越来越自然了。

语言排行
    TIOBE(The Importance Of Being Earnest) 发音读[ti'ɔbi]
    Java， C，Python, C++,VB .net, JS, C#, Php, SQL, Objective-C, VB, Go, Swift
    https://www.tiobe.com/tiobe-index/

语言分类

    是否需要编译区分
        编译型
        解释性
        混合型

   强弱动静区分
        强类型语言：
            一旦一个变量被指定了某个数据类型，如果不经过强制类型转换，那么它就永远是这个数据类型。
            你不能把一个整形变量当成一个字符串来处理。
        弱类型语言：
            数据类型可以被忽略，一个变量可以赋不同数据类型的值。
            一旦给一个整型变量a赋一个字符串值，那么a就变成字符类型。
    强动
    强静
    弱动
    弱静

C++编程语言： 
    编译型
    弱类型，静态语言
发明人：
    Bjarne Stroustrup（本贾尼·斯特劳斯特卢普）
通识：
    程序 = 数据结构 + 算法

C++程序：
        字
            关键字
                类型
                    数字
                        整型
                            有符号(signed)
                                char                1
                                short               2
                                int                 4
                                long                4
                                long long           8
                            无符号(unsigned)
                                unsigned char       1
                                unsigned int        4
                                unsigned long       4
                                unsigned long long  8
                        浮点型
                            float                   4
                            double                  8
                    字符串
                        单字符
                            char
                        多字符
                            char *
                            char []
                    指针
                        *p
                        **p
                        取址
                            *p
                        取值
                            p (指针指向地址）
                            &p (指针的地址）
                    引用
                        引用，顾名思义是某一个变量或对象的别名，对引用的操作与对其所绑定的变量或对象的操作完全等价
                        语法：类型 &引用名=目标变量名
                        样例：
                            int a = 10;
                            int &b=a;
                        引用注意：
                            1. &不是求地址运算符，而是起标志作用
                            2.引用的类型必须和其所绑定的变量的类型相同
                                错误样例：
                                double a=10.3;
                                int &b=a; //错误，引用的类型必须和其所绑定的变量的类型相同
                            3.声明引用的同时必须对其初始化，否则系统会报错
                                int &a; //错误！声明引用的同时必须对其初始化
                            4.引用相当于变量或对象的别名，因此不能再将已有的引用名作为其他变量或对象的名字或别名
                            5.引用不是定义一个新的变量或对象，因此内存不会为引用开辟新的空间存储这个引用
                            6.对数组的引用
                                语法：类型 (&引用名)[数组中元素数量]=数组名；
                                int a[3]={1,2,3};
                                int (&b)[3]=a;//对数组的引用
                            7.对指针的引用
                                语法：类型 *&引用名=指针名;//可以理解为：（类型*） &引用名=指针名，即将指针的类型当成类型*
                                int a=10;
                                int *ptr=&a;
                                int *&new_ptr=ptr;
                                cout<<&ptr<<" "<<&new_ptr<<endl;
            标点
                , ; = & > < >= <= != == >> << && || ! {} [] () <> '' "" \ # ## // /**/ 空格
                , 逗号分隔
                    多行并单行
                        int a, b;
                        <==>
                        int a;
                        int b;
                    逗号运算
                        表达式1, 表达式2 (先求解表达式1，再求解表达式2。整个逗号表达式的值是表达式2的值)
                        for (int i=0; i++; i++, j++)
                ; 分号分隔
                    语句结束
                        ; 每条语句结尾必须用
                    循环内部
                        for (int i = 0; i < 10; i++)
                = 赋值
                & 取值，引用
                > < >= <=  != == 算数比较运算
                    >, 大于
                    <, 小于
                    >=, 大于等于
                    <=, 小于等于
                    != 不等于
                    == 等于
                >> << 移位运算
                && || ! 逻辑运算
                    && 与
                    || 或
                    ！ 非
                {} 花括号（语句块）
                    函数
                        fun() {
                            //...
                        }
                    循环
                        for (int i = 0; i < 10; i++) {
                            //...
                        }
                    选择
                        if () {
                            //...
                        }
                        else {
                            //...
                        }
                [] 中括号
                    数组
                        1.声明变量时使用“[]”，表示数组。如下所示： 
                        int a[5];    //定义了一个大小为5的整型数组 
                        int a[]={1,2,3,4,5};    //定义一个整型数组并初始化 
                        int *p=new int[size];    //申请一个动态整型数组，数组长度由变量size决定 
                        int (*a)[10];    //定义一个数组指针，注意：*a表明a是指针类型，而[10]则表明a指向的是一个大小为10的数组。
                        /* 这一条与上一条对比来看，同样表示了一个大小为10的数组，不过数组元素均是指向整型变量的指针，故称为指针数组。 */
                        int *a[10];    
                        2.表示下标运算。如下所示： 
                        int *p; 
                        p[1]=2; 
                        上面的语句不难理解：定义了一个指向整型变量的指针p，由于指针变量中保存着地址，通过“地址+[]”的运算即可给下一地址赋值2. 
                        3.指示指针。这种用法一般是在数组作为函数参数时会用到。如下所示： 
                        void fun(int a[]);    //[]说明a是一个指针变量 
                        /* 
                        前一个“[]”说明a是指针类型，后一个“[]”则说明指针数组的大小为10.
                        这里的“数组”指的是由二维数组行向量构成的一维数组。
                        这种书写方式一般是在二维数组作为函数参数调用时会用到，此处的10即代表的是数组第二维的大小。
                        需要注意的是，第二维的大小必须明确。 
                        */
                        void fun(int a[][10]); 
                        void fun(int (*a)[10]);    //这种写法和上面是等价的。

                () 小括号
                    参数边界
                        函数参数边界
                            fun (int a, int b)
                        循环
                            for (int i = 0; i < 10; i++)
                            while(i < 10)
                        选择
                            if (a > 10)
                            {
                                //...
                            }
                            else {}
                    默认构造
                        int a = 10;
                        int b(a);
                <> 尖括号
                    文件包含
                    #include <iostream>
                ''  单引号（成对）
                    单字符
                        char ch = 'a';
                ""  双引号（成对）
                    字符串
                        char *sz = "hello";
                \ 反斜杠
                    转义
                        \\ 转义符号
                        \n  换行
                        \n	换行(LF)	010
                        \r	回车(CR)	013
                        \t	水平制表(HT)	009
                        \'	单引号字符	039
                        \"	双引号字符	034
                        \0	空字符(NULL)	000
                    接上一行
                        样例，函数长参数列表：
                        void fun(int a, int b, \
                                int c)
                       样例，宏：
                       #define add(f)   \
                        int main()      \
                        {               \
                            ph();       \
                            return f;   \
                        }
                # ## 宏拼接
                    # 是字符串化的意思，出现在宏定义中的#是把跟在后面的参数转成一个字符串；
                        #define  strcpy__(dst, src)      strcpy(dst, #src)
                        strcpy__(buff,abc)  相当于 strcpy__(buff,“abc”)
                    ##是连接符号，把参数连接在一起
                        #define FUN(arg)     my##arg
                        则     FUN(ABC)
                        等价于  myABC
                // 单行注释
                    //xxxx
                /**/ 多行注释
                    /*
                    1.xxxx
                    2.xxxx
                    */
        词
            单字（保留字）
                C++中共有74个关键字 保留字
                    A# and and_eq asm auto
                    B# bitand bitor bool break
                    C# case catch char class compl const const_cast continue
                    D# default delete do double dynamic_cast else enum explicit
                    E# export extern 
                    F# false float for friend 
                    G# goto 
                    H#
                    I# if inline int 
                    J#
                    K#
                    L# long 
                    M# mutable
                    N# namespace new not not_eq
                    O# operator or or_eq 
                    P# private protected public 
                    R# register reinterpret_cast return 
                    S# short signed struct sizeof static static_cast switch
                    T# throw template this typeid true try typedef typename
                    U# using union unsigned 
                    V# virtual void volatile 
                    W# wchar_t while
                    X# xor xor_eq
                    Y#
                    Z#

                根据其内容可将其细分一下：
                    基本的数据类型关键字：void, int, char, float, double, bool
                    类型修饰关键字：long, short, singed, unsigned 
                    布尔型字面值：true, false
                    非常重要的变量声明修饰符：const, inline
                    存储类别关键字：auto, static, extern, , register
                    控制结构关键字：for, while, if, else, do
                    switch语句关键字：switch, case, default
                    路径跳转关键字：break, continue, return, goto
                    动态创建变量关键字：new, delete
                    长度运算符：sizeof
                    复合类型关键字：class, struct, enum, union, typedef
                    与类成员相关关键字：this, friend, virtual, mutable, explicit, operator 
                    派生类继承方式：private, protected, public
                    模板：template, typename
                    命名空间：namespace, using
                    异常处理：catch, throw, try,
                    各种操作符的替代名：and, and_eq, bitand, bitor, compl, not, not_eq, or, or_eq, xor, xor_eq
                    其他不常用的：asm, export, typeid, volatile
                
            组合（成对的字）
                //////////////////////
                new;
                delete;
                //////////////////////
                try {
                }
                catch(xx){
                }
        句
            基本句式
                顺序
                    语句1;
                    语句2;
                选择
                    //////////////////////
                    if(){
                    } 
                    else(){
                    }
                    //////////////////////
                    switch() {
                    case a:
                        {
                            //...
                            break;
                        }
                     //...
                     default:
                     {
                        //...
                     }
                    }
                循环
                    //////////////////////
                    for(...) {
                        //...
                    }
                    //////////////////////
                    while(...) {
                        //...
                    }
                    //////////////////////
                    do {
                    }while(1);
              面向过程
                结构体
                函数（方法）
              面向对象
                抽象数据类型
                类
                    成员
                    成员函数（方法）
                对象
                    类的实例
                访问控制
                    private     私有
                    protected   保护
                    public      公开
                面向对象3大特征
                    封装（按粒度分）
                        数据结构封装
                            类（属性+方法）/（成员变量+成员函数）
                        函数封装
                            函数功能
                            通用接口
                        模块封装
                            业务功能
                            通用模块
                    继承（复用性）
                        单继承
                            子类->父类
                        多继承
                            子类->多父类
                    多态
                        重写
                            覆盖之前方法
                        重载
                            根据运行时，选择方法
              泛型编程
                通用模式
                STL 标准模板库
                    STL的六大组件
                    1.容器（Container），
                        是一种数据结构，如list，vector，和deques ，以模板类的方法提供。为了访问容器中的数据，可以使用由容器类输出的迭代器；
                    2.迭代器（Iterator），
                        提供了访问容器中对象的方法。例如，可以使用一对迭代器指定list或vector中的一定范围的对象。迭代器就如同一个指针。
                        事实上，C++的指针也是一种迭代器。但是，迭代器也可以是那些定义了operator*()以及其他类似于指针的操作符地方法的类对象；
                    3.算法（Algorithm），
                        是用来操作容器中的数据的模板函数。
                        例如，STL用sort()来对一个vector中的数据进行排序，用find()来搜索一个list中的对象，
                        函数本身与他们操作的数据的结构和类型无关，
                        因此他们可以在从简单数组到高度复杂容器的任何数据结构上使用；
                    4.仿函数（Function object），
                        仿函数(functor)又称之为函数对象（functionobject），其实就是重载了()操作符的struct，没有什么特别的地方
                    5.迭代适配器（Adaptor）
                    6.空间配制器（allocator）
                        其中主要工作包括两部分
                            1.对象的创建与销毁    
                            2.内存的获取与释放
               工程化
                    文件包含
                        #include <iostream>
                        #include "hello.h"
                    外部引用
                        链接库
                            动态链接库
                            静态链接库
                        交叉编译
                            C++ 使用别的语言库
                                使用C
                                    extern “C”
                            别的语言使用 C++库
                    编译链接
                        源程序 -》 预处理 -》 编译 -》 汇编 -》 链接 -》 可执行文件
                        编译（编译工具）
                            IDE
                                Windows
                                    Visual studio C++
                                        VS6.0
                                        VS2005
                                        VS2008
                                        VS2010
                                        VS2013
                                        VS2015
                                        VS2017
                                        VS2019
                                    VSCode
                                Linux
                                    编辑器编辑,  vim, Emacs, gedit,
                                跨平台
                                    Code::Blocks
                                    Eclipse
                                    QT
                                    编辑器编辑, Atom, Sublime Text
                            Console
                                gcc and g++分别是GNU的c & c++编译器。
                                    gcc编译C语言程序
                                    g++编译c++程序
                                Intel C++ Compiler （简称 icc 或 icl）
                                    intel对C++编译器的优化版本
                         调试工具（gdb）
                            单步调试
                            断点
                    框架
                        通用功能分
                            boost
                                1.字符串和文本处理库
                                    a) Conversion库：对C++类型转换的增强，提供更强的类型安全转换、更高效的类型安全保护、进行范围检查的数值转换和词法转换。
                                    b) Format库：实现类似printf的格式化对象，可以把参数格式化到一个字符串，而且是完全类型安全的。
                                    c) IOStream库 ：扩展C++标准库流处理，建立一个流处理框架。
                                    d) Lexical Cast库：用于字符串、整数、浮点数的字面转换。
                                    e) Regex 库：正则表达式，已经被TR1所接受。
                                    f) Spirit库：基于EBNF范式的LL解析器框架
                                    g) String Algo库：一组与字符串相关的算法
                                    h) Tokenizer库：把字符串拆成一组记号的方法
                                    i) Wave库：使用spirit库开发的一个完全符合C/C++标准的预处理器
                                    j) Xpressive 库：无需编译即可使用的正则表达式库
                                2.容器库
                                    a) Array 库：对C语言风格的数组进行包装
                                    b) Bimap 库：双向映射结构库
                                    c) Circular Buffer 库：实现循环缓冲区的数据结构
                                    d) Disjoint Sets库 ：实现不相交集的库
                                    e) Dynamic Bitset 库：支持运行时调整容器大小的位集合
                                    f) GIL 库：通用图像库
                                    g) Graph 库：处理图结构的库
                                    h) ICL 库：区间容器库，处理区间集合和映射
                                    i) Intrusive 库：侵入式容器和算法
                                    j) Multi-Array 库：多维容器
                                    k) Multi-Index 库：实现具有多个STL兼容索引的容器
                                    l) Pointer Container 库：容纳指针的容器
                                    m) Property Map 库：提供键/值映射的属性概念定义
                                    n) Property Tree 库：保存了多个属性值的树形数据结构
                                    o) Unordered 库：散列容器，相当于hash_xxx
                                    p) Variant 库：简单地说，就是持有string, vector等复杂类型的联合体
                                3.迭代器库
                                    a) GIL 库：通用图像库
                                    b) Graph 库：处理图结构的库
                                    c) Iterators 库：为创建新的迭代器提供框架
                                    d) Operators 库：允许用户在自己的类里仅定义少量的操作符，就可方便地自动生成其他操作符重载，而且保证正确的语义实现
                                    e) Tokenizer 库：把字符串拆成一组记号的方法
                                4.算法库
                                    a) Foreach库：容器遍历算法
                                    b) GIL库：通用图像库
                                    c) Graph库：处理图结构的库
                                    d) Min-Max库：可在同一次操作中同时得到最大值和最小值
                                    e) Range库：一组关于范围的概念和实用程序
                                    f) String Algo库：可在不使用正则表达式的情况下处理大多数字符串相关算法操作
                                    g) Utility库：小工具的集合
                                5.函数对象和高阶编程库
                                    a) Bind库：绑定器的泛化，已被收入TR1
                                    b) Function库：实现一个通用的回调机制，已被收入TR1
                                    c) Functional库：适配器的增强版本
                                    d) Functional/Factory库：用于实现静态和动态的工厂模式
                                    e) Functional/Forward库：用于接受任何类型的参数
                                    f) Functional/Hash库：实现了TR1中的散列函数
                                    g) Lambda库：Lambda表达式，即未命名函数
                                    h) Member Function库：是STL中mem_fun和mem_fun_ref的扩展
                                    i) Ref库：包装了对一个对象的引用，已被收入TR1
                                    j) Result Of库：用于确定一个调用表达式的返回类型，已被收入TR1
                                    k) Signals库：实现线程安全的观察者模式
                                    l) Signals2库：基于Signal的另一种实现
                                    m) Utility库：小工具的集合
                                    n) Phoenix库：实现在C++中的函数式编程。
                                6.泛型编程库
                                    a) Call Traits库：封装可能是最好的函数传参方式
                                    b) Concept Check库：用来检查是否符合某个概念
                                    c) Enable If库:允许模板函数或模板类在偏特化时仅针对某些特定类型有效
                                    d) Function Types库：提供对函数、函数指针、函数引用和成员指针等类型进行分类分解和合成的功能
                                    e) GIL库：通用图像库
                                    f) In Place Factory, Typed In Place Factory库：工厂模式的一种实现
                                    g) Operators库：允许用户在自己的类里仅定义少量的操作符，就可方便地自动生成其他操作符重载，而且保证正确的语义实现
                                    h) Property Map库：提供键值映射的属性概念定义
                                    i) Static Assert库：把断言的诊断时刻由运行期提前到编译期，让编译器检查可能发生的错误
                                    j) Type Traits库：在编译时确定类型是否具有某些特征
                                    k) TTI库：实现类型萃取的反射功能。
                                7.模板元编程
                                    a) Fusion库：提供基于tuple的编译期容器和算法
                                    b) MPL库：模板元编程框架
                                    c) Proto库：构建专用领域嵌入式语言
                                    d) Static Assert库：把断言的诊断时刻由运行期提前到编译期，让编译器检查可能发生的错误
                                    e) Type Traits库：在编译时确定类型是否具有某些特征
                                8.预处理元编程库
                                    a) Preprocessors库：提供预处理元编程工具
                                9.并发编程库
                                    a) Asio库：基于操作系统提供的异步机制，采用前摄设计模式实现了可移植的异步IO操作
                                    b) Interprocess库：实现了可移植的进程间通信功能，包括共享内存、内存映射文件、信号量、文件锁、消息队列等
                                    c) MPI库：用于高性能的分布式并行开发
                                    d) Thread库：为C++增加线程处理能力，支持Windows和POSIX线程
                                    e)Context库：提供了在单个线程上的协同式多任务处理的支持。该库可以用于实现用户级的多任务处理的机制，比如说协程coroutines，用户级协作线程或者类似于C#语言中yield关键字的实现。 [1] 
                                    f) Atomic库：实现C++11样式的atomic<>，提供原子数据类型的支持和对这些原子类型的原子操作的支持。
                                    g)Coroutine库：实现对协程的支持。协程与线程的不同之处在于，协程是基于合作式多任务的，而多线程是基于抢先式多任务的。
                                    h)Lockfree库：提供对无锁数据结构的支持。
                                10.数学和数字库
                                    a) Accumulators库：用于增量计算的累加器的框架
                                    b) Integer库：提供一组有关整数处理的类
                                    c) Interval库：处理区间概念的数学问题
                                    d) Math库：数学领域的模板类和算法
                                    e) Math Common Factor库：用于支持最大公约数和最小公倍数
                                    f) Math Octonion库 ：用于支持八元数
                                    g) Math Quaternion库：用于支持四元数
                                    h) Math/Special Functions库：数学上一些常用的函数
                                    i) Math/Statistical Distributions库：用于单变量统计分布操作
                                    j) Multi-Array库：多维容器
                                    k) Numeric Conversion库：用于安全数字转换的一组函数
                                    l) Operators库：允许用户在自己的类里仅定义少量的操作符，就可方便地自动生成其他操作符重载，而且保证正确的语义实现
                                    m) Random库：专注于伪随机数的实现，有多种算法可以产生高质量的伪随机数
                                    n) Rational库：实现了没有精度损失的有理数
                                    o) uBLAS库：用于线性代数领域的数学库
                                    p) Geometry库：用于解决几何问题的概念、原语和算法。
                                    q) Ratio库：根据C++ 0x标准N2661号建议 [2]  ，实现编译期的分数操作。
                                    r)Multiprecision库：提供比C++内置的整数、分数和浮点数精度更高的多精度数值运算功能。 [3] 
                                    s)Odeint库：用于求解常微分方程的初值问题。 [4] 
                                11.排错和测试库
                                    a) Concept Check库 ：用来检查是否符合某个概念
                                    b) Static Assert库 ：把断言的诊断时刻由运行期提前到编译期，让编译器检查可能发生的错误
                                    c) Test库：提供了一个用于单元测试的基于命令行界面的测试套件
                                12.数据结构库
                                    a) Any库：支持对任意类型的值进行类型安全的存取
                                    b) Bimap库：双向映射结构库
                                    c) Compressed Pair库：优化的对pair对象的存储
                                    d) Fusion库：提供基于tuple的编译期容器和算法
                                    e) ICL库：区间容器库，处理区间集合和映射
                                    f) Multi-Index库：为底层的容器提供多个索引
                                    g) Pointer Container库：容纳指针的容器
                                    h) Property Tree库：保存了多个属性值的树形数据结构
                                    i) Tuple库：元组，已被TR1接受
                                    j) Uuid库：用于表示和生成UUID
                                    k) Variant库：有类别的泛型联合类
                                    l) Heap库：对std::priority_queue扩展，实现优先级队列。
                                    m) Type Erasure: 实现运行时的多态。
                                13.图像处理库
                                    a) GIL库：通用图像库
                                14.输入输出库
                                    a) Assign库：用简洁的语法实现对STL容器赋值或者初始化
                                    b) Format库：实现类似printf的格式化对象，可以把参数格式化到一个字符串，而且是完全类型安全的
                                    c) IO State Savers库：用来保存流的当前状态，自动恢复流的状态等
                                    d) IOStreams库：扩展C++标准库流处理，建立一个流处理框架
                                    e) Program Options库：提供强大的命令行参数处理功能
                                    f) Serialization库：实现C++数据结构的持久化
                                15.跨语言混合编程库
                                    a) Python库：用于实现Python和C++对象的无缝接口和混合编程
                                16.内存管理库
                                    a) Pool库：基于简单分隔存储思想实现了一个快速、紧凑的内存池库
                                    b) Smart Ptr库：智能指针
                                    c) Utility库：小工具的集合
                                17.解析库
                                    a) Spirit库：基于EBNF范式的LL解析器框架
                                18.编程接口库
                                    a) Function库：实现一个通用的回调机制，已被收入TR1
                                    b) Parameter库：提供使用参数名来指定函数参数的机制
                                19.综合类库
                                    a) Compressed Pair库：优化的对pair对象的存储
                                    b) CRC库：实现了循环冗余校验码功能
                                    c) Date Time 库：一个非常全面灵活的日期时间库
                                    d) Exception库：针对标准库中异常类的缺陷进行强化，提供<<操作符重载，可以向异常传入任意数据
                                    e) Filesystem库：可移植的文件系统操作库，可以跨平台操作目录、文件，已被TR2接受
                                    f) Flyweight 库：实现享元模式，享元对象不可修改，只能赋值
                                    g) Lexical Cast 库：用于字符串、整数、浮点数的字面转换
                                    h) Meta State Machine库：用于表示UML2有限状态机的库
                                    i) Numeric Conversion 库：用于安全数字转换的一组函数
                                    j) Optional 库：使用容器的语义，包装了可能产生无效值的对象，实现了未初始化的概念
                                    k) Polygon 库：处理平面多边形的一些算法
                                    l) Program Options库：提供强大的命令行参数处理功能
                                    m) Scope Exit库：使用preprocessor库的预处理技术实现在退出作用域时资源自动释放
                                    n) Statechart库：提供有限自动状态机框架
                                    o) Swap库：为交换两个变量的值提供便捷方法
                                    p) System库：使用轻量级的对象封装操作系统底层的错误代码和错误信息，已被TR2接受
                                    q) Timer库：提供简易的度量时间和进度显示功能，可以用于性能测试等需要计时的任务
                                    r) Tribool库：三态布尔逻辑值，在true和false之外引入indeterminate不确定状态
                                    s) Typeof库：模拟C++0x新增加的typeof和auto关键字，以减轻变量类型声明的工作，简化代码
                                    t) Units库：实现了物理学的量纲处理
                                    u) Utility库：小工具集合
                                    v) Value Initialized库：用于保证变量在声明时被正确初始化
                                    w) Chrono库：实现了C++ 0x标准中N2661号建议 [2]  所支持的时间功能。
                                    x) Log库：实现日志功能。
                                    y) Predef库：提供一批统一兼容探测其他宏的预定义宏。 [5] 
                                20.编译器问题的变通方案库
                                    a) Compatibility库：为不符合标准库要求的环境提供帮助
                                    b) Config库：将程序的编译配置分解为三个部分：平台、编译器和标准库，帮助库开发者解决特定平台特定编译器的兼容问题
                                    
              C++经典书籍推荐
                C++ Primer
                C++ Primer Plus
                Essential C++
                Effective C++
                Thinking in C++
                The Complete C++ Training Course
                The Design and Evolution of C++
                The C++ Programming Language， Special Edition
                Inside the C++ Object Model

```

参考

https://blog.csdn.net/creator123123/article/details/82150183
引用参考
https://www.cnblogs.com/duwenxing/p/7421100.html

https://blog.csdn.net/xbb123456rt/article/details/78089517 

C++发明人书籍：
    C++程序设计语言（第1~3部分）        https://item.jd.com/11130236139.html
    C++程序设计语言（第4部分：标准库） https://item.jd.com/12034136.html
    C++程序设计：原理与实践（进阶篇）  https://item.jd.com/12173150.html
    C++程序设计语言(特别版) 
    
转义符
https://baike.baidu.com/item/%E8%BD%AC%E4%B9%89%E5%AD%97%E7%AC%A6/86397?fromtitle=%E8%BD%AC%E4%B9%89%E7%AC%A6&fromid=6151115
宏拼接
https://www.cnblogs.com/little-ant/p/3463080.html
关键字
https://baike.baidu.com/item/C%2B%2B%E5%85%B3%E9%94%AE%E5%AD%97

STL 标准模板库
https://www.cnblogs.com/yejianyong/p/7137998.html

extern
https://www.cnblogs.com/yuxingli/p/7821102.html

编译链接
https://www.cnblogs.com/kekec/p/3238741.html

boost
https://baike.baidu.com/item/boost/69144

C++ 开源框架
https://blog.csdn.net/sunjing_/article/details/79690563

学习C++从入门到精通的的十本最经典书籍
https://www.cnblogs.com/lizhigang/p/6933031.html

Linux C/C++ 编译器cc\gcc\g++\c++区别
https://blog.csdn.net/jimmyleeee/article/details/83860388

https://baike.baidu.com/item/Intel%20C++%20Compiler


