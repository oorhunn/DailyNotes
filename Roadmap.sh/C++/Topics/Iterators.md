Iterators are object in the C++ Standard Library that help us traverse containers like arrays, lists, and vectors. Essentially, they act as a bridge between container classes and algorithms. Iterators behave similar to pointers but provide more generalized and abstract way of accessing elements in a container.

For most cases, you would want to start with the `auto` keyword and the appropriate methods like `begin()` and `emd()` to work with iterators.
```
std::vector<int> nums = {1, 2, 3, 4};
for (auto itr = nums.begin(); itr != nums.end(); ++itr) {
    std::cout << *itr << " ";
}
```
Other than that there is iterators like forward, backward, and bidirectional.