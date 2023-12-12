Multithreading is the concurrent execution of multiple threads within a single process or program. It improves the performance and efficiency of an application by allowing multiple tasks to be executed in parallel.

#### Basic Thread Creation
```
#include <thread>
void my_function() {
	std::cout << "thread stuff \n";
}
int main() {
	std::thread t(my_funcion);
	t.join();
	return 0;
}
```

#### Thread with Arguments
```
void print_sum(int a, int b) {
    std::cout << "The sum is: " << a + b << std::endl;
}

int main() {
    std::thread t(print_sum, 3, 5);
    t.join();
    return 0;
}
```

#### Mutex and Locks
```
#include <iostream>
#include <mutex>
#include <thread>

std::mutex mtx;

void print_block(int n, char c) {
    {
        std::unique_lock<std::mutex> locker(mtx);
        for (int i = 0; i < n; ++i) {
            std::cout << c;
        }
        std::cout << std::endl;
    }
}

int main() {
    std::thread t1(print_block, 50, '*');
    std::thread t2(print_block, 50, '$');

    t1.join();
    t2.join();

    return 0;
}
