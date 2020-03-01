# 7-Eleven Python
[![CircleCI](https://circleci.com/gh/SongGithub/7Eleven-Python/tree/master.svg?style=svg)](https://circleci.com/gh/SongGithub/7Eleven-Python/tree/master)


What is this program? This is an extremely simple program to use that lets you lock in a fuel price from the comfort of your computer. Using this is easier than using the mock location removed APK that is floating around the internet because you do not need to use any other apps to fake a GPS location, and it universally works whether you are using an iPhone or an Android device! 7-Eleven Python will also automatically lock in the maximum amount of fuel that you are allowed to lock in. For instance if you have $38.97 in your account and fuel costs $1.13 a litre you will be able to lock in 35 litres.
There is also a function that will automatically search a couple of websites for a reduction in fuel prices where if enabled, will automatically lock in that price for you. For example, if a service station has the price of Unleaded 98 for $1.28 per litre but only for an hour because it was a price error or they are out of normal unleaded fuel, it will still lock that price for you as long as the script is running in the background.


## Setup
Download Python3 from http://python.org/downloads/, and install it on your computer. It is a good idea to add Python to your PATH file after installing it, this makes it easier to run Python from any folder. To add Python to your Windows PATH you can follow this link https://geek-university.com/python/add-python-to-the-windows-path/.

With Python installed, download the *pip* installer if you haven't installed it already. Follow the instructions here https://pip.readthedocs.io/en/latest/installing/#install-pip.

Now that you have pip installed, you will need to install the dependencies in requirements.txt so that you can run the script. You can use the following pip command `pip install -r requirements.txt`.

Optional: You can use a [Google Maps API key](https://developers.google.com/maps/documentation/embed/get-api-key) with the 'Geocoding API' enabled if you want to get a stores location via Google. You should set this key in settings.py or using the `API_KEY` environment variable described below.

## Optional Security Setup

Uncomment the basic authentication sections in app.py to enable a login prompt before accessing the site. Update the 'BASIC_AUTH_USERNAME' and 'BASIC_AUTH_PASSWORD' values to set the username and password.

Uncomment the SSL section to enable HTTPS. Generate your own certificates using letsencrypt (https://letsencrypt.org/getting-started/) or generate a self signed certificate with OpenSSL.

`openssl req -new -newkey rsa:4096 -x509 -sha256 -days 3650 -nodes -out domain.crt -keyout domain.key`

Copy the crt and key files to the same directory as app.py and uncomment the last line in app.py and comment the app.run line above.

`app.run(host='0.0.0.0',port=443,ssl_context=context)`

## Docker Usage

`docker build -t fuellock .`

Then run the image in a container:
```
docker run -d \
  --name 7Eleven_Fuel \
  -p 5000:5000 \
  fuellock
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
  fuellock
  ```
