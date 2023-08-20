# C++ 中的层次转换

## C++层次转换的标准中，有两种关键字

1. static_cast
2. dynamic_cast

## static_cast关键字

- 用法

```c++
static_cast <type-id> (expression)
```

- 该运算符把expression转换为type-id类型，但没有运行时类型检查来保证转换的安全性，它主要用法有如下几种用法:
  - 用于基本类型之间的转换
    - 但是这种转换需要开发者自己保证安全性，比如说`int`转换成`char`类型的话，那么static_cast只是做一个简单的截断，及简单地把int的低8位复制到char的8位中，并直接抛弃高位。
    - 把空指针转换成目标类型的空指针。
    - 把任何类型的表达式类型转换成`void`类型
    - **用于类层次结构中父类和子类之间指针和引用的转换**
      - 上行转换
        - 子类到父类
      - 下行转换
        - 父类到子类
      - 上行转换是安全的
        - 由于子类总是包含父类的所有数据成员和成员函数，因此从子类转换到父类的指针可以没有任何顾虑的访问其父类的成员
      - 下行转换是不安全的

- 实例 - 下行转换


```c++
#include <iostream>

class Shape {
    public:
        virtual void printInfo(){
            std::cout << "This is a shape." << std::endl;
        }
};

class Circle : public Shape {
    public:
        void printInfo() override 
        {
            std::cout << "This is a circle." << std::endl;
        }
};

class Rectangle : public Shape {
    public:
        void printInfo() override
        {
            std::cout << "This is a rectangle" << std::endl;
        }
};

int main()
{
    Circle circle;
    Shape* shapePtr = &circle;

    Circle* circlePtr = static_cast<Circle*>(shapePtr);

    circlePtr->printInfo();
    return 0;
}
```

- 实例-上行转换

```c++
#include <iostream>

class Shape {
    public:
        virtual void printInfo(){
            std::cout << "This is a shape." << std::endl;
        }
};

class Circle : public Shape {
    public:
        void printInfo() override 
        {
            std::cout << "This is a circle." << std::endl;
        }
};

class Rectangle : public Shape {
    public:
        void printInfo() override
        {
            std::cout << "This is a rectangle" << std::endl;
        }
};

int main()
{
    // Circle circle;
    // Shape* shapePtr = &circle;

    // Circle* circlePtr = static_cast<Circle*>(shapePtr);

    // circlePtr->printInfo();
    Rectangle rectanglePtr;

    Shape* shapePtr = static_cast<Shape*>(&rectanglePtr);
    
    shapePtr->printInfo();
    
    return 0;
}
```





## dynamic_cast关键字

- 运行时类型检查

- 基本用法与static_cast关键字的用法是一致的
- 主要用于
  - `dynamic_cast`关键字主要用于类层次结构中父类和子类之间的指针和引用的转换
  - 由于具有运行时的类型检查，因此可以保证下行转换的安全性
    - 如果转换成功，则返回转换后的正确类型的指针
    - 如果转化失败，则返回NULL（如果是在static_cast中，转换失败也不返回null）
- 实例

```c++
#include <iostream>

class Shape {
    public:
        virtual void printInfo() 
        {
            std::cout << "This is a shape. " << std::endl;
        }
};

class Circle : public Shape {
    public:
        void printInfo() override
        {
            std::cout << "This is a circle. " << std::endl;
        }
};

class Rectangle : public Shape {
    public:
        void printInfo() override
        {
            std::cout << "This is a rectangle. " << std::endl;
        } 
};

int main(){
    Shape* shapePtr = new Circle;

    Circle* cirlePtr = dynamic_cast<Circle*>(shapePtr);

    if (cirlePtr)
    {
        cirlePtr->printInfo();
    }
    else
    {
        std::cout << "Dynamic cast failed." << std::endl;
    }

    delete shapePtr;

    return 0;
}
```

