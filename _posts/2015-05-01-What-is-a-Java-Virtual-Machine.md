---
layout      : post_page
title       : "Why do we need a Java Virtual Machine?"
date        : 2015-05-01 16:46:05
categories  : Java
---

In high-level programming languages such as C and C++, we write a program in a human-readable format, and a program called a compiler translates it to a binary format called executable code that the computer can understand and execute. The executable code depends upon the computer machine that we use to execute our program i.e. it is machine dependent. Java on the other hand, uses a slightly different approach for which it needs something called the Java Virtual Machine. 

To understand the need of the Java Virtual Machine, we first need to understand on a high level how Java actually works:

1. To begin with, Java code is written by programmers in text editors and saved with a .java format. These files are known as the **source code** files.

2. This source code is fed into a **compiler** at compilation time. The compiler scans the code for any obvious syntax errors and does not compile the code until it is error free.

3. Once compiled, the code is converted into an intermediate format known as the **byte code**. These byte code files have a .javac extension

4. When the Java program has to be run, the bytecode file with the .javac extension is passed to the **Just in Time Compilar** which converts it to the machine level code/ native code and runs the program.

![Java Compilation and Interpretation](/resources/java_compile_interpret.png) 


Now lets try and understand the need of the **Java Virtual Machine** and where it comes into the picture. 

As explained above, after the compilation process is completed, the source code is converted into an intermediate form called the byte code. These byte code files are **platform independent files** i.e. they can be transferred and run on any machine, irrespective of where the source code was created. 

And this is exactly where the Java Virtual Machine (or the **JVM** as it is lovingly called) works its magic. The JVM sits as a layer between the operating system and the hardware, and converts the machine independent byte code to the machine specific native code. 

What does this mean? Well, because of the JVM, java programs that are written and converted to the byte code form can be run on any machine in the world provided it has a Java Virtual Machine running on it. Pretty cool, eh?

![Demonstration of the use of the Java Virtual Machine](/resources/byte_code_jvm.png) 

If you're still wondering why Java uses the compile and interpret approach with the byte code instead of directly running the program by converting it into executables like C or C++ do, well, here's why:

1. **Portability:** Each computer has its unique set of instructions and what runs on one machine may not run on another. Thus, Java puts is Virtual Machine between the Operation System and the hardware to convert the byte code to the machine specific format. This means that a program written on one machine can be run on any other machine in the world if it has a Java run time installed on it. 

2. **Security:** The JVM also does basic security checks and validation's before running the code on the machine

3. **Size:** Maintaining a series of operating system and architecture targetted compilations of the same code base can be tedious and tiresome. With this approach, Java ensures that a single compilation of the code needs to exist as it can be compiled and distributed in the form of byte code. This byte code can then be converted by the JVM to the native code depending on the configuration of the machine it is running on. 

4. **Just in Time(JIT) Compilation:** This allows us to update a program by replacing a single patched source file instead of regenerating everything from scratch (More on this later)

Java's approach does have disadvantages in terms of **performance** as it takes a little longer for the compile and interpret process to be completed along with the fact that it is easier to decompile the code. 

It can thus be said with reasonable confidence that the creators of Java valued portability and security a little more than performance. 
