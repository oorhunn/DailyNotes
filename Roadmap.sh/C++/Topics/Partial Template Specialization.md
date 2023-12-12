Partial specialization is used when you want to create a separate implementation of a template for a subset of types that match a certain pattern or condition.

Here is an example of how you can partially specialize a template class:

```
#include <iostream>

template <typename K, typename V>
class MyPair {
public:
    MyPair(K k, V v) : key(k), value(v) {}

    void print() const {
        std::cout << "General template: key = " << key << ", value = " << value << std::endl;
    }

private:
    K key;
    V value;
};

template <typename T>
class MyPair<T, int> {
public:
    MyPair(T k, int v) : key(k), value(v) {}

    void print() const {
        std::cout << "Partial specialization for int values: key = " << key
                  << ", value = " << value << std::endl;
    }

private:
    T key;
    int value;
};

int main() {
    MyPair<double, std::string> p1(3.2, "example");
    MyPair<char, int> p2('A', 65);
    p1.print(); // General template: key = 3.2, value = example
    p2.print(); // Partial specialization for int values: key = A, value = 65
}
```

In this example, the `MyPair` template class is partially specialized to provide a different behavior when the second template parameter is of type `int`.