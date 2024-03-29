---
title: "C++模板例子"
date: 2023-11-02T01:05:25+08:00
tags: ["C++"]
categories: []
draft: false
toc: true
---

```cpp
#include <vector>
#include <type_traits>
using namespace std;

class AA {};
class BB {};


class Test {
public:
    template <class T, template <class> class Container, std::enable_if_t<std::is_same_v<T, int>> * = nullptr>
    void f1(Container<T> &ret);

    template<template<class> class Container>
    void f2(Container<AA> *);

    template<template<class> class Container>
    void f3(Container<BB> *);
};


template <class T, template <class> class Container, std::enable_if_t<std::is_same_v<T, int>> * = nullptr>
void Test::f1(Container<T> &ret)
{
    cout << __func__ << std::endl;
    ret.push_back(1);
//    if constexpr (std::is_same_v<int, T>) {
//        std::cout << "inst" << std::endl;
//    }
}

template <template<class> class Container>
void Test::f2(Container<AA> *c)
{
    std::cout << __func__ << std::endl;
}

template <template<class> class Container>
void Test::f3(Container<BB> *c)
{
    std::cout << __func__ << std::endl;
}

struct X {enum { value1 = false, value2 = true };};
template<class T, std::enable_if_t<T::value2, int> = 0>
void func() {
    std::cout << __func__ << std::endl;
}


int main()
{
    vector<int> vec(10);

    Test *test = new Test;
    test->template f1<int, std::vector>(vec);
    test->template f2<std::vector>(nullptr);
    test->template f3<std::vector>(nullptr);

    func<X>();
    return 0;
}
```
