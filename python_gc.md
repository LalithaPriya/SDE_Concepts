### Python Garbage Collection: What It Is and How It Works

#### Basics of Memory Management
Python, a popular programming language, excels in data analysis, web applications, and task automation. The article delves into memory management, highlighting the need for effective garbage collection.

#### Why we need Garbage Collection
Memory management in early languages required developers to allocate and deallocate memory manually, leading to issues like memory leaks and dangling pointers. Automatic memory management, including garbage collection, alleviates these problems but comes with trade-offs.

#### How Python Implements Garbage Collection
Python utilizes two main approaches to memory management and garbage collection: 
1. **Reference counting:** Tracks references to objects, deallocating when the count reaches zero.
2. **Generational garbage collection:** Categorizes objects into generations, promoting efficiency and addressing issues like reference cycles.

### What is Python garbage collection and why do we need It?

#### Memory management
Objects, including variables and data structures, store values in memory. Early languages required manual memory management, leading to potential memory leaks or premature deallocation issues.

#### Automatic memory management and garbage collection
Automatic memory management, handled by the runtime, eliminates the need for manual memory management. Reference counting, a common method, tracks references to objects and deallocates when the count reaches zero. However, issues like reference cycles may persist.

### How Python implements garbage collection

#### Reference counting in CPython
The primary garbage collection mechanism in CPython involves reference counts. Objects' reference counts increase when referenced and decrease when dereferenced. Objects with zero references are deallocated.

Everything looks ok until now, but …

There is a problem!
The most important issue in reference counting garbage collection is that it doesn’t work in cyclical references.

What is a cyclical reference or reference cycle?
It is a situation in which an object refers to itself. The simplest cyclical reference is appending a list to itself.


The simplest cyclical reference. Image by author made with Canva
Reference counting alone can not destroy objects with cyclic references. If the reference count is not zero, the object cannot be deleted.

The solution to this problem is the second garbage collection method.
#### Generational garbage collection
Python employs a generational garbage collector to address challenges like reference cycles. Objects start in the first generation, moving to older generations if they survive garbage collection processes. The garbage collector has thresholds and can be manually triggered or adjusted.

Python keeps track of every object in memory. 3 lists are created when a program is run. Generation 0, 1, and 2 lists.

Newly created objects are put in the Generation 0 list. A list is created for objects to discard. Reference cycles are detected. If an object has no outside references it is discarded. The objects who survived after this process are put in the Generation 1 list. The same steps are applied to the Generation 1 list. Survivals from the Generation 1 list are put in the Generation 2 list. The objects in the Generation 2 list stay there until the end of the program execution.

#### Using the GC module
The `gc` module provides tools to check and modify garbage collection behavior. Users can inspect thresholds, count objects in generations, and manually trigger garbage collection processes.

### Python Garbage Collector: What does it mean for you as a developer

#### General rule: Don't change garbage collector behavior
Python's garbage collection is designed for developer productivity, abstracting low-level details. Manual memory management may be more relevant in constrained environments, but for most cases, relying on Python's default behavior is advisable.

#### Disabling the garbage collector
While reference counting cannot be disabled, the generational garbage collector in the `gc` module can be altered. However, caution is advised, and changing behavior may be unnecessary for typical applications. The article mentions Instagram's case of disabling the garbage collector for specific performance gains in a unique scenario.

### Wrapping up
Understanding Python garbage collection is crucial for developers, even though Python handles most memory management intricacies. The knowledge of avoiding reference cycles and occasional adjustments to garbage collection behavior can contribute to efficient Python programming.
