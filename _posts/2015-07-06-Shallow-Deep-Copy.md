---
layout      : post
title       : "Shallow and Deep Copy in Python"
date        : 2015-07-05 14:46:05
categories  : Python
---

In the previous section we saw that variables in python behave differently from variables in other languages in the way that values are tagged with variable names instead of each variable having a box created for itself in memory. Because of this behavior, trying to copy lists can be a stumping experience.

**Copying a shallow list:**

In the example below a simple list is assigned to colours1. This list is a so-called "shallow list", because it doesn't have a nested structure, i.e. no sublists are contained in the list. 

We then assign colour1 to colours2. The id() function shows us that both variables point to the same list object, i.e. they share this object.

{% highlight python %}
colours1 = ["red", "green"]
colours2 = colours1
print(colours1) #['red', 'green']
print(colours2) #['red', 'green']
print(id(colours1),id(colours2)) #43444416 43444416
{% endhighlight %}

![Two lists with the same content](/resources/same_content_list.png)


If we assign a new list object to colours2, the values of colours1 remained unchanged. This is due to the fact that a new memory location has been allocated for colours2, because we have assigned a complete new list, i.e. a new list object, to this variable.

{% highlight python %}
colours2 = ["rouge", "vert"]
print(colours1) #['red', 'green']
print(colours2) #['rouge', 'vert']
print(id(colours1),id(colours2)) #43444416 43444200
{% endhighlight %}

Now, if we try and change one element of the list colours2, we see that the contents of both the lists show the change. 

{% highlight python %}
colours1 = ["red", "green"]
colours2 = colours1
print(id(colours1),id(colours2)) #14603760 14603760
colours2[1] = "blue"
print(id(colours1),id(colours2)) #14603760 14603760
print(colours1) #['red', 'blue']
print(colours2) #['red', 'blue']
{% endhighlight %}

![Two lists with the same content and one element replaced](/resources/deep_copy_2.png)


The above problem can be overcome by using the slice operator which creates a new copy of the mutable list and stores it at a different memory address. 

{% highlight python %}
list1 = ['a','b','c','d']
list2 = list1[:]
list2[1] = 'x'
print(list2) #['a', 'x', 'c', 'd']
>>> print(list1) #['a', 'b', 'c', 'd']
{% endhighlight %}

But even with the slice operator, we run into the same problems as before when we try and slice or copy nested lists.

{% highlight python %}
lst1 = ['a','b',['ab','ba']]
>>> lst2 = lst1[:]
{% endhighlight %}

results in

![Slicing nested lists](/resources/deep_copy_3.png)

When we now try to change an element a normal element of the new list, the original list is not affected. But when it comes to changing the value present in the inner list, the effect is still seen in the original list.

{% highlight python %}
lst2[0] = 'c'
lst2[2][1] = 'd'
print(lst1) #['a', 'b', ['ab', 'd']]
print(lst2) #['c', 'b', ['ab', 'd']]
{% endhighlight %}

This is because the memory structure for the above operation looks like:

![Slicing nested lists](/resources/deep_copy_4.png)

To overcome the above situation, we need to use the deepcopy method of the copy module provided by Python. 

{% highlight python %}
from copy import deepcopy
lst1 = ['a','b',['ab','ba']]
lst2 = deepcopy(lst1)
lst2[2][1] = "d"
lst2[0] = "c";
print(lst2) #['c', 'b', ['ab', 'd']]
print(lst1) #['a', 'b', ['ab', 'ba']]
{% endhighlight %}

The usage of deepcopy results in the following type of memory structure, thus avoiding the change in the original list due to modifications in the new one. 

![Slicing nested lists](/resources/deep_copy_5.png)

PS- The difference between shallow and deep copying is only relevant for compound objects, i.e. objects containing other objects, like lists or class instances. 