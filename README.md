# Knowledge base

Personnal documentation on C++ concepts and knowledge. 

## Inline functions vs. Macros

In C++, inline functions serves as compiler directive that suggests that the compiler substitute the body of a function by performing inline expansion at compile-time.

When a program executes an inline function call, the CPU directly  substitutes the function code, eliminating the need to store the memory  address of the next instruction. [^ 1]

```cpp
inline int square(int side) { return side * side; }
```

C uses macros. At compile-time, the preprocessor replaces all macro calls  within the macro code. in C++, it is recommended to always use the inline function instead of macros as they are error-prone. It is recommanded to always use inline functions instead. [^ 2]

## Virtual functions

Virtual functions are  inheritable and overridable methods. They allow for the execution of target functions that were not precisely identified at compile time. When defined in a base class, the modifier is inherited by all implementations of that method in derived class. [^ 3] Virtual functions should be accessed using a pointer or reference of base class type to achieve runtime polymorphism : 

```cpp
class A {
    public:
    	virtual void print() const =  0;
};

class B : public A {
    public:
    	void print() {
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
    	int get_a() const {
            return this->a;
        }
}

class B : public A {
    B(int i) : A(i) {
        std::cout << "Constructing B with param i: " << this->get_a() << std::endl;
    }
    ~B() override {}
    void print() override {
        std::cout << "method overriden in class B" << std::endl;
    }
    
}
```





[^ 1]: https://en.wikipedia.org/wiki/Inline_function
[^ 2]: https://www.geeksforgeeks.org/inline-functions-cpp/
[^ 3]: https://en.wikipedia.org/wiki/Virtual_function

