---
layout      : post
title       : "Everything in Java is an Object"
date        : 2015-05-06 18:46:05
categories  : Java
---


To do any kind of programming, we need to manipulate elements that are present in memory. In some languages, the programmer needs to be constantly aware of whether they are manipulating the elements directly or they are dealing with some indirect representation (like pointers in C or C++) that need to be handled specially.

In Java, every element is an object. And although we treat everything as an object, what we actually manipulate is the **reference** to that object.

{% highlight java %}
String s; 
{% endhighlight %}

But here we have only created a reference named 's'. If we tried to do anything with 's' at this point, we would get an error since there is no object connected to this reference.

Thus, whenever we create an object in Java, we should connect it to an object. We do this by using the new operator or the assignment (=) operator:

{% highlight java %}
String s = new String("Gaurav");
String s = "Gaurav";
{% endhighlight %}

The above statement is the equivalent of saying "Make me a new String" while also giving the information about how to by supplying the initial characters. Please note the using the '=' sign instead of the new operator produces the same output but is very different in terms of the implementation (More on this later)

**Analogy:** To better imagine the above explanation, imagine a television as an object and a remote control as the reference. Although we always need the remote control to manipulate what the television does, owning a remote control does not always mean that we have a television as well.

***
<br>

**PRIMITIVE TYPES**:

Some types of objects (also known as the primitive types) are given special treatment by Java. This is because it isnt very efficient to create small and simple variables with the **new operator** since 'new' places objects on the **heap**. For these types, instead of creating variables that hold a reference to the object, Java creates variables that **directly hold the value**. This leads to the variables being placed on the **stack** rather than the heap and makes the process a lot **more efficient**. 

![Primitive Data Types in Java](/resources/primitive_data_types.jpg)

Every primitive type in Java has a **Wrapper Class** that allows us to make a non primitive object on the heap. 

{% highlight java %}
Primitive Type:     int x = 2;
Non-Primitive Type: Integer x = new Integer(2);
{% endhighlight %}

As mentioned above, primitive types are created on the stack while non-primitive types are created on the heap.

***
<br>

**OBJECT DESTRUCTION IN JAVA**:

In most languages, the concept of the lifetime of the variable occupies a significant portion of the programming effors and can also lead to a lot of bugs. Java simplifies thus by doing the cleanup work for us.

**Scoping** determines the visibility and the lifetime of the variables that have been defined. In Java, this scope is defined by the usage of the **curly braces {}** and a variable defined within a scope is only available to the end of that scope.

{% highlight java %}
{
    int x = 12;  //Only x is available
    {
        int q = 10; //Both x and q are available
    }
    //Only x is available as q is out of scope
}
{% endhighlight %}

Some languages allow the hiding of the variables that are in the **larger scope** if they are re-defined in the current scope. For example: the following is legal in C and C++, but is not allowed in Java as it causes a lot of confusion without adding a lot of value:
{% highlight java %}
{
    int x = 12;
    {
        int x = 10; //Illegal
    }
}
{% endhighlight %}

<br>

**Scope of Objects:**

Java objects do not have the same lifetimes as primitives. When we create an object using new, the **object hangs around even after the end of the scope even though the reference vanishes at the end of the scope**. This leads to a situation where in an object continues to exist in memory without any way for the programmer to access it since the only reference to it has become out of scope. 

In C++, it is the programmer's job to destroy the objects once they are not needed which leads to a class of programming problems called the **memory leak**, in which a programmer forgets to release memory. 

To eliminate this, Java comes with an inbuilt **garbage collector**, which looks at all objects that were created with new and figures out which ones are **not being referred** to anymore. Then it **releases memory** for those objects so the memory can be used for new objects. 

![Garbage Collection in Java](/resources/garbage_collection.png)

