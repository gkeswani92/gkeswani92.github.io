---
layout      : post
title       : "Control Flow in Java"
date        : 2015-05-20 10:46:05
categories  : Java
---

Control flow or execution control in Java is done using the keywords like if-else, while, do-while, for, and a selection statement called switch along with conditionals. All conditional statements use the truth or falsehood of a conditional expression to determine the execution path. 

An example of a conditional expression is A == B. This uses the conditional operator == to see if the value of A is equivalent to the value of B. The expression returns true or false.  

Note: Java doesn’t allow you to use a number as a boolean, even though it’s allowed in C and C++ (where truth is nonzero and falsehood is zero). 

{% highlight java %}
a = 0;
if (a): //Allowed in C and C++, not in Java
    print True;
{% endhighlight %}

If you want to use a non-boolean in a boolean test, such as if(a), you must first convert it to a boolean value using a conditional expression, such as if(a != 0).

***
<br>

**if-else:**

The if-else statement is probably the most basic way to control program flow. The else is optional, so you can use if in two forms:

{% highlight java %}
if(Boolean-expression)
    statement

OR

if(Boolean-expression)
    statement
else
    statement
{% endhighlight %}

The conditional must produce a boolean result. The statement is either a simple statement terminated by a semicolon or a **compound statement**, which is a group of simple statements **enclosed in braces.**

Although indenting the code is not mandatory in Java, it helps to make the code more readable and thus must be done at all times.

***
<br>

**return:**

The return keyword has two purposes: it specifies what value a method will return (if it doesn’t have a void return value) and it causes that value to be returned immediately. 

This is an important execution control method as it is generally used to come out of a method if a particular condition is encountered (used mostly in **recursive** techniques)

***
<br>

**while:**

In a while loop, the Boolean-expression is evaluated once at the beginning of the loop and again before each further iteration of the statement. The form of such a loop is:

{% highlight java %}
while(Boolean-expression)
    statement
{% endhighlight %}

Running a while loop is like saying "Check for this condition. If it is true, keep doing this loop until the condition becomes false”

***
<br>

**do while:**

The sole difference between while and do-while is that the statement of the do-while always **executes at least once**, even if the expression evaluates to false the first time. In a while, if the conditional is false the first time the statement never executes. 

{% highlight java %}
do
    statement
while(Boolean-expression);
{% endhighlight %}

Running a do while loop is like saying "Run this loop at least once. Then check for the condition and keep doing this loop until the condition becomes false”

***
<br>

**for:**

A for loop performs initialization before the first iteration. Then it performs conditional testing and, at the end of each iteration, some form of “stepping.” The form of the for loop is:

{% highlight java %}
for(initialization; Boolean-expression; step)
    statement
{% endhighlight %}

Any of the expressions initialization, Boolean-expression or step can be empty. The expression is **tested before each iteration**, and as soon as it evaluates to false, execution will continue at the line following the for statement. At the **end of each loop, the step executes**. 

We can define multiple variables within a for statement, but they must be of the same type. In the given example, the int definition in the for statement covers both i and j

{% highlight java %}
for(int i = 0, j = 1;
    i < 10 && j != 11;
    i++, j++)
    /* body of for loop */
{% endhighlight %}

The for loop is generally used in conditions where we **know in advance how many times the loop is to be run**. In places where the number of iterations aren't very clear in advance, the while or the do while loop are used.

***
<br>

**break and continue:**

Inside the body of any of the iteration statements you can also control the flow of the loop by using break and continue. 

**break quits the loop** without executing the rest of the statements in the loop while **continue stops the execution of the current iteration** and goes back to the beginning of the loop to begin the next iteration. 

{% highlight java %}
for(int i = 0;; i++)
{
    if ( i == 20 )
        break //This loop would go on infinitely unless the break statement would be 
              //present. Now the last number to be checked for odd or even is 19 and 
              //the control goes out of the loop as soon as 20 is encountered.
    if (i % 2 == 0)
        continue //Skips the iteration in case of even numbers and proceeds to next
    else
        System.out.println(i) //Prints only the odd numbers
}
{% endhighlight %}


**Infinite Loops:** It is important to understand that while(true) and for(;;) are infinite loops which we cannot come out of unless there is a break or return statement used somewhere in them. The compiler treats both while(true) and for(;;) in the same way so whichever one you use is a matter of programming taste.

***
<br>

**goto/label:**

A label is an identifier followed by a colon, like this:
{% highlight java %}
label1:
{% endhighlight %}

The only place a label is useful in Java is right before an iteration statement. And that means right before—it does no good to put any other statement between the label and the iteration. And the sole reason to put a label before an iteration is if you’re going to nest another iteration or a switch inside it. That’s because the break and continue keywords will normally interrupt only the current loop, but when used with a label they’ll interrupt the loops up to where the label exists

{% highlight java %}
label1:
outer-iteration 
{
    inner-iteration {
    //...
        break; // 1
    //...
        continue;  // 2
    //...
        continue label1; // 3
    //...
        break label1;  // 4
{% endhighlight %}

In case 1, the break breaks out of the inner iteration and you end up in the outer iteration. In case 2, the continue moves back to the beginning of the inner iteration. But in case 3, the continue label1 breaks out of the inner iteration and the outer iteration, all the way back to label1. Then it does in fact continue the iteration, but starting at the outer iteration. In case 4, the break label1 also breaks all the way out to label1, but it does not re-enter the iteration. It actually does break out of both iterations

The following rules are used to work out how break and continue function:

1. A **plain continue** goes to the **top of the innermost** loop and continues.
2. A **labeled continue** goes to the label and re-enters the loop right **after that label**.
3. A **break** “drops out of the **bottom” of the loop**
4. A **labeled break** drops out of the bottom of the **end of the loop denoted by the label**.

<br>

**Why did Djikstra have a problem with the original goto statement?**

In Dijkstra’s “goto considered harmful” paper, what he specifically objected to was the labels, not the goto. He observed that the number of bugs seems to increase with the number of labels in a program. Labels and gotos make programs **difficult to analyze statically**, since it **introduces cycles** in the program execution graph. But this has been controlled by Java and their labels don’t suffer from this problem, since they are **constrained in their placement**(only right before the iteration) and can’t be used to transfer control in an ad hoc manner.

***
<br>

**switch:**

The switch is sometimes classified as a selection statement. The switch statement selects from among pieces of code based on the value of an integral expression. Its form is:

{% highlight java %}
switch(integral-selector) 
{
    case integral-value1 : 
        statement; 
        break;
    case integral-value2 : 
        statement; 
        break;
    case integral-value3 : 
        statement; 
        break;
    // ...
    default: 
        statement;
}
{% endhighlight %}

**Integral-selector** is an expression that produces an integral value. The switch **compares the result of integral-selector to each integral-value**. If it finds a match, the corresponding statement (simple or compound) executes. If **no match occurs, the default statement executes**.

Each case ends with a break, which causes execution to jump to the end of the switch body. This is the conventional way to build a switch statement, but the **break is optional**. If it is missing, the code for the **following case statements execute until a break is encountered**. 

There is no break statement following the default, because the execution just falls through to where the break would have taken it anyway. You could put a break at the end of the default statement with no harm if you considered it important for style’s sake. 

The switch statement is a clean way to implement **multi-way selection** (i.e., selecting from among a number of different execution paths), but it **requires a selector that evaluates to an integral value such as int or char**. If you want to use, for example, a string or a floating-point number as a selector, it won’t work in a switch statement. For **non-integral types**, you must use a **series of if statements**. 

