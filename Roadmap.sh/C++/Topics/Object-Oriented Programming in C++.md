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
Check it:
[[Diamond Inheritance]] 

#### Polymorphism
[[Static Polymorphism]]
[[Dynamic Polymorphism]]
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
