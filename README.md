# C++14
## Features of C++ 14
### 1. Generic lambdas
A lambda is a concise way to define an anonymous function (closure) directly at the point where it is called or passed as an argument to a function. Typically, they are used to encapsulate short pieces of code that are passed to algorithms, where the code is not intended for reuse.

Let’s say we create a lambda function to return the sum of two integers. The lambda function would look like this:
```c++
[](int a, int b) -> int { return a + b; }
```

But what if we needed to calculate the sum of two floating-point values later? In that case, we would need to create a new lambda expression for double values. 
Similarly, whenever the input types changed, the lambda function would have to be rewritten.

```c++
[](double a, double b) -> double { return a + b; }
```
C++14 eliminates this issue by allowing the use of the auto keyword in the input parameters of a lambda expression. This enables the compiler to deduce the parameter types at compile time. Therefore, in our previous example, a single lambda expression that works for both integer and floating-point values would look like this:

```c++
auto sum = [](auto a, auto b) { return a + b; };
```

### 2. Return Type deduction for functions
Let us consider the function template has at least two type parameters as mentioned below:
```c++
template <typename T, typename T2>
??? sum(T a, T2 b) {
    return a + b;
}
```
When a function template has at least two type parameters, the return type cannot always be determined automatically. However, in the case of sum, the return type should match the type produced by the arithmetic operation a + b.
In C++11 we can solve this by using auto in Combination with decltype.

```c++
template <typename T, typename T2>
auto sum(T a, T2 b) -> decltype(a + b) {
    return a + b;
}
```

Using auto indicates that you don't know the type upfront and will specify it later. This specification is done using the decltype expression: decltype(a + b). 
The return type of the function template sum will be the type that the arithmetic expression evaluates to. 
However, you have to use the same expression, a + b, twice. This can be error-prone and redundant.

From C++14 onwards 
```c++
template <typename T, typename T2>
auto sum(T t, T2 t2) {
    return t + t2;
}
```
### 2. Variable template

Parametrized variables were commonly implemented using either static data members within class templates or constexpr function templates that returned the desired values.

Starting from C++14, variable templates provide a way to create parameterized variables, making it easier for programmers to define constants and use them with different data types.

```c++
// declaring thhe variable template
template <class T> constexpr T pi = T(3.1414);

//Usage
int int_pi = pi<int>; 
double double_pi = pi<double>;

Note: A variable created from a variable template is referred to as an instantiated variable.

```

Variable templates in classes are used to declare static data member templates.

Before variable templates, static variables in a class template were parameterized as shown below:

```cpp
template<class T>
class X {
    static T s; // declaration of a non-template static data member in a class template
};
```

With the introduction of variable templates in C++14, there's no longer a need to make the entire class a template. Instead, you can declare static data member templates like this:

```cpp
class X {
    template<typename T>
    static const T s; // declaration of a static data member template
};
```




