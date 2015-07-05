---
layout      : post
title       : "Python Collections: defaultdict"
date        : 2015-06-30 10:46:05
categories  : Python
---

Dictionaries are a convenient way to store data for retrieval by its keys. Keys must be unique, immutable objects, and are typically strings. The values in a dictionary can be integers, strings or collections like lists, dicts etc. In this case, the value (an empty list or dict) must be initialized the first time a given key is used. 

{% highlight python %}
#Lets try and store the index of the numbers that appear in a list
num     = [1,2,3,1,2,4,5]
counter = {}
for i, x in enumerate(num):
    if x in counter:
        counter[x].append(i)
    else:
        counter[x] = [i]
{% endhighlight %}

What this above piece of code does first is it checks whether a number is present as a key in the dictionary. If it is present, it appends the current index to the already present list. If not, it creates a single element list with the current index.While this is relatively easy to do manually, the defaultdict type automates and simplifies these kinds of operations.

A defaultdict works exactly like a normal dictionary, but it is **initialized with a function** (“default factory”) that takes no arguments and provides the default value for a nonexistent key. The above piece of code with defaultdict would look like follows:

{% highlight python %}
#Lets try and store the index of the numbers that appear in a list
from collections import defaultdict
num     = [1,2,3,1,2,4,5]
counter = defaultdict(list)
for i, x in enumerate(num):
    counter[x].append(i)
{% endhighlight %}

Using defaultdict lets us **avoid the conditional checking of whether a key exists in the dict**. If the key exists, it appends the current index to it as usual. On the other hand, if the key does not exist, it considers the default value of the key as an empty list i.e. [] and appends the current index to it, thus mimicking the behavior of the earlier piece of code.


The standard behavior of a python dictionary when the programmer tries to access a key that is not present in the dictionary is to throw a Key Error exception. It should be pretty evident by now that a defaultdict will **never raise a KeyError**. Any key that does not exist gets the value returned by the default factory.

{% highlight python %}
from collections import defaultdict
default_counter = defaultdict(list)
normal_counter  = {}
print(normal_counter[1])  #Key Error
print(default_counter[1]) #[]
{% endhighlight %}

Other places where default dict can be used is to maintain the frequencies of alphabets in a string.

{% highlight python %}
from collections import defaultdict
name    = 'abcabca'
counter = defaultdict(int) #default function being int defaults the value to 0
for x in name:
    counter[x] += 1
{% endhighlight %}



