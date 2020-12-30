Year 2020 has been quite hard for hardware supply. Graphics Cards are out of stock everywhere. Nobody can grab the
new generation (AMD RX 6000 series, NVIDIA GeForce RTX 3000 series). Even older generations are hard to find.
**GraphicRestock** is a bot that crawl retailers websites and notify when a product is available.

# Setup

Based on Debian 10:

```
apt install python3-selenium python3-sqlalchemy python3-tweepy firefox-esr
curl -L -s https://github.com/mozilla/geckodriver/releases/download/v0.28.0/geckodriver-v0.28.0-linux64.tar.gz | tar xvpzf - -C /usr/local/bin/
chown root:root /usr/local/bin/geckodriver
chmod +x /usr/local/bin/geckodriver
```

# Configure

Configuration file example can be found [here](config.json.example).

Options:
* **twitter.consumer_key**: key of your Twitter application
* **twitter.consumer_secret**: secret of your Twitter application
* **twitter.access_token**: authentication token generated by [twitter_auth.py](twitter_auth.py)
* **twitter.access_token_secret**: authentication token secret generated by [twitter_auth.py](twitter_auth.py)
* **urls**: list of retailers web pages (they need to respect crawlers' format)
* **executable_path** (optional): path to selenium driver (firefox/gecko browser)


# Twitter authentication

Create a configuration file with **twitter.consumer_key** and **twitter.consumer_secret** parameters.

Then authenticate:

```
python3 twitter_auth.py
```

You will have to open the URL and authenticate:

```
Please go to https://api.twitter.com/oauth/authorize?oauth_token=****

```
Click on **Authorize app**. A verifier code will be shown. Go back to your console and enter the code.

```
Verifier:*******
```

Tokens will be created:

```
access_token = *****
access_token_secret = ****
```

Finally, write them to configuration file in **twitter.access_token** and **twitter.access_token_secret** parameters.


# Usage

```
python3 main.py --help
```

# How to contribute

First things first, check issues to ensure the feature or bug you are facing is not already declared.

Pull requests are highly appreciated.

Please lint your code:

```
docker run -it -v $(pwd):/mnt/ --rm debian:10 bash
apt-get update && apt-get upgrade -y && apt-get install -y python3-pip git
pip3 install pre-commit
cd /mnt
pre-commit run --all-files
```

Happy coding!


# Disclaimer

Crawling a website should be used with caution. Please check with retailers if the bot respects the terms of use for
their websites. Authors of the bot are not responsible of the bot usage.