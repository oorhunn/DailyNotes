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


