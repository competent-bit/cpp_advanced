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
