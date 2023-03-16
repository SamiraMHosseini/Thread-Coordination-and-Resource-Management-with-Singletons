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
The Singleton pattern ensures that a class has only one instance and provides a global point of access to that instance. 
It is particularly useful when you need to coordinate actions across multiple threads or objects.

In this code, the CtrlSingleton and ThrdCounter classes are implemented as Singletons, ensuring that only one instance of each class is created throughout the program. The methods GetInstance() in both classes are responsible for creating and returning the unique instances.

The Singleton pattern is used here to manage shared resources (mutex and condition variables) and to coordinate the execution of threads in a synchronized manner. By using the Singleton pattern, the code ensures that all threads interact with the same instance of the CtrlSingleton and ThrdCounter classes, providing a consistent and controlled way of managing synchronization and thread coordination.

However, it is worth noting that the Singleton pattern can sometimes be considered an anti-pattern due to its global state and potential issues with testing and maintainability. As such, it's important to carefully consider when and how to use it in your projects. In this particular case, the Singleton pattern seems to be a suitable choice for managing shared resources and coordinating threads.
  
# A brief overview of CtrlSingleton's functionality 
  
In the code above, CtrlSingleton is a Singleton class that manages the synchronization between the main thread and other spawned threads. It contains a mutex and a condition variable that are used to coordinate the execution of threads in the program.

Here's a brief overview of its functionality:

The GetInstance() method returns a reference to the unique instance of the CtrlSingleton class, ensuring that only one instance is created and used throughout the program.
  
The GetMutex() method returns a reference to the mutex (mtx_key) in the CtrlSingleton instance. This mutex is used to synchronize access to shared resources or code sections between different threads.
  
The GetCV() method returns a reference to the condition variable (cv_key) in the CtrlSingleton instance. This condition variable is used to block or notify threads in a synchronized manner.
  
In the main part of the code, the CtrlSingleton is used by the Controller class, which acts as a thread controller. The Controller class waits for a keypress from the user and then sends a signal to terminate the other spawned threads (A, B, C, and D). The CtrlSingleton's mutex and condition variable are used to synchronize the keypress event and the termination of the threads.

 # CtrlSingleton and ThrdCounter as Singleton classes
These classes are designed to ensure that only one instance of each class exists throughout the program's lifetime. They achieve this by:

1) Making the constructors private, which prevents external instantiation.

2) Deleting the copy constructor and assignment operator, preventing copying and assignment.

3) Using a static GetInstance() function that returns a reference to the single instance of the class.

# Singleton patterns are used in this code for the following reasons:

1) Resource sharing: The Singleton pattern allows multiple threads to share resources like the mutex and condition variable in a controlled manner. In this code, the CtrlSingleton class provides a shared mutex and condition variable used by the Controller thread, while the ThrdCounter class provides shared resources to keep track of the number of active threads.


2) Ensuring consistency: The Singleton pattern ensures that there is only one instance of each class, maintaining consistency across the application. For example, ThrdCounter's instance keeps track of the number of active threads, and if multiple instances were allowed, the count might become inconsistent.


3) Encapsulation: Singleton classes encapsulate their resources and provide controlled access to them. This promotes better organization and makes the code more maintainable.


In summary, the Singleton pattern is used in this code to manage shared resources and ensure consistency across the application while also providing a clear and maintainable structure.
  
