---
layout: post
title:  "Lightning Tutorial : Twitter Emoji Weather Forecast "
date:   2017-01-02 14:32:00 +0100
categories: tutorial
---

This is a lightning tutorial explain how I did this .

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Automated the <a href="https://twitter.com/hashtag/100DaysOfCode?src=hash">#100DaysOfCode</a> counter in my bio. Oh, and my twitter username shows Londons weather in emoji now. All powered by Tweepy! 😁</p>— Alex Chiu ☔ (@chiubaca) <a href="https://twitter.com/chiubaca/status/819581877048721408">January 12, 2017</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>



**Requirements:**
- Have [pip](https://pip.pypa.io/en/stable/installing/) installed .
- Basic Python knowledge.


**Time Required:**

30 minutes

# Set Up TweePy

TweePy is an easy-to-use Python library for accessing the Twitter API. 

To install:

```python
pip install tweepy
```

Here is the code you will need to establish a connection to your twitter account.

```python
import tweepy

#login
auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)

#connect through a secure connection
auth.secure = True
api = tweepy.API(auth)
```
To get your keys, sign in to <https://apps.twitter.com/> .

Here you can set up a new app then fill in the form to register your app.

![img](http://i1381.photobucket.com/albums/ah228/chiubaca/Jekyll%20Blog/register_zpsq2s5odax.png)

Make sure you parse the the keys in as a `"string"`.





##Updating Your Profile Using TweePy

Now we have established a connection to our Twitter account we can interact with our whole account through TweePy as if you were actually on Twitter. Because we have the power of Python too , you can do some pretty interesting things like streaming in a specfic hashtag , create twitter bots and perform some quite sophisticated data crawling if you wanted too. If you want to learn more about everything TweePy can do check out the [docs]() .

For this tutorial we just want to update our username and you can do so like this :

```python
 api.update_profile( "your-username" + "your-website","location", "description")
```
Thats it. Its almost too easy!

# PyOWM

Next, PyOWM.

PyOWM is a client Python wrapper library for the OpenWeatherMap (OWM) web API.

To install, simply:
```python
pip install PyOWM
```

Like the Twitter API you will also have to obtain an API by signing up at the following site. <https://home.openweathermap.org/users/sign_up>

Once you have done that, sign in and you can find your OWM in the "API keys" tab in your home section.

![img](http://i1381.photobucket.com/albums/ah228/chiubaca/Jekyll%20Blog/register2_zpstlup98ao.jpg)




Remember to `import pyowm`  . Then simply parse that API key into this function as a `"string"`.

```
owm = OWM(API_key)
```

## Check the weather with PyOWM

Now we can start having fun the with the Open Whether Map API. 

Set up the follow boilerplate code:

```python
obs = owm.weather_at_place('London,uk')
w = obs.get_weather()
```

Now `w` can call PyOWM functions like this.

```python
w.get_wind()                  # {'speed': 4.6, 'deg': 330}
w.get_humidity()              # 87
w.get_temperature('celsius')  # {'temp_max': 10.5, 'temp': 9.7, 'temp_min': 9.0}
```
What we want is the general weather status , which you can call like this:

```python
w.get_status() # returns'Clouds'
```

# Emojify 

We have now established how to update our Twitter username and also how to call a basic weather forecast with PyOWM. 

​So now lets mash the two APIs together with emojis :smile: . 

Here is some code that calls the weather via PyOWM and then uses Tweepy to update our Twitter username with an Emoji that corresponds with the weather. 

```python
# Weather Emoji Unicode
Clouds = u'\U00002601' #returns ☁  
Clear = u'\U00002600' #returns ☀
Rain =  u'\U00002614' #returns ☔
Extreme =  u'\U0001F300' #returns 🌀
Snow = u'\U00002744' #returns ❄
Thunderstorm = u'\U000026A1' #returns ⚡
Mist = u'\U0001F32B' #returns 🌤
Haze = u'\U0001F324' #returns 🌫
notsure = u'\U0001F648' #returns 🙈

if weather == "Clouds":
api.update_profile("chiubaca "+ Clouds,"chiubaca.github.io","London","Hey'Im Alex!")

elif weather == "Clear":
    api.update_profile("chiubaca "+ Clear,"chiubaca.github.io","Hey'Im Alex!")

elif weather == "Rain":
    api.update_profile("chiubaca "+ Rain,"chiubaca.github.io","Hey'Im Alex!")

elif weather == "Extreme":
    api.update_profile("chiubaca "+ Extreme,"chiubaca.github.io","Hey'Im Alex!")

elif weather == "Snow":
    api.update_profile("chiubaca "+ Snow,"chiubaca.github.io","London","Hey'Im Alex!")

elif weather == "Thunderstorm":
    api.update_profile("chiubaca "+ Thunderstorm,"chiubaca.github.io","London", "Hey'Im Alex!")

elif weather == "Haze":
    api.update_profile("chiubaca "+ Haze,"chiubaca.github.io","London",bio + counter+"/100")

elif weather == "Mist":
    api.update_profile("chiubaca "+ Mist,"chiubaca.github.io","London","Hey'Im Alex!")

else:
    api.update_profile("chiubaca "+ notsure,"chiubaca.github.io","London",bio + counter+"/100")
```

 Not the most elegant bit of code - If there are any suggestions to improve please drop a comment below. Nonetheless, I think it's pretty self explanatory. To break it down quickly...First we map the emoji unicode to some easier to understand variables. Next is just a rudimentary `if: elif: else:` crawl to go through all the possible weather outputs. The `else:` finishes on the monkey emoji just as precaution (kind of like a 404). Also the monkey emoji is my favourite so  wanted to sqeeze it somehow 🙈.

# Host on PythonAnywhere 

So we've written all this code but we still need a way to schedule this to run at least once a day.

Enter [PythonAnywhere](https://www.pythonanywhere.com) . A cloud service for learning, writing, hosting and running Python code. The beginner tier gives you access to two virtual Python consoles and lets you run  a single python script on a scheduled task for free. Pretty neat aye?

Once you're signed up, Go to your files section . You can either upload a python script you have already writen or create a new python file and paste the code in. 

Your final code should look something like this .

```python
#!/usr/bin/python2.7
import tweepy
from pyowm import OWM

#Twitter API Keys
consumer_key = "twitter-consumer-key"
consumer_secret = "twitter-consumer-secret-key"
access_token = "twitter-access-token"
access_token_secret = "twitter-access-token-secret"

#Twitter Authentication
auth = tweepy.OAuthHandler(owmconsumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)

#Open Weather Map API 
API_key = 'owm-api-key'
owm = OWM(API_key)

#quick variables to check weather in London
obs = owm.weather_at_place('London,uk')
w = obs.get_weather()
weather = w.get_status()

# Weather Emoji
Clouds = u'\U00002601'
Clear = u'\U00002600'
Rain =  u'\U00002614'
Extreme =  u'\U0001F300'
Snow = u'\U00002744'
Thunderstorm = u'\U000026A1'
Mist = u'\U0001F32B'
Haze = u'\U0001F324'
notsure = u'\U0001F648'


#Check Weather and return relevant Emoji
if weather == "Clouds":
    api.update_profile("chiubaca_bot "+ Clouds,"chiubaca.github.io","London",bio + counter +"/100")
elif weather == "Clear":
    api.update_profile("chiubaca_bot "+ Clear,"chiubaca.github.io","London",bio + counter+"/100")
elif weather == "Rain":
    api.update_profile("chiubaca_bot "+ Rain,"chiubaca.github.io","London",bio + counter+"/100")
elif weather == "Extreme":
    api.update_profile("chiubaca_bot "+ Extreme,"chiubaca.github.io","London",bio + counter+"/100")
elif weather == "Snow":
    api.update_profile("chiubaca_bot "+ Snow,"chiubaca.github.io","London",bio + counter+"/100")
elif weather == "Thunderstorm":
    api.update_profile("chiubaca_bot "+ Thunderstorm,"chiubaca.github.io","London",bio + counter+"/100")
elif weather == "Haze":
    api.update_profile("chiubaca_bot "+ Haze,"chiubaca.github.io","London",bio + counter+"/100")
elif weather == "Mist":
    api.update_profile("chiubaca_bot "+ Mist,"chiubaca.github.io","London",bio + counter+"/100")
else:
    api.update_profile("chiubaca_bot "+ notsure,"chiubaca.github.io","London",bio + counter+"/100")

print Clear+Rain+Extreme+Clouds+Snow+Thunderstorm+Haze+Mist+notsure
print("updated!")
```











