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
