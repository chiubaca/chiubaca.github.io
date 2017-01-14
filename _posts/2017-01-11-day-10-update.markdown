---
layout: post
title:  "#100DaysOfCode : Day 10 Update"
date:   2017-01-14 21:08:00 +0100
categories: code
---

# Day 10 update

I'm a bit late posting this! turns out squeezing in coding, fitness, cooking and work is actually pretty tricky. But I'm not making excuses, I've remained diligent and stuck to this. Here's what I've been up to in the last 10 days. 

##CSS

I've been focusing at lot of on getting my CSS fundamentals up to scratch which is something I have been working on before starting [#100DaysOfCode](https://twitter.com/hashtag/100DaysOfCode?src=hash) . I've been reading David S. McFarlands book, CSS - The Missing Manual and have learnt so much from it. The book covers everything - from the history of CSS , basic CSS to more advanced concepts and techniques such as responsive web design approaches, grid frame works , CSS pre-compilers, and general CSS best practices. What great about the is that is written in plain laymans and for mere mortals to understand . I really recommend it if you want to improve your knowledge of CSS. 

I've been playing around with [Skeleton](http://getskeleton.com/) , a really light weight CSS framework for responsive web pages, a nice alternative to Twitter Bootstrap. The whole thing is only ~400 lines of code which is awesome in my opinion. I have been able to read the source code and understand what the inner workings are doing.

Additionally, I've learnt how Flexbox works and had the chance to get my hands dirty with it . When I initially first heard of Flexbox I assumed it was another CSS tool, but to my delight its native CSS. For anyone reading this who doesnt know what Flexbox is, It's a relatively new CSS module which is being supported by most browsers. It makes aligning and moving CSS objects a whole lot easier. For instance if you want to align some an unordered HTML list objects in a row( rather than stacked on top each other like they are by default ), the only would be 

`ul{`
  display:flex 
`}`

Perfect for quick navigation buttons!

It also support other cool things like reversing the order of objects and  aligning objects. Doing things the Flexbox way can rapidly reduce the amount the CSS you need to write and makes hacky CSS approaches a whole lot more elegant. [CSS-Tricks]( https://css-tricks.com/snippets/css/a-guide-to-flexbox/) has a great summary about it . 

## Python 

During the tail end of these last 10 days I have been doing a bit of Python work. I was a little bit burnt out on CSS so decided to mix things up and try a Project Euler challenge which was : - 

*2520 is the smallest number that can be divided by each of the numbers from 1 to 10 without any remainder. What is the smallest positive number that is evenly divisible by all of the numbers from 1 to 20?*

My solution - brute force.

```
counter = 5
while True: 
    if counter % 1 == 0 and counter % 2 == 0 and counter % 3 == 0 and counter % 4 == 0 and counter % 5 == 0 and counter % 6 == 0 and counter % 7 == 0 and counter % 8 == 0 and counter % 9 == 0 and counter % 10 == 0 and counter % 11 == 0 and counter % 12 == 0 and counter % 13 == 0 and counter % 14 == 0 and counter % 15 == 0 and counter % 15 == 0 and counter % 16 == 0 and counter % 17 == 0 and counter % 18 == 0 and counter % 19 == 0 and counter % 20 == 0:
        print str(counter) + " IS THE WINNER"
        break
    else:
        print counter
        counter += 5
```

I'm not really satisfied with my solution and frankly I'm a bit embarrassed by how long it takes to compute the result.However, it is a great feeling when you finally crack it. I will try another when the time is right. 

The other Python related work I've focused on was a  little automation project. I was fed up of manually updating the 100 Days of Code counter in my twitter bio so was looking at ways to automate it. Twitter has a REST API, but it's some thing  I wasnt really familar with right out of the box. A quick search on the internet led a me to TweePy, a Python wrapper for the Twitter API. I was really surposed with how easy it was to use, for instance, to update your Twitter profile only requires one function:

``` api.update_profile("username","website","location","Bio") ```

My method of updating my 100 days of  counter  in my bio is only a crappy temporary hack at the moment. As I started  this challenge on the 1st of January ( but missed one day) I simply assigned a varible called `counter` to  the current date using the datetime library and then doing a minus 1 like so:

`counter = counter = str(datetime.datetime.today().day - 1)` 

Then all I had to do was append this variable as a string along with my usual bio as an argument in the function above, simples! This will only work until the end of the month.. so will need to figure out another way to do this. 

Whilst I was working this out I had this wacky idea  " I could totally mash this with another API... would'nt it be funny if I could tell the weather within my twitter account?" - I thought to myself . So instantly went searching for weather API's . Google searching led me to some stack exchange threads and the general consensus was to check out the Open Weather Map API. Of course I wanted to stick with using Python so had two options to do this; use the Requests library  to poll the json feed from Open Weather Map. I could map this to variable and starting working with it as a dictionary object. This turned out to be an absolute nightmare and has highlighted some holes in my knowledge with working with json/dictionaries in Python. Lukily there was another Python libary called PyOWM which has done all the hard for me.  Using PyOWM I was able to call the current weather status in London with the function

`weather_at_place('London,uk')`

Awsome.

I will write a lighting tutorial going through my automation script line by line in a new blog.

Once the script was working I was a able to set it as a daily scheduled task on PythonAnywhere and voila, everything was automated. 

## Thoughts So Far

Though initially the first couple of days were tough I find I'm enojoying this challenge more and more. The [#100DaysOfCode](https://twitter.com/hashtag/100DaysOfCode?src=hash) Twitter community is amazing and I've enjoyed interacting with others also participating challenge.

For the next 10 days I'm planning more CSS work . I want too play with Sass , disasemble this Jeklly blog and attempt to theme it from the ground up. 

To the next 10 days!

## Resources referenced

[CSS - The Missing Manual ](http://shop.oreilly.com/product/0636920036357.do) 
[CSS Tricks](https://css-tricks.com/) 
[Skeleton](http://getskeleton.com/) 
[PythonAnywhere](https://www.pythonanywhere.com)
[TweePy](http://www.tweepy.org/)
[PyOWM](https://github.com/csparpa/pyowm)