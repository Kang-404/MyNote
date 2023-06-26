### 不要返回局部对象的引用或指针
函数终止意味着局部变量的引用将指向不再有效的内存区域
``` C++
// 严重错误：这个函数试图返回局部对象的引用
const std::string &manip(){
    std::string ret;
    // 以某种方式改变一下 ret
    if(!ret.empty())
        return ret; // error: 返回局部对象的引用！
    else
        return "Empty"; // error: "Empty"是一个局部临时量
}
```

### 引用返回左值
函数的返回类型决定函数调用是否是左值。   
* 调用一个返回引用的函数得到左值，其他返回类型得到右值。可以想使用其它啊左值那样来使用返回引用的函数的调用。
* 可以为返回类似为非常量引用的函数结果赋值。
* 如果返回类型是**常量引用**，不能给调用的结果赋值。

``` C++
#include <iostream>

using std::cout;
using std::endl;
using std::string;

char &get_val(string &str, string::size_type ix){
    return str[ix];
}

int main(){
    string s("a value");
    cout << s << endl;
    get_val(s, 0) = 'A';
    cout << s << endl;
}
```
### 列表初始化返回值
函数可以返回花括号包围的列表，此处的列表也用来对表示返回的临时量进行初始化。
* 若列表为空，临时量执行***值初始化***；否则返回的值由函数的返回类型决定。
> - 默认初始化：如果T是一个类，那么调用默认构造函数进行初始化；如果是一个数组，每个元素默认初始化；除了前面的情况之外，不进行初始化，其值未定义。至于合成的默认构造函数初始化数据成员的规则是：1.如果类数据成员存在类内初始值，则用该值初始化相应成员（c++11）；2.否则，默认初始化数据成员。 [参考链接](http://en.cppreference.com/w/cpp/language/default_initialization)  
> - 值初始化：如果T是一个类，那么类的对象进行默认初始化(如果T类型的默认构造函数不是用户自定义的，默认初始化之前先进行零初始化)；如果是一个数组，每个元素值初始化，否则进行零初始化。  [参考链接](http://en.cppreference.com/w/cpp/language/value_initialization)
> - 零初始化：对于static或者thread_local变量将会在其他类型的初始化之前先初始化。如果T是算数、指针、枚举类型，将会初始化为0；如果是类类型，基类和数据成员会零初始化；如果是数组，数组元素也零初始化。 [参考链接](https://en.cppreference.com/w/cpp/language/zero_initialization)

### 返回数组指针
数组不能被拷贝，所以函数不能返回数组。
- 想要定义一个返回数组的指针或引用的函数可以使用类型别名。
    ``` C++
    typedef int arrT[10];   // arrT 是一个类型别名，表示含有10个整数的数组
    using arrT = int[10];   // arrT 的等价声明
    arrT* func(int i);      // func 返回一个指向含有10个整数数组的指针
    ```
- 声明一个返回数组指针的函数`Type (*function(parameter_list)) [dimension]`   
    ``` C++
    int (*func(int i))[10];
    ```      
    - `func(int i)`
    - `(*func(int i))`
    - `(*func(int i)) [10]`
    - `int (*func(int i)) [10]`
- 使用尾置返回类型
    `auto func(int i) -> int(*) [10];`
- 使用 decltype 
    如果知道函数返回的指针将指向哪个数组，可以使用`decltype`关键字声明返回类型
    ``` C++
    int odd[] = {1, 3, 5, 7, 9};
    int even[] = {2, 4, 6, 8, 10};
    decltype(odd) *arrPtr(int i){
        return (i % 2) ? &odd : &even;
    }
    ```
    decltype 的结果是个数组，想要表示 arrPtr 返回指针还必须在函数声明时加一个 * 符号。
