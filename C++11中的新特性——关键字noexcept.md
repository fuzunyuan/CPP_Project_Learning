# C++11中的新特性——关键字noexcept

## 关键字noexcept

- 从C++11开始，我们能看到很多代码里面都有关键字noexcept。例如以下代码：

```c++
#include <iostream>

void performSafeDivision(int numerator,int denominator) noexcept{

    if (denominator == 0)
    {
        std::cerr << "Error : Division by zero is not allowed." << std::endl;
        return;
    }
    int result = numerator / denominator;
    std::cout << "Result of division: " << result << std::endl;

}

int main(){
    performSafeDivision(10,2);
    performSafeDivision(5,0);

    return 0;
}
```

- 这段代码的意思就是告诉编译器这个函数不会抛出异常，这有利于编译器对程序做出更多的优化。
- 很明显在主函数中，第一行代码是正常运行的，第二行代码是会出现错误的
- 那么在执行第二行的时候，noexcept函数向外抛出了异常，程序会直接终止，调用std::terminate() 函数，这几个函数内部会调用std::abort()终止程序。





