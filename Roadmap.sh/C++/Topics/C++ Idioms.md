C++ idioms are well-established patterns or techniques that are commonly used in C++ programming to achieve a specific outcome. They help make code efficient, maintainable, and less error-prone.
#### Rule of Three, Five
```
#include <iostream>
// violating rule of three example
class RuleOfThree {
public:
    RuleOfThree(){
        mData = new int(0);
    }
    ~RuleOfThree(){
        delete mData;
    }
    void setValue(int value) {
        *mData = value;
    }
    int* getValue() {
        return mData;
    }
private:
    int *mData;
};
int main() {
    RuleOfThree obj1;
    obj1.setValue(42);
    RuleOfThree obj2 = obj1;
    obj1.setValue(10);
}
```
in this example if rule of three is not followed, obj2 shallow copying obj1. 
To avoid this kind of phenomena there is rule of three, five and six.
```
class MyClass {
public:
    MyClass();
    MyClass(const MyClass& other); // Copy constructor
    MyClass(MyClass&& other); // Move constructor
    MyClass& operator=(const MyClass& other); // Copy assignment operator
    MyClass& operator=(MyClass&& other); // Move assignment operator
    ~MyClass(); // Destructor
};
```

#### Resource Acquisition is Initialization (RAII)
Ensure that resources are always properly acquired and released by trying their lifetime to the lifetime of an object. When the object gets created, it acquires the resources and when it gets destroyed, it releases them.
```
class Resource {
public:
    Resource() { /* Acquire resource */ }
    ~Resource() { /* Release resource */ }
};

void function() {
    Resource r; // Resource is acquired
    // ...
} // Resource is released when r goes out of scope
```

#### Plmpl (Pointer to Implementation)
This is used to separate the implementation details of a class from its interface, resulting in faster compile times and the ability to change implementation without affecting clients.
```
// header file
class MyClass {
public:
    MyClass();
    ~MyClass();
    void someMethod();

private:
    class Impl;
    Impl* pImpl;
};

// implementation file
class MyClass::Impl {
public:
    void someMethod() { /* Implementation */ }
};

MyClass::MyClass() : pImpl(new Impl()) {}
MyClass::~MyClass() { delete pImpl; }
void MyClass::someMethod() { pImpl->someMethod(); }
```
Dunno who uses this stuff though.
#### Non-Virtual Interface(NVI)
This enforces a fixed public interface and allows subclasses to only override specific private or protected virtual methods.
```
class Base {
public:
    void publicMethod() {
        // Common behavior
        privateMethod(); // Calls overridden implementation
    }

protected:
    virtual void privateMethod() = 0; // Pure virtual method
};

class Derived : public Base {
protected:
    virtual void privateMethod() override {
        // Derived implementation
    }
};
```
#### CRTP
Curiously Recurring Template Pattern
CRTP is a C++ idiom that involves a class template being derived from its own specialization. This pattern allows for the creation of static polymorphism, which differs from regular runtime polymorphism that relies on virtual functions and inheritance. 
CRTP is usually employed when you want to customize certain behavior in the base class without adding the overhead of a virtual function call. In short, CRTP can be used for achieving compile-time polymorphism without the runtime performance cost.
```
template <typename Derived>
class Base {
public:
    void interface() {
        static_cast<Derived*>(this)->implementation();
    }

    void implementation() {
        std::cout << "Default implementation in Base" << std::endl;
    }
};

class Derived1 : public Base<Derived1> {
public:
    void implementation() {
        std::cout << "Custom implementation in Derived1" << std::endl;
    }
};

class Derived2 : public Base<Derived2> {
    // No custom implementation, so Base::implementation will be used.
};

int main() {
    Derived1 d1;
    d1.interface();  // Output: "Custom implementation in Derived1"

    Derived2 d2;
    d2.interface();  // Output: "Default implementation in Base"

    return 0;
}
```


