This is a lightning tutorial to show you how I have used Python to hook my twitter account to the Open Weather Map API using Tweepy, PyOWM , and PythonAnywhere.



# TweePy

TweePy is An easy-to-use Python library for accessing the Twitter API. Like, really easy.

Here is the code you will need to establish a connection to your twitter account

```
#login
auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)

#connect through a secure connection
auth.secure = True
api = tweepy.API(auth)

```
To get your keys sign in to <https://apps.twitter.com/> .

Here you can set up a new app .Fill in the form
Map the keys to varibles first or parse them strating in to the function . 

# PyOWM

Next Open Weather Map. Like Twitter you will also have to obtain an API by signing up <https://home.openweathermap.org/users/sign_up>

Once you have done that, sign in and you can find your OWM in the API key tab in your "home" section.

Simply parse that PI key into this function as a string

```
owm = OWM(<'API_key'>)
```

Now we can start having fun the with the Open Whether Map API. I set up the follow boilerplate code

```
obs = owm.weather_at_place('London,uk')
w = obs.get_weather()
```

Now "w" can call PyOWM functions like this.

```
w.get_wind()                  # {'speed': 4.6, 'deg': 330}
w.get_humidity()              # 87
w.get_temperature('celsius')  # {'temp_max': 10.5, 'temp': 9.7, 'temp_min': 9.0}
```
What I personally was the weather status , so all I had to call was:

```
w.get_status() # 'Clouds'
```

# Oh, We're Half Way There...

So 





