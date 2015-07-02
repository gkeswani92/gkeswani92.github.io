---
layout      : post_page
title       : "Operators in Java"
date        : 2015-05-13 10:46:05
categories  : Java
---

To do anything meaninful with programs, one needs to manipulate the data and make choices during execution. In Java, we manipulate data using operators and make choices with execution control statements. In this post, we will look at the various operators that are at the programmers disposal while using Java.

An **operator** takes one or more arguments and produces a new value. These arguments to operators are not passed like they are to methods, but the effect is the same. Some common operators include addition(+), subraction(-), multiplication(*), division(/) etc. Operators either produce a value from their operands or change the value of their operand (called **side effect**).

**Operator Precedence:** This defines how an expression is evaluated when several operators are present. In Java, multiplication and division have equal precedence and are evaluated before addition and subraction. When two operators with equal precedence are present, the expression is evaluated from left to right. 

***
<br>

**ASSIGNMENT OPERATOR:** 

Assignment in java is performed with the '=' operator which means that the value of the right hand side has to be copied into the left hand side. The right hand value can be any constant, variable or expression that can produce a value, but the left hand value must be a variable that can accept the data being copied into it. 

{% highlight java %}
int a = 47; //Valid
4 = a; //Invalid
int a = "Gaurav"; //Invalid
{% endhighlight %}

Assignment with **primitives** is straight forward in the sense that when we say a = b, it is the **content/value** present in b that is copied over to a. If we then go and modify a, b continues to be unaffected by this alteration.

{% highlight java %}
int a = 47; 
int b = a
System.out.println(a); //47
System.out.println(b); //47
b = 10
System.out.println(a); //47
System.out.println(b); //10
{% endhighlight %}

When it comes to **objects**, the assignment operator is used to **copy the reference** from one variable to another. So when we manipulate an object, what we're actually manipulating is the reference. 

![Aliasing in Java](/resources/aliasing.png)

And since both variables now have the same reference with the same underlying object, the change reflects in both variables even when only one is modified. 

{% highlight java %}
Number n1 = new Number(10);
Number n2 = new Number(20);
System.out.println(n1.num); //10
System.out.println(n2.num); //20

n1 = n2
System.out.println(n1.num); //10
System.out.println(n2.num); //10

n1.num = 30
System.out.println(n1.num); //30
System.out.println(n2.num); //30
{% endhighlight %}

This concept in Java where an object is referred to by multiple names/variables and can be modified by any one of them with the change reflecting in all of them is known as **aliasing**

***
<br>

**MATHEMATICAL OPERATORS:** 

The basic mathematical operators include addition(+), subraction(-), multiplication(*), division(/) and modulus(%). These operations can be performed as follows:

{% highlight java %}
int a = 10; 
int b = 6;
System.out.println(a + b); //16
System.out.println(a - b); //4
System.out.println(a * b); //60
System.out.println(a / b); //1 (Integer division truncates rather than rounding the result)
System.out.println(a % b); //4
{% endhighlight %}

Java also uses a **shorthand** to perform an operation and assignment at the same time. This is denoted by using an operator and the equal sign together as follows:
{% highlight java %}
int a = 10; 
int b = 6;
a += b; //Equivalent to a = a + b
{% endhighlight %}

<br>

**Unary Operators:** Most operators that we have seen till now have been binary operators i.e. they need two operands to function normally. There is another class of operators, known as the unary operators, that work with a single operand.

The unary minus(-) and plus(+) operators are used to invert the sign of the variable and make the sign of the variable explicit respectively. 

Unary operators can also be used to shorten the syntax of increasing or decreasing the value of a variable by 1 in the following manner:
{% highlight java %}
int a = 10; 
a = a + 1 
a += 1; //Shorthand
a++; //Unary increment
{% endhighlight %}

Such increment and decrement operators are of two types: Prefix and Postfix. **Prefix** operators means the ++ appears before the operand and the value of the operand is changed before any other operation is performed on it. **Postfix** operators are where the ++ appears after the operand and the value of the operand is changed after any other operation is performed on it. 

{% highlight java %}
int i = 1;
System.out.println("i : " + i);     //1
System.out.println("++i : " + ++i); //2
System.out.println("i++ : " + i++); //2
System.out.println("i : " + i);     //3
System.out.println("--i : " + --i); //2
System.out.println("i-- : " + i--); //2
System.out.println("i : " + i);     //1
{% endhighlight %}

Unary Operators are the only operators (other than those involving assignment) that have **side effects**. (That is, they change the operand rather than using just its value.)

***
<br>

**RELATIONAL OPERATORS:** 

Relational operators generate a boolean result. They evaluate the relationship between the values of the operands. A relational expression produces true if the relationship is true, and false if the relationship is untrue. The relational operators are less than (<), greater than (>), less than or equal to (<=), greater than or equal to (>=), equivalent (==) and not equivalent (!=). 

**Testing Equivalence:** The relational operators == and != work with objects too, but the results can be a little confusing at times. Try guessing the output of the following code snipet:

{% highlight java %}
Integer n1 = new Integer(47);
Integer n2 = new Integer(47);
System.out.println(n1 == n2); //False
System.out.println(n1 != n2); //True
{% endhighlight %}

But surely, n1 is equal to n2 since both the objects have the integer value 47. Well, this is not how == and != work. These two operators compare the **object references** rather than the underlying value or object.

To compare the underlier, we must use the **equals()** method of Java in the following manner:

{% highlight java %}
Integer n1 = new Integer(47);
Integer n2 = new Integer(47);
System.out.println(n1.equals(n2)); //True
{% endhighlight %}

***
<br>

**LOGICAL OPERATORS:**

Each of the logical operators && (AND), (OR) and ! (NOT) produces a boolean value of true or false based on the logical relationhip of its arguments. While AND and OR take two arguments each, NOT is used to reverse the value of a boolean conditional.

![Logical Operators](/resources/logical_operators.png)

You can apply AND, OR, or NOT to boolean values only. You can’t use a non-boolean as if it were a boolean in a logical expression as you can in C and C++

{% highlight java %}
i = 20;
j = 20;
a = (i < 10) && (j < 10); => False AND True ==> False
b = (i < 10) || (j < 10); => False OR  True ==> True
c = 1 || 0 //Not Allowed
{% endhighlight %}

<br>

**Short Circuiting:**

When dealing with logical operators we run into a phenomenon called “short circuiting.” This means that the expression will be evaluated only until the truth or falsehood of the entire expression can be unambiguously determined. As a result, all the parts of a logical expression might not be evaluated. 

For example:
{% highlight java %}
i = 20;
j = 20;
a = (i < 10) && (j < 10); => False AND True ==> False
{% endhighlight %}

In the above case, the first part i.e. i < 10 evaluates to False. It is common knowledge that the logical operator AND requires all conditions to be true, for the final result to be True. So in this case, there is no point in evaluating the rest of the expression as this expression will never be True after the first condition has resulted in a False. 

