# C_reviewr
Macro Substitution

Conditional Inclusion


对数组而言，const 限定符指定数组所有元素的值都不能被修改   
const 限定符也可配合数组参数使用，它表明函数不能修改数组元素的值：
``` C
int strlen(const char[]);
```   
如果试图修改 const 限定符限定的值，其结果取决于具体的实现。   


类型转换   
C 语言中，很多情况下会进行隐式的算术类型转换。一般来说，如果二元运算符（具有两
个操作数的运算符称为二元运算符，比如+或*）的两个操作数具有不同的类型，那么在进行
运算之前先要  ***把“较低”的类型提升为“较高”的类型***  ，运算的**结果为较高的类型**。