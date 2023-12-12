This occurs when you provide a specific implementation for a specific type or set of types.
### Full Template Specialization

Full specialization is used when you want to create a separate implementation of a template for a specific type. To do this, you need to use keyword `template<>` followed by the function template with the desired specialized type.

Here is an example:

```
#include <iostream>

template <typename T>
void printData(const T& data) {
    std::cout << "General template: " << data << std::endl;
}

template <>
void printData(const char* const & data) {
    std::cout << "Specialized template for const char*: " << data << std::endl;
}

int main() {
    int a = 5;
    const char* str = "Hello, world!";
    printData(a); // General template: 5
    printData(str); // Specialized template for const char*: Hello, world!
}
```