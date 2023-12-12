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
