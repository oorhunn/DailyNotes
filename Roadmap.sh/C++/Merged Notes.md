### Data Types

- float 4 bytes 
- double 8 bytes
- char 1 byte
- bool  1 byte 
- **Arrays**: 
``` 
int numbers[5] = {1, 2, 3, 4, 5};
```

- **Pointers**: Pointers are used to store the memory address of a variable.
```
int num = 42;
int* pNum = &num;
```

- **References**: References are an alternative way to share memory locations between variables, allowing you to create an alias for another variable.
```
int num = 42;
int& numRef = num;
```

- **Structures**:
Structures are used to store different data types under a single variable and accessibility of member variables and methos are PUBLIC.

```
struct Person {
	string name;
	int age;
	float height; 
};
Person p1 = {"John Doe", 31, 5.9};
```

- **Classes**:  
Classes are similar to structures, but the accessibility of the member data and function are governed by access specifiers. By default access to members of a class is private.

```
class Person { 
public:
	string name;
	int age;
	void printInfo() {
		cout << name << age << endl;
	};
};

Person p1;
p1.name = "John Doe";
p1.age = 31;
```

- **Unions**:
Unions are used to store different data types in the same memory location.

```
union Data {
	int num;
	char letter;
	float decimal;
};
Data myData;
myData.num = 42;
```





### Pointers 
```
struct node {
    int data;
    struct node *next;
};

typedef struct node Node;

Node *head = nullptr;
Node *tail = nullptr;

void link(int data) {
    Node *temp = new Node;
    temp->data = data;
    temp->next = nullptr;
    if (head == nullptr) {
        head = temp;
        tail = temp;        
    }
    else {
        tail->next = temp;
        tail = temp;
    }
    return;
}

  
void print_links() {
    Node *track = head;

    while (track != nullptr){
        cout << track->data<< endl;
        track = track->next;
    }
    return;
}

int main() {
    link(12);
    link(31);

    print_links();
    return 0;
}
```

### Memory Model in C++
The memory model in C++ defines how the program stores and accesses data in computer memory. It consists of different segments, such as the Stack, Heap, Data and Code segments.
#### Stack Memory
Stack memory is used for automatic storage duration variables, such as local variables and function call data. Stack memory is managed by the compiler, and its allocation and deallocation are done automatically. The stack memory is also a LIFO data structure.

#### Heap Memory 
Heap memory is used for dynamic storage duration variables, such as objects created using the `new` keyword. The programmer has control over the allocation and deallocation of heap memory using `new` and `delete` operators. Heap memory is a larger pool of memory than  the stack, but has a slower access time.

#### Data Segment
The Data segment is composed of two parts: the initialized data segment and the uninitialized data segment. The initialized data segment stores global, static and constant variables with initial values, whereas the uninitialized segment stores uninitialized global and static variables.

#### Code Segment 
The Code segment also known as the text segment stores the executable code (machine code) of the program. It usually located in a read-only area of memory to prevent accidental modification.

### Object Lifetime in C++
- **Static Storage Duration:** Objects with static storage duration exist for the entire run of the program. These objects are allocated at the beginning of the programs run and deallocated when the program terminates. Global variables, static data members and static local variables fall into this category.
```
int global_var; // static storage duration
class MyClass {
	static int static_var; // static storage duration
};
void myFunction() {
	static int local_var; // static storage duration
}
```

- **Thread Storage Duration:**  Objects with thread storage duration exist for the lifetime of the thread they belong to. Can be specified using the `thread_local` keyword.
```
thread_local in my_var; // thread storage duration
```

- **Automatic Storage Duration:** Objects with automatic storage duration are created at the point of definition and destroyed when the scope in which the are declared is exited. These objects are also known as local or stack objects.
- **Dynamic Storage Duration:** Objects with dynamic storage are created at runtime, using memory allocation functions such as `new`. Its the programmers responsibility to destroy the objects using `delete` to avoid memory leaks.
```
int *ptr = new int;
delete ptr;
```



### Diamond Inheritance
Diamond inheritance is a specific scenario in multiple inheritance where a class is derived from two or more classes, which in turn, are derived from a common base class. It creates an ambiguity that arises from duplicating the common base class, which leads to an ambiguous behavior while calling the duplicate members.
To resolve this ambiguity, you can use virtual inheritance. A virtual base class is a class that is shared by multiple classes using `virtual` keyword in C++. This ensures that only one copy of the base class is inherited in the final derived class, and thus, resolves the diamond inheritance problem.
*Example:*
```
#include <iostream>

class Base {
public:
    void print() {
        std::cout << "Base class" << std::endl;
    }
};

class Derived1 : virtual public Base {
public:
    void derived1Print() {
        std::cout << "Derived1 class" << std::endl;
    }
};

class Derived2 : virtual public Base {
public:
    void derived2Print() {
        std::cout << "Derived2 class" << std::endl;
    }
};

class Derived3 : public Derived1, public Derived2 {
public:
    void derived3Print() {
        std::cout << "Derived3 class" << std::endl;
    }
};

int main() {
    Derived3 d3;
    d3.print(); // Now, there is no ambiguity in calling the base class function
    d3.derived1Print();
    d3.derived2Print();
    d3.derived3Print();

    return 0;
}

```

### Object-Oriented Programming in C++
#### Classes 
```
class Dog {
public:
	string name;
	int age;
	void bark() {
		cout << name << "barks" << endl;
	}
} 
```
#### Encapsulation
Encapsulation is the concept of bundling data and functions that operate on that data within a single unit. In C++ you can use access specifiers like `public`, `private`, and `protected` to control the visibility and accessibility of class members.

#### Inheritance
```
class Animal {
public:
	void breathe() {
		cout << " i breathe" << endl;
	}
};

class Dog : public Animal {
public:
	void bark() {
		cout << "dog barks" << endl;
	}
}
```
In this example, the `Dog` class inherits from the `Animal` class so the `Dog` class can access the `breathe` function from the `Animal` class. When you create a `Dog` object, you can use both `breathe` and `bark` functions.

#### Polymorphism
```
class Animal {
public:
    virtual void makeSound() {
        std::cout << "The Animal makes a sound" << std::endl;
    }
};

class Dog : public Animal {
public:
    void makeSound() override {
        std::cout << "Dog barks!" << std::endl;
    }
};

class Cat : public Animal {
public:
    void makeSound() override {
        std::cout << "Cat meows!" << std::endl;
    }
};
```

```
Animal *animals[2] = {new Dog, new Cat};
animals[0]->makeSound(); // Output: Dog barks!
animals[1]->makeSound(); // Output: Cat meows!
```



### Static Polymorphism
Static polymorphism, also known as compile-time polymorphism, is a type of polymorphism that resolves the types and method calls at compile time rather than at runtime. This commonly achieved through the use of function **overloading** and **templates** in C++. 
#### Templates 
```
#include <iostream>

// Template function to print any type
template<typename T>
void print(const T& value) {
    std::cout << "Printing value: " << value << std::endl;
}

int main() {
    print(42);           // int
    print(3.14159);      // double
    print("Hello");      // const char*

    return 0;
}
```

### Dynamic Polymorphism
Dynamic polymorphism is a programming concept in object-oriented languages like C++ where a derived class can override or redefine methods of its base class. This means that a single method call can have different implementations based on the type of object it is called on.

Dynamic polymorphism is achieved through **virtual functions**, which are member functions of a base class marked with the `virtual` keyword.
```
#include <iostream>

// Base class
class Shape {
public:
    virtual void draw() {
        std::cout << "Drawing a shape" << std::endl; 
    }
};

// Derived class 1
class Circle : public Shape {
public:
    void draw() override {
        std::cout << "Drawing a circle" << std::endl; 
    }
};

// Derived class 2
class Rectangle : public Shape {
public:
    void draw() override {
        std::cout << "Drawing a rectangle" << std::endl;
    }
};

int main() {
    Shape* shape;
    Circle circle;
    Rectangle rectangle;

    // Storing the address of circle
    shape = &circle;

    // Call circle draw function
    shape->draw();

    // Storing the address of rectangle
    shape = &rectangle;

    // Call rectangle draw function
    shape->draw();

    return 0;
}
```
Output will be like:
```
Drawing a circle
Drawing a rectangle
```

### SOLID Principles

SOLID is an acronym that represents a set of five design principles for writing maintainable and scalable software.
### C++ Containers
#### 1.) Vector
Vectors are dynamic arrays that can resize themselves as needed. They store elements in a contiguous memory location.
```
std::vector<int> vec = {1, 2, 3, 4, 5};

vec.push_back(6); // Add an element to the end

std::cout << "Vector contains:";
for (int x : vec) {
	std::cout << ' ' << x;
}
```

#### 2.) List
A list is a doubly-linked list that allows elements to be inserted or removed from any position in constant time.
```
std::list<int> lst = {1, 2, 3, 4, 5};
```

#### 3.) Map
A map is an associative container that stores key-value pairs. It supports the retrieval of values based on their keys. The keys are sorted in ascending order by default.
```
std::map<std::string, int> m;

m["one"] = 1;
m["two"] = 2;
```

#### 4.) Unordered_map
Similar to a map, an unordered map stores key-value pairs, but it is implemented using a hash table. This means unordered map has faster average-case performance compared to map.
```
std::unordered_map<std::string, int> um;
```

### Compilers
A compiler is a computer program that translates source code written in one programming language into a different language, usually machine code or assembly. 
It is essential to know that they work closely with the linker and the standard library. The linker takes care of combining compiled object files and libraries into a single executable, while the standard library provides implementations for common functionalities used in your code.

#### Stages of Compilation in C++
The process of compilation in C++ can be divided into four primary stages: Preprocessing, compilation, assembly, and linking.

**Preprocessing:** Preprocessors modify the source code before the actual compilation process. They handle directives that start with `#` symbol like `#define` , `#include` , and `#if` . In this stage, included header files are expanded, macros are replaced , and conditional compilation statements are processed. 

**Compilation:** The compiler translates the modified source code into an intermediate representation, usually specific to the target processor architecture. This step also involves performing syntax checking, semantic analysis, and producing error messages for and issues encountered in the source code.

**Assembly:** This stage generates assembly code using mnemonics and syntax that is specific to the target processor architecture. Assemblers then convert this assembly code into object code.

**Linking:** The final stage is the linking of the object code with the necessary libraries and other object files. The linker merges multiple object files and libraries, resolves external references from other modules or libraries, allocates memory addresses for functions and variables, and generates an executable file that can be run on the target platform.

### Build Systems in C++
A build system is a collection of tools and utilities that automate the process of compiling, linking, and executing source code files in a project. The primary goal of build systems is to manage the complexity of the compilation process and produce a build in the end.

#### CMake
```
cmake_minimum_required(VERSION 3.0)

project(MyProject)

set(SRC_DIR "${CMAKE_CURRENT_LIST_DIR}/src")
set(SOURCES "${SRC_DIR}/main.cpp" "${SRC_DIR}/file1.cpp" "${SRC_DIR}/file2.cpp")

add_executable(${PROJECT_NAME} ${SOURCES})

target_include_directories(${PROJECT_NAME} PRIVATE "${CMAKE_CURRENT_LIST_DIR}/include")

set_target_properties(${PROJECT_NAME} PROPERTIES
    CXX_STANDARD 14
    CXX_STANDARD_REQUIRED ON
    CXX_EXTENSIONS OFF
)
```

### Package Managers
Some popular package managers used in the C++ ecosystem include:
	- Conan
	- vcpkg
	- C++ Archive Network (cppan)

