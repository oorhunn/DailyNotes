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

