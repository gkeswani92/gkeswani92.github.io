---
layout      : post
title       : "Visitor Pattern"
date        : 2015-09-03 14:46:05
categories  : Design_Patterns
---

The goal of the visitor pattern is to **separate the functionality from the data structures**. Because of this, it allows us to add methods/operations to classes without actually modifying the class.

**UML Diagram of Visitor Pattern:**

![New Memory Space for Variable](/resources/visitor_pattern.png)

The **Visitor interface** defines all the visit methods (with the types of objects they take as input) that need to be implemented by the **Visitor class** (TaxVisitor). This just means that we should have 3 different visit methods in the TaxVisitor class that take a Liquor, Tobacco and Necessity object as an input respectively.

These 3 methods would then contain the object specific logic for what needs to be done when the visit method is called from that particular class. Thus, we can say that the TaxVisitor class **implements** the Visitor interface.

We also need to create a **Visitable interface** that has an accept method which takes a Visitor as an input. Every class (Liquor, Tobacco and Necessity) should implement this interface and provide an implementation for the accept() method. This implementation is generally as follows:

{% highlight java %}
double accept(Visitor visitor)
{
    return visitor.visit(this);
}
{% endhighlight %}

**How does the code look?**

- We have a Visitor interface that contains 3 visit methods- one each for Liquor, Tobacco and Necessity

  {% highlight java %}
  public interface Visitor {
  	public double visit(Liquor liquorItem);
  	public double visit(Tobacco tobaccoItem);
  	public double visit(Necessity necessityItem);
  }
  {% endhighlight %}

- We also need a Visitor Class that implements this interface and has local logic for what to do for each of the 3 classes

  {% highlight java %}
  public class TaxVisitor implements Visitor {

  	public double visit(Liquor liquorItem) {
  		return liquorItem.getPrice() * 0.20;
  	}

  	public double visit(Tobacco tobaccoItem) {
  		return tobaccoItem.getPrice() * 0.40;
  	}

  	public double visit(Necessity necessityItem) {
  		return necessityItem.getPrice() * 0;
  	 }
  }
  {% endhighlight %}

- We have a Visitable interface that forces all classes implementing it to have an accept method

  {% highlight java %}
  public interface Visitable {
	   public double accept(Visitor visitor);
   }
  {% endhighlight %}

- We now need to create the 3 classes for Liquor, Tobacco and Necessity which implement the Visitable interface

  {% highlight java %}
  public class Liquor implements Visitable {
	private double price;

	//Constructor to initialise the price of the liquor
	public Liquor(double price) {
		this.price = price;
	}

        //Returns the price of the Liquor
	public double getPrice(){
		return price;
	}

	//Accepts the visitor and calls the visit method on it while passing an instance of the Liquor class
	public double accept(Visitor visitor) {
		return visitor.visit(this);
	}
  {% endhighlight %}

**How does it all come together?**

- Instantiate the TaxVisitor Class
{% highlight java %}
TaxVisitor taxVisit = new TaxVisitor();
{% endhighlight %}

- Create an instance of the Liquor, Tobacco or Necessity Class
{% highlight java %}
Necessity milk = new Necessity(10);
{% endhighlight %}

- Call the accept() method on the instance of the previous class and pass the TaxVisitor object to it
{% highlight java %}
milk.accept(taxVisit)
{% endhighlight %}

The last statement calls the accept method of the Necessity class, which in turn calls the visit method on the visitor with Necessity (notice the 'this') as a parameter. Hence, we finally end up in executing the following method:

{% highlight java %}
public double visit(Necessity necessityItem) {
  return necessityItem.getPrice() * 0;
 }
 {% endhighlight %}

 Still don't understand the use of the visitor pattern? Let's think of an extension to this. Suppose we did not use the visitor pattern and instead had calculateTax() methods inside each of the 3 classes - Liquor, Tobacco and Necessity. Now if the goverment came up with another tax known as VAT, we would have to go and change all 3 of them. **In real life, there may be times when we may not even have access to these classes.** This is where the visitor pattern comes into the picture. With this pattern, all we need to create is a new Visitor class for the VAT and pass that to the accept() method of these 3 classes to use this new functionality.

 And this is the end game of using the Visitor pattern. **To add new functionality to the existing structure without modifying the original structure**
