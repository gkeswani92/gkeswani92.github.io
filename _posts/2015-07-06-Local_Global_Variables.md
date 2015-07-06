---
layout      : post
title       : "Local and Global variables in Python"
date        : 2015-07-06 14:46:05
categories  : Python
---

Local variables are the variables that are defined inside a method and are only available inside the scope of the method while global variables are defined outside a method and are thus available to all methods in the same module. 

Local variables of functions can't be accessed from outside, when the function call has finished:

{% highlight python%}
def f():
    s = "I am globally not known"
    print s 

f()
print s #NameError: name 's' is not defined
{% endhighlight %}

There are times when we want to define variables at a global level and use them in multiple methods. In the below code snippet, 's' is defined as a global variable and can be used inside the method 'f' or any other similar methods.

{% highlight python%}
def f(): 
    print s 
s = "I hate spam"
f()
{% endhighlight %}

The variable s is defined as the string "I hate spam", before we call the function f(). The only statement in f() is the "print s" statement and as there is no local 's', the value from the global 's' will be used. 

Now, if we try and define a variable in a method that has the same name as that of a global variable, it's value inside that method is taken from it's local instance.

{% highlight python%}
def f(): 
    s = "Me too."
    print s         #Me too

s = "I hate spam." 
f()
print s             #I hate spam
{% endhighlight %}

While using the same name for a local variable and a global variable, if we reference the global variable first, then define the local variable and then try and reference the local instance, the interpretor throws an error

{% highlight python%}
def f(): 
    print s         #UnboundLocalError: local variable 's' 
                    #referenced before assignment
    s = "Me too."
    print s

s = "I hate spam." 
f()
print s
{% endhighlight %}

Python "assumes" that we want a local variable due to the assignment to s inside of f(), so the first print statement throws this error message.

In the code snippet before this, we see that the print statement inside the method prints "Me too", but the print statement in the global scope still continues to print "I hate spam". 

If we, for any reason want to change the value of a global variable, we should mention "global <variable_name>" in the function before changing its value.

{% highlight python%}
def f():
    global s
    print s                 #Python is great!
    s = "That's clear."
    print s                 #That's clear.


s = "Python is great!" 
f()
print s                     #That's clear. (As can be seen,
                            #value of the global variable 
                            #has changed)
{% endhighlight %}

Specifying, global <variable_name> makes sure that any changes made inside the method change the global variable's value, which will reflect in any usage of that variable further on.

PS- Keep in mind, that you only need to declare them global inside the function if you want to do assignments / change them. global is not needed for printing and accessing.

