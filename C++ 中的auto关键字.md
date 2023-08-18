# C++ 中的auto关键字

- 在C++中，`auto` 是一个关键字，用于自动推断变量的数据类型。
- 它在编译的时候，根据初始化表达式的类型推断变量的数据类型，从而使代码更加简介和灵活

## 变量的初始化和声明

- 在声明变量的时候，可以使用`auto` 关键字来自动推断变量的数据类型。
- 编译器会根据初始化的值来确定变量的数据类型。
- 以下是一个实例:

```c++
#include <iostream>
#include <string>

int main(){
    auto x = 10;
    auto name = "John";
    auto pi = 3.14159;

    std::cout << "x: " << x << ",name = " << name << ",pi = " << pi << std::endl;

    return 0;
}
```

## 迭代器和范围循环

- 在循环中使用`auto` 关键字可以自动推断迭代器或循环范围中的元素类型，使代码更加的简洁。
- 以下是一个实例：

```c++
#include <iostream>
#include <vector>

int main(){
    std::vector<int> numbers = {1,2,3,4,5};

    // 使用auto推断迭代器的类型
    for (auto it = numbers.begin();it != numbers.end();it++)
    {
        std::cout << *it << " ";
    }

    std::cout << std::endl;

    // 使用auto推断元素的类型
    for (auto num : numbers)
    {
        std::cout <<  num << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

## 函数返回值类型

- 在函数类型中，可以使用`auto`关键字来推断函数返回值的类型。这样可以避免显式指定函数返回值类型，**特别是当返回类型较为复杂或与表达式密切相关时。**
- 以下是一个实例:

```c++
#include <iostream>

auto add(int a,int b)
{
    return a + b;
}

auto getValue(bool someCodition){
    if (someCodition)
    {
        return 42;
    }
    else
    {
        return 3;
    }
}

int main(){
    int sum = add(5,7);
    std::cout << "Sum : " << sum << std::endl;

    std::cout << "Value : " << getValue(true) << std::endl;

    std::cout << "Value : " << getValue(false) << std::endl;

    return 0;
}
```



