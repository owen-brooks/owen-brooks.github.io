---
layout: post
title: "Decorators in Python"
date: 2018-08-17 08:34:25
categories: Python
tags: featured
image: /assets/article_images/web-scrape/dec.jpg
---

A decorator is a function that takes another function as a input, and does something with it. Say we have two functions:

{% highlight python %}

def FunctionA():
print('something')

def FunctionB(someFunction):
someFunction()

FunctionB(FunctionA)

{% endhighlight %}

Function B is a decorator. Running this would return:

{% highlight python %}

something

{% endhighlight %}

Decorators can be used for many things like monitoring the output of functions or calling a function multiple times

## Pie Syntax

Decorator functions are usually called using Pie syntax. It looks like this:

{% highlight python %}

def FunctionA():
print('something')

@FunctionB
def FunctionA():
print('something')

{% endhighlight %}

This is the python way of doing:

{% highlight python %}

FunctionA(FunctionB())

{% endhighlight %}

## Real Example

### Flask

Flask is a Python application framework. Decorators are used in Flask web controllers to map URLs to the functions they perform. For example:

{% highlight python %}

@app.route('/home')
def home()
return('You are home')

{% endhighlight %}

If a user went to the URL **/home** the decorator **app.route()** would execute the function returning "You are home".