### Working with Libraries in C++
In C++ libraries can be either static libraries (.lib) or dynamic libraries (.dll).

#### 1.) Static Libraries
Static libraries are incorporated into your program during compile time. They are linked with your code, creating a larger executable file, but it does not require any external files during runtime. 

#### 2.) Dynamic Libraries
Dynamic libraries are loaded during runtime, which means that your executable file only contains references to these libraries. The libraries need to be available on the system where your program is running.

### C++ Idioms

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

### STL Algorithms
The Standard Template Library (STL) in C++ provides a collection of generic algorithms that are designed to work with various container classes. These algorithms are implemented as functions and can be applied to different data structures, such as arrays, vectors, lists, and others. The primary header file for algorithms is `<algorithm>`.

#### std::sort
It is used to sort a range of elements `[first, last)` in non descending order by defualt.
```
std::vector<int> nums = {10, 9, 8, 7, 6, 5};
std::sort(nums.begin(), nums.end());
```
#### std::find
```
std::vector<int> nums = {5, 6, 7, 8, 9, 10};
auto it = std::find(nums.begin(), nums.end(), 9);

if (it != nums.end()) {
	std::cout << "Found 9 at position: " << (it - nums.begin());
} else {
	std::cout << "9 not found";
}
```
#### std::remove
```
std::vector<int> nums = {5, 6, 7, 6, 8, 6, 9, 6, 10};
nums.erase(std::remove(nums.begin(), nums.end(), 6), nums.end());
```

### Multithreading in C++
Multithreading is the concurrent execution of multiple threads within a single process or program. It improves the performance and efficiency of an application by allowing multiple tasks to be executed in parallel.

#### Basic Thread Creation
```
#include <thread>
void my_function() {
	std::cout << "thread stuff \n";
}
int main() {
	std::thread t(my_funcion);
	t.join();
	return 0;
}
```

#### Thread with Arguments
```
void print_sum(int a, int b) {
    std::cout << "The sum is: " << a + b << std::endl;
}

int main() {
    std::thread t(print_sum, 3, 5);
    t.join();
    return 0;
}
```

#### Mutex and Locks
```
#include <iostream>
#include <mutex>
#include <thread>

std::mutex mtx;

void print_block(int n, char c) {
    {
        std::unique_lock<std::mutex> locker(mtx);
        for (int i = 0; i < n; ++i) {
            std::cout << c;
        }
        std::cout << std::endl;
    }
}

int main() {
    std::thread t1(print_block, 50, '*');
    std::thread t2(print_block, 50, '$');

    t1.join();
    t2.join();

    return 0;
}
```



### Iterators
Iterators are object in the C++ Standard Library that help us traverse containers like arrays, lists, and vectors. Essentially, they act as a bridge between container classes and algorithms. Iterators behave similar to pointers but provide more generalized and abstract way of accessing elements in a container.

For most cases, you would want to start with the `auto` keyword and the appropriate methods like `begin()` and `emd()` to work with iterators.
```
std::vector<int> nums = {1, 2, 3, 4};
for (auto itr = nums.begin(); itr != nums.end(); ++itr) {
    std::cout << *itr << " ";
}
```
Other than that there is iterators like forward, backward, and bidirectional.
### Dynamic Typing in C++

#### `void*` Pointers
Void pointer is a generic pointer that can point to objects of any data type. They can be used to store a reference to any type of object without knowing the specific type of the object.

```
void* void_ptr;
int x = 42;
void_ptr = &x;
float y = 2.1;
void_ptr = &y;
```

#### `std::any` 
C++17 introduced the `std::any` class which represents a generalized type-safe container for single values of any type.
```
#include <any>
std::any any_value;
any_value = 42;
std::cout << std::any_cast<int>(any_value)
```

`any` keyword supports type-checking at runtime and does not require explicit casting when retrieving the stored value. It provides a safer and more convenient alternative to using `void*` , as it avoids the need for manual casting and allows better type safety.


