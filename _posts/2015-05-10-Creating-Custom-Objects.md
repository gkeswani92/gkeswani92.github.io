---
layout      : post_page
title       : "Class and Objects in Java"
date        : 2015-05-10 20:46:05
categories  : Java
---

In the object oriented world, a class is nothing but a blueprint or a template for creating different objects. Each class defines some properties and behaviors. Java objects exhibit these properties and behaviors that are defined by its class. These properties and behaviours are defined in a class by means of fields and methods.

A class can be created in the following manner:

{% highlight java %}
class aTypeName 
{
    //Class body goes here
}
{% endhighlight %}

The above code snippet creates a class or a new type and we can create an object with the following three steps:

**1. Declaration:** A variable declaration with a variable name with an object type.

**2. Instantiation:** The 'new' key word is used to create the object.

**3. Initialization:** The 'new' keyword is followed by a call to a constructor (will be described later). This call initializes the new object.
 
{% highlight java %}
ATypeName a = new ATypeName();
{% endhighlight %}

<br>

**FIELDS:**

When we define a class, we can add two types of elements to it: fields (data members) and methods (member functions). Fields can be primitive types or non-primitive ones that we can talk to via their reference. What is important is that each object keeps its own storage for its fields.

{% highlight java %}
class DataOnly 
{
    int i;
    double d;
    boolean b;
}
{% endhighlight %}

When an object of the above class is created, we can assign data to the fields and manipulate that data by using the '.' operator in the following manner:

{% highlight java %}
DataOnly data =  new DataOnly();
data.i = 47;
data.b = True
{% endhighlight %}

It is also possible for objects to contain other objects which might contain data. To access that data, we would use multiple '.' operators like

{% highlight java %}
myPlace.leftTank.capacity = 100
{% endhighlight %}

<br>

**METHODS:**

Methods in Java determine the messages an object can receive and can thus only be a part of classes. If we try to call a wrong method for an object, we will get an error message at compile time. To call a method, we use the object name, the dot operator and then the method name.

The fundamental parts of a method are its name, arguments, return type and the body. 

{% highlight java %}
ReturnType methodName( Argument List )
{
    //Method Body
}
{% endhighlight %}

The return type describes the value that comes back from the method after it has been called while the argument list is the information that we want to pass to the method for it to be executed the way we want it to. The method name and the argument list (together known as the **method signature**) are used to uniquely identify a method.

**Argument list:** This specifies the information that is being passed into the method. The argument list must contain the type of object that needs to be passed in and the name that must be used to refer to that object. Like any other situation in Java, when we pass objects in the arguments, we are actually passing their references.

{% highlight java %}
int Storage( String s )
{
    //Method body
}
{% endhighlight %}

The data type of the object being passed to the method should match the data type specified in the method signature or else an error is thrown. 

**Return type:** The return variable causes a value to be returned from a method. If we are storing the value retured by a method in a variable, then the return type of the method should be compatible with the data type of the variable it is being stored in. 

{% highlight java %}
int sum( int a, int b )
{
    return a + b;
}
int c = sum(2,3);
{% endhighlight %}

If no value is to be returned from a particular method, the return type should be **void**
{% highlight java %}
void nothing( int a, int b ) { }
void nothing( int a, int b ) 
{
    return;
}
{% endhighlight %}

One important point to note about the return statement is that it is always the last statement to be executed in a method. This means that once a return statement is encountered, the flow of control will exit from the method and go back to the caller method without executing the statements below the return statement.

***
<br>

**THE STATIC KEYWORD:**

As we have seen till now, with ordinary, data and methods you must create an object and use that object to access the data or method, since data and methods must know the particular object they are working with. 

But there are times we need to store data or use methods irrespective of which object we are using them with or even at times when no objects have been created. This is where the statis keyword comes into the picture.

The static keyword is primarily used for two purposes:

1. If you want to have only **one piece of storage** for a particular piece of data, regardless of how many objects are created, or even if no objects are created. 
2. The other is if you need a **method that isn’t associated with any particular object** of this class. That is, you need a method that you can call even if no objects are created. 

When you say something is static, it means that data or method is not tied to any particular object instance of that class. So even if you’ve never created an object of that class you can call a static method or access a piece of static data.

NOTE: Since static methods don’t need any objects to be created before they are used, they **cannot directly access non-static members or methods** by simply calling those other members without referring to a named object

To make a field or method static, you simply place the static keyword before the definition as follows:
{% highlight java %}
class StaticTest
{
    static int i = 47;
}
{% endhighlight %}

Now, if we create two objects of the static test class and try and access the variable i, both will have the **same value** i.e. 47

{% highlight java %}
StaticTest st1 = new StaticTest();
StaticTest st2 = new StaticTest();
System.out.print(st1.i); //47
System.out.print(st2.i); //47
{% endhighlight %}

Although static variables can be accessed with the object name, it is better to access them via the **class name** since it gives the compiler a chance for optimisation

{% highlight java %}
System.out.print(StaticTest.i); //47
{% endhighlight %}

Using the static keyword, does not change the functionality of methods as much as they do with fields, but it allows the method to be called without creating an object (main() method will be talked about later)

***
<br>

Thus, we see that a class can contain any of the following variable types:

**1. Local variables:** Variables defined inside methods are called local variables. The variable will be declared and initialized within the method and the variable will be destroyed when the method has completed.

**2. Instance variables:** Instance variables are variables within a class but outside any method. These variables are instantiated when the class is loaded. Instance variables can be accessed from inside any method of that class.

**3. Class variables:** Class variables are variables declared with in a class, outside any method, with the static keyword.



