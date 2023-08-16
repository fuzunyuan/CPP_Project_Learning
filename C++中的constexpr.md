# C++中的constexpr

- C++中，关键字`constexpr`用于声明一个表达式函数或函数在编译时求值的。
- 也就是说在程序的编译阶段就可以得出结果，而不是在运行的时候再产生结果。
- 它的主要目的是在编译时优化，从而提高代码的性能和效率。

## constexpr用于以下两个方面

1. 常量表达式的声明
2. 函数的声明

## constexpr的实例

- 使用constexpr实现的代码

```c++
#include <iostream>

constexpr int fact(int n){
    return (n <= 1) ? 1 : n * fact(n - 1);
}

int main(){
    constexpr int n = 6;
    constexpr int result = fact(n);

    std::cout << "Fact of " << n << " is: " <<result << std::endl;

    return 0; 
}
```

- 使用普通写法的实现相同功能的代码

```c++
#include <iostream>

int fact(int n){
    if (n <= 1) return 1;
    else
    {
        return n * fact(n - 1);
    }
}

int main(){
    int n = 6;
    int result = fact(n);

    std::cout << "fact of " << n << " is : " << result << std::endl;
    
    return 0;
}
```

- 两者的区别和不同之处
  - 第一种代码使用了`constexpr`，这表明在编译时就会计算阶乘的结果，这意味着，在编译的过程中，编译器会展开递归调用，从而生成一个编译时常量，这个常量在程序运行的时候就已经计算好了。这种方式在运行时只需要执行一个简单的赋值操作，因此在性能上就非常的高效。
  - 第二种代码并没有使用`constexpr`，那么每次函数调用都会在运行时进行，直到达到递归基准情况。这会导致多次函数调用和递归操作，从而造成一些运行时开销。
  - 很明显时间复杂度都为O(n)，但是第一种方法是编译时就已经计算好了，所以速度会更快一些。

