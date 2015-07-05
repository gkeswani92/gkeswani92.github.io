---
layout      : post
title       : "Does python have variables or names?"
date        : 2015-07-03 14:46:05
categories  : Python
---

The working of the assignment operators and variables differs slightly from language to language. But Python brings a complete different perspective to the table when it comes to assignments and memory management of variables/names.

In many other languages, assigning a value to a variable puts a value into a box. There is a block of memory space that is created so that it can hold the value for that variable

{%highlight java %}
int a = 1;
{% endhighlight %}

![New Memory Space for Variable](/resources/a1box.png)

And for all the variables you create, a new box is created with the variable name to hold the value. If you change the value of the variable the box will be updated with the new value. That means doing

{%highlight java %}
a = 2;
{% endhighlight %}

will result in

![Value in memory space is replaced](/resources/a2box.png)

Now, due to this behavior, assigning one variable to another makes a copy of the value and puts it in the new box that has been created for the new variable

{%highlight java %}
int b = a;
{% endhighlight %}

![Two variables](/resources/a2b2box.png)

This new box has a different memory location and id even if the value it contains is the same as that of the original box.

But in Python variables work more like tags unlike the boxes you have seen before. When we do an assignment in Python, it tags the value with the variable name.

{%highlight python %}
a = 1
{% endhighlight %}

![New tag for a variable](/resources/a1tag.png)

And if we change the value of the varaible, it just changes the tag to the new value in memory. We dont need to do the housekeeping job of freeing the memory as Python's Automatic Garbage Collection does it for us. When a value is without names/tags it is automatically removed from memory.

{%highlight python %}
a = 2
{% endhighlight %}

![New tag for a variable](/resources/a2tag.png)

Because of this, assigning one variable to another makes a new tag bound to the same value as shown below and both share the same memory location and id.

{%highlight python %}
b = a
{% endhighlight %}

![Two variables with same value](/resources/ab2tag.png)

Thus we can say that while other languages have 'variables', Python has 'names'.