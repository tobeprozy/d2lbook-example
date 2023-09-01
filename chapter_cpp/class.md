# Class

## template

### 基本功能

#### 一、函数模板--用于不同的数据类型

```c++
#include <iostream>

// 定义一个函数模板
template <typename T>
T add(T a, T b) {
    return a + b;
}

int main() {
    // 调用函数模板，编译器会根据实参的类型自动生成对应的函数
    int result1 = add(5, 10);
    double result2 = add(3.14, 2.71);

    std::cout << "Result 1: " << result1 << std::endl;
    std::cout << "Result 2: " << result2 << std::endl;

    return 0;
}
```

#### 二、类模板-创建不同类型的对象

```c++
#include <iostream>
// 定义一个类模板
template <typename T>
class MyClass {
public:
    void printType() {
        std::cout << "Type: Unknown" << std::endl;
    }
};

// 类模板的特化，针对特定类型提供定制的实现
template <>
class MyClass<int> {
public:
    void printType() {
        std::cout << "Type: Integer" << std::endl;
    }
};

int main() {
    MyClass<float> obj1;
    MyClass<int> obj2;

    obj1.printType(); // 输出: Type: Unknown
    obj2.printType(); // 输出: Type: Integer

    return 0;
}
```

#### 三、类的特化-用于类的不同实现

```c++
#include <iostream>

// 定义一个类模板
template <typename T>
class MyClass {
public:
    void printType() {
        std::cout << "Type: Unknown" << std::endl;
    }
};

// 类模板的特化，针对特定类型提供定制的实现
template <>
class MyClass<int> {
public:
    void printType() {
        std::cout << "Type: Integer" << std::endl;
    }
};

int main() {
    MyClass<float> obj1;
    MyClass<int> obj2;

    obj1.printType(); // 输出: Type: Unknown
    obj2.printType(); // 输出: Type: Integer

    return 0;
}
```

