---
layout: post
title:  "Python Functional Programming"
comments: true
date:   2016-04-25 18:05:18 +0100
---

Python is a very powerful language, being one of <a href="http://stackoverflow.com/research/developer-survey-2016#technology">the most popular technologies</a> used by developers. It has many features that make it very dynamic and powerful, one of which is it's support for functional programming. 

Today, I will walk you through the Map, Lambda and Filter functions in Python. The map() function applies a function to all the elements of a list. It takes two parameters, the function that is to be applied to the list and the list itself.

{% highlight python %}
>>> print(list(map(len, ['Hello','World'])))
[5, 5]
{% endhighlight %}

The lambda function is annonymous function which returns itself. It is used as an inline function and can only have one expression.

{% highlight python %}
>>> divide = lambda: a, b: a/b
>>> print(divide(4,2))
2
{% endhighlight %}

Now lets use the above two functions to return the cube of a list of fibonacci numbers.  
{% highlight python %}
n = int(raw_input())
x = []
cube = lambda a: a*a*a
a,b = 0,1
if n!=0:
    x.append(a)
for i in range(n-1):
    if i == 0:
        x.append(b)
        i+=2
    else:
        x.append(a+b)
        a,b = b, x[i+1]
print list(map(cube,x))
{% endhighlight %}

For the above piece of code, when 
Input is
```5```
The output turns out to be:
```[0, 1, 1, 8, 27]```

Python is incredible, isn't it? Now let's talk about filters in python. A filter() takes in a boolean function and applies it to a list, and finally returns the elements for which the applied function is true. For instance
{% highlight python %}
>>> l = [2, 3, 5, 6]
>>> filter(lambda x: x%2 == 0, l)
[2, 6]
{% endhighlight %}

Now lets use all that we have learnt to perform email validation. The first line is the integer N, the number of email addresses. This will be followed by the respective emails in N lines.

The Output is the list of email addresses which are valid in lexographic order. An email address is valid if-
<ul> 
<li> It has the username@websitename.extension format type. </li>
<li> The username only contains letters, digits, dashes and underscores. </li>
<li> The website name only has letters and digits. </li>
<li>The maximum length of the extension is 3.</li> 
</ul>

Sample Input:<br>
```3``` <br>
```lara@wells.com```<br>
```brian-23@yahoooo.com```<br>
```declan@gmaill.com```<br>

Sample Output:

```
['brian-23@yahoooo.com', 'declan@gmaill.com', 'lara@wells.com']
```
Lets get started! We have three lambda functions that check the validity of the username, website Name and the extension. We also have to make sure that there is a username, '@' isnt being used twice, the address contains '.' etc.

{% highlight python linenos %}
import re
def validate(email):
    valid_username = lambda a: re.match("^[A-Za-z0-9_-]*$", a) and len(a) != 0
    valid_website = lambda b: b.isalnum()
    valid_extension = lambda c: len(c) <= 3
    
    if ('@' and '.' in email and email.count('@') == 1):
        return (valid_username(email[:email.index('@')]) and 
               valid_website(email[(email.index('@')+1):email.index('.')]) and
               valid_extension(email[(email.index('.')+1):]))
    else:
        return False

n = int(raw_input())
emails = []
for i in range(n):
    a = raw_input()
    emails.append(a)

ans = list(filter(lambda email: validate(email), emails))

print sorted(ans)

{% endhighlight %}

So today we learnt about some of the functional programming aspects of python which makes it so powerful. This was my first blog post and I hope you enjoyed it. See you soon! 