# Thread Coordination and Resource Management with Singletons
This code is a multi-threaded C++ program that uses the Singleton design pattern, the std::promise and std::future constructs, 
and various synchronization mechanisms. The main purpose of the code is to create and run four different threads named A, B, C, and D, 
along with a Controller thread that manages the others. The program demonstrates the use of thread-safe Singleton classes and synchronization techniques.

# Important parts of the code:

CtrlSingleton and ThrdCounter classes: These are Singleton classes that manage the resources needed for synchronization. 

Singleton design pattern ensures that there's only one instance of each class throughout the lifetime of the program.

A, B, C, and D classes: These classes inherit from BannerBase and define the behavior of each of the four threads. Each class has a constructor 
and an overloaded operator() function that takes a reference to a std::future<void> object. Inside the operator() function, 
a while loop is run until the future object is ready, and the thread performs its specific task in each iteration.

Controller class: This class also inherits from BannerBase and has an overloaded operator() function that takes a std::promise<void> object. 
This thread waits for a keypress, then sets the value for the promise object, which will signal the A, B, C, and D threads to exit their loops.

main() function: This is the entry point of the program. It creates instances of the A, B, C, D, and Controller classes, spawns the threads, and starts them. 
It also creates a std::promise and std::future pair for synchronization, and calls the _getch() function to wait for a keypress before notifying the Controller thread.

# Key points to note:

The CtrlSingleton and ThrdCounter classes utilize the Singleton pattern, ensuring only one instance of each class exists throughout the program's lifetime.
The A, B, C, and D threads are detached, meaning they can continue running even after the main thread has exited.
The Controller thread is responsible for waiting for
