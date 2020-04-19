# 7-Eleven Python
[![CircleCI](https://circleci.com/gh/SongGithub/7Eleven-Python/tree/master.svg?style=svg)](https://circleci.com/gh/SongGithub/7Eleven-Python/tree/master)


What is this program? This is an extremely simple program to use that lets you lock in a fuel price from the comfort of your computer. Using this is easier than using the mock location removed APK that is floating around the internet because you do not need to use any other apps to fake a GPS location, and it universally works whether you are using an iPhone or an Android device! 7-Eleven Python will also automatically lock in the maximum amount of fuel that you are allowed to lock in. For instance if you have $38.97 in your account and fuel costs $1.13 a litre you will be able to lock in 35 litres.
There is also a function that will automatically search a couple of websites for a reduction in fuel prices where if enabled, will automatically lock in that price for you. For example, if a service station has the price of Unleaded 98 for $1.28 per litre but only for an hour because it was a price error or they are out of normal unleaded fuel, it will still lock that price for you as long as the script is running in the background.

## Prerequisite

- You have Docker installed on your computer.

## Usage

Built Docker image has been published to the Dockerhub, so to run the app, simply:
```
docker run \
  -p 5000:5000 \
  songgithub/7eleven-python:e2e59
```

And browse to [localhost URL](http://localhost:5000)

Other environment variables you can specify at runtime:
```
BASE_URL: The URL for the 7-Eleven API.
TZ: Display time using the chosen timezone.
PRICE_URL: The URL for the fuel price API (currently defaults to the API at projectzerothree.info)
DEVICE_NAME: The name of the device reported on login to the 7-Eleven API (set by default in settings.py)
OS_VERSION: The Android OS version reported on login to the 7-Eleven API (set by default in settings.py)
APP_VERSION: The 7-Eleven app version reported on login to the 7-Eleven API (set by default in settings.py)
```
An example of running with environmental variables is as follows:

```bash
docker run -d \
  -e APP_VERSION=1.7.1 \
  -e TZ=Australia/Melbourne \
  --name 7Eleven_Fuel \
  -p 5000:5000 \
  songgithub/7eleven-python:e2e59
  ```
