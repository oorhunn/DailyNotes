Templates in C++ are a powerful feature that allows you to write generic code, meaning that you can write a single function or class that can work with different data types. This means you do not need to write separate functions or classes for each data type you want.
### Template Functions 
This one is easy and pretty straightforward. To create a template function, you use the `template` keyword followed by the type parameters or placeholders enclosed in angle `<>` brackets. Then you define your function.
```
template <typename T>
T max(T a, Tb){
	return (a>b) ? a : b;
}
```

```
int res = max<int>(10, 20);
```

### Template Classes
```
template <typename T1, typename T2>
class Pair {
public:
    T1 first;
    T2 second;

    Pair(T1 first, T2 second) : first(first), second(second) {}
};
```
To use this class, you need to specify the type parameters when creating an object:

```
Pair<int, std::string> pair(1, "Hello");
```

### Template Specialization
[[Full Template Specialization]]
[[Partial Template Specialization]]
Sometimes, you may need special behavior for a specific data type. In this case, you can use template specialization.
```
template <>
class Pair<char, char> {
public:
    char first;
    char second;

    Pair(char first, char second) : first(first), second(second) {
        // Special behavior for characters (e.g., convert to uppercase)
        this->first = std::toupper(this->first);
        this->second = std::toupper(this->second);
    }
};
```
Now, when you create a `Pair` object with `char` template arguments, the specialized behavior will be used:

```
Pair<char, char> charPair('a', 'b');
```
