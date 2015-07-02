---
layout      : post_page
title       : "Types of Memory used in Java"
date        : 2015-05-07 20:46:05
categories  : Java
---

Two of the most important things to consider while writing programsare the time and space complexity. Time complexity is the amount of time taken by the program to produce the desired output while space complexity refers to the amount of memory that is consumed by the program for its execution. And although memory is getting cheaper by the day, the amount of data that is being generated and the large scaling needs of applications has made it paramount for programs to be memory efficient. 

For this, we first need to understand the different types of memory that are available to us while programming in Java so that we can make an informed decision about which type to use in which situations. 

**Registers:**

1. This is the **fastest storage** because it exists inside the processor. However, the number of registers is **severely limited**, so registers are allocated by the compiler according to its needs.
2. Although some languages like C and C++ allow the programmer to suggest register allocation to the compiler, Java does not provide any such control to the programmers.

**Stack:**

1. The stack lives in the general **RAM (random-access memory)** area, but has direct support from the processor via its stack pointer.
2. The stack pointer is moved down to create new memory and moved up to release that memory. This is an extremely fast and efficient way to allocate storage, second only to registers. 
3. The downside of using a stack is that the Java compiler must know, while it is creating the program, the exact size and lifetime of all the data that is stored on the stack. This is because it must generate the code to move the stack pointer up and down. This places **limits on the flexibility** of programs, so while some Java storage like **object references exists on the stack**, Java **objects are not placed on the stack**

**Heap:**

1. This is a general-purpose pool of memory that also exists in the **RAM area** where all Java objects live. 
2. Unlike the stack, the compiler doesn’t need to know how much storage it needs to allocate from the heap or how long that storage must stay on the heap. Thus, there’s a great deal of **flexibility** in using storage on the heap.
3. Whenever we create an object using the **new keyword**, the storage is allocated on the heap when that code is executed.
    Of course there’s a price you pay for this flexibility: it takes **more time to allocate heap storage** than it does to allocate stack storage

![Stack and Heaps work together in Java](/resources/stack_heap.png)