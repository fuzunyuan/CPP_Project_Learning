# C++中的模板函数

## 一个简单的例子

- 当声明一个C++模板函数时，需要指定一个或者多个模板参数，并使用这些参数来定义函数的参数和返回类型。
- 比如说下面这个例子：

```c++
#include <iostream>

template <typename T>
T add(T a,T b);

int main(){
    int result1 = add(5,3);
    double result2 = add(2.5,1.5);

    std::cout << "Result 1 :" << result1 << std::endl;
    std::cout << "Result 2 :" << result2 << std::endl;

    return 0;
}

template <typename T>
T add(T a,T b){
    return a + b;
}
```

- 在这个实例中，我们声明一个名为`add`的模板函数。有一个模板参数`typename T`,表示这个函数可以接受任何类型的参数。
- 然后我们在主函数中使用这个模板函数两次，一次使用整数参数，另一次使用双精度参数。
- 模板函数允许你用一种通用的方式编写代码，使其适用于多种数据类型。

## C++模板详解

- 模板是C++支持参数化多态的工具，使用模板可以使用用户或者函数声明一种一般模式，使得类中的某些数据或者成员函数的参数、返回值取得任意类型。
- 模板是一种对类型进行参数化的工具
- 通常包含两种方式：
  - 函数模板
  - 类模板
- 函数模板针对 **仅参数类型不同的** 函数
- 类模板针对 **仅数据成员和成员函数类型不同的** 函数
- 使用模板的目的就是能够让程序员编写与类型无关的代码。

### 函数模板通式

```c++
template <class 形参名,class 形参名, ...> 返回类型  函数名(参数列表)
{
    函数体;
}
```

- class 关键字可以使用typename关键字进行代替。
- 不能在函数调用的参数中指定模板形参的类型，对函数模板的调用应该使用实参推演来进行。

### 类模板通式

```c++
template<class T>
    class A
    {
        public:
        	T a;
        	T b;
        	T hy(T c,T &d); 
    };
```

- 在类A中声明了两个类型为T的成员变量a和b，还声明了一个返回类型为T带两个参数类型为T的函数hy

#### 类模板对象的创建

- 比如一个模板类A，则使用类模板创建对象的方法为A<int> m;
- 在类后面跟上一个尖括号并在里面填上相应的类型，这样的话类A中凡是用到模板形参的地方都会被int所代替。
- 当类模板有两个模板形参时创建对象的方法为A<int, double> m，**类型之间用逗号隔开。**
- **注意事项：**
  - 模板形参的类型必须在类名后的尖括号中明确指定。
  - 比如A<2> m；用这种方法把模板形参设置为int是错误的，**类模板形参不存在实参推演的问题。**
  - **也就是说不能把整型2推演为int型传给模板形参，要把类模板形参调置int，也就是必须是这种形式A<int> m;  **

#### 在类模板外部定义成员函数的方法为:

- 在类模板外部定义成员函数的方法为:

```c++
template <模板形参列表> 函数返回类型 类名<模板形参名>::函数名(参数列表)
{
    函数体
}
```

- 例如以下例子:

```c++
template <class T1,class T2> void A<T1,T2>::h(){
    
}
```

- 当在类外面定义类的成员的时候，template后面的模板形参应该与要定义的类的模板形参一致。

#### 实例

```c++
#include <iostream>
#include <vector>

template <typename T>
class Stack{
    private:
        std::vector<T> data;
    public:
        void push(const T& value){
            data.push_back(value);
        }  

        T pop(){
            if (!data.empty())
            {
                T vaule = data.back();
                data.pop_back();
                return vaule;
            }
            else
            {
                throw std::runtime_error("Stach is empty");
            }
        }

        bool empty() const{
            return data.empty();
        }
};

int main(){
    //实例化整数型类型的栈
    Stack<int> intStack;
    intStack.push(5);
    intStack.push(10);
    std::cout << "Popped value : " << intStack.pop() << std::endl;

    // 实例化双精度浮点数类型的栈
    Stack<double> doubleStack;
    doubleStack.push(3.14);
    doubleStack.push(1.23);
    std::cout << "Popped value : " << doubleStack.pop() << std::endl;

    return 0;
}
```



