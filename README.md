# C++ Knowledge base

Personnal documentation on C++ concepts and knowledge. 


## Destructor

Destructor destroys the class objects created by the constructor. A destructor is the last function being called before an object is destroyed.

```cpp
class A {
    private:
    	int a;
    public:
    	A(int n) : a(n) {}
    	virtual ~A() {} // <---- destructor
    	virtual void print() const = 0;
    	virtual void display() const {
            std::cout << "display function called from A" << std::endl;
        }
    	int get_a() const {
            return this->a;
        }
}

class B : public A {
    B(int i) : A(i) {
        std::cout << "Constructing B with param i: " << this->get_a() << std::endl;
    }
    ~B() override {}
    void print() const override {
        std::cout << "method overriden in class B" << std::endl;
    }
    void print() const override {
        std::cout << "display function called from B" << std::endl;
    }    
}
```



## Inline functions vs. Macros

In C++, inline functions serves as compiler directive that suggests that the compiler substitute the body of a function by performing inline expansion at compile-time.

When a program executes an inline function call, the CPU directly  substitutes the function code, eliminating the need to store the memory  address of the next instruction. [^1]

```cpp
inline int square(int side) { return side * side; }
```

C uses macros. At compile-time, the preprocessor replaces all macro calls  within the macro code. in C++, it is recommended to always use the inline function instead of macros as they are error-prone. It is recommanded to always use inline functions instead. [^2]



## Lambda

Lamdas or anonymous functions are functions definitions that are not bound to an identifier. [^4]

``` cpp
auto add = [](int x, int y) -> int { return x + y; };
int result = add(1, 2);

// capture by value
int sum = 90;
auto add = [sum] (int to_add) -> int { return sum + to_add; };
int total = add(10);

// implicit capture by value
int a=1, b=2, c=3, d=4;
auto prod = [=] () -> int { return a*b*c*d; };

// capture by reference
int ref = 2048;
auto double_it = [&ref] () -> int { ref += ref; }

// implicit capture by reference
int a = 10, b = 11, c = 12;
auto increments = [&] () -> int { ++a; ++b; ++c; }
```



## Virtual functions

Virtual functions are  inheritable and overridable methods. They allow for the execution of target functions that were not precisely identified at compile time. When defined in a base class, the modifier is inherited by all implementations of that method in derived class. [^3] Virtual functions should be accessed using a pointer or reference of base class type to achieve runtime polymorphism : 

```cpp
class A {
    public:
    	virtual void print() const =  0;
};

class B : public A {
    public:
    	void print() override const {
            cout << "method overriden in class B" << endl;
        }
};

int main() {
    
    // Creating 'b' object
    B b;
    
    // 'a' pointer store the address of b
    A *a = &b;
    
    // calling 'method' using 'a' pointer
    a->method();
    
}
```

An <u>abstract class</u> with <u>only pure virtual functions and no member variable</u> can be used to model what is called an <u>interface</u> in OOP.

## Concepts to be covered

- [x] destructor
- [ ] exceptions
- [ ] friend function
- [x] inline functions vs. macros
- [x] lambda
- [ ] objects lifetime
- [ ] operator overloading
- [ ] pointers (weak, shared, unique)
- [ ] static cast
- [ ] templates
- [ ] type casting (static, const, dynamic, reinterpret)
- [x] virtual functions

[^1]: https://en.wikipedia.org/wiki/Inline_function
[^2]: https://www.geeksforgeeks.org/inline-functions-cpp/
[^3]: https://en.wikipedia.org/wiki/Virtual_function
[^4]: https://en.wikipedia.org/wiki/Anonymous_function

