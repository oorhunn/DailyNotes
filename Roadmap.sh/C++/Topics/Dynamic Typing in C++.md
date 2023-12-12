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