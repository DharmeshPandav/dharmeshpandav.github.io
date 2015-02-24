---
layout: post
title : Torifying  your Scrapy project on UBUNTU(Linux) and saving your spider from embarrassment of banning itself
tags:
- Scrapy
- TOR
- Polipo
- useragents
- ubuntu
permalink: torifying-scrapy-project-on-ubuntu
excerpt: This article contains the detailed walk-through of how to use TOR Relays in your scrapy project on ubuntu ( or linux) machine..this comprehensive guide covers the parts to download and install all the required dependencies to use scrapy on your distro as well the changes you must make to your project in order to be able to use that tor relays in your project..
---

<div class="message">
  Howdy! This articles covers the step-by-step guide for implementing http proxy middleware to use TOR relay in scrapy project..
</div>

<strong> So without any due let's dive in </strong>

### **First Install TOR(port 9050) relay and Polipo(port 8123) proxy** ..
will explain the technical part later in this article, for now read the statement as english only !

**Reason:** Scrapy does not support SOCK Proxy(only http proxy) but in order to use TOR exit , one must transfer traffic via SOCK Proxy.. As a Solution ,Install Polipo proxy (default 8123 port)..which listens as a HTTP Proxy and can forward/receive traffic to/from SOCKS proxy ( for us  to-and-from TOR relay)



### **Installing TOR and POLIPO:**

### **FOR TOR:**

use this link for installation of TOR for your distro : [TOR Project](https://www.torproject.org/docs/documentation.html.en)

> for ubuntu : DO NOT DOWNLOAD TOR Relay from Ubuntu repository ...Include Specific TOR project PPA instead

Use this page for selecting system specific PPA : [ubuntu PPA's](https://www.torproject.org/docs/debian.html.en#ubuntu)

example (UTOPIC UNICORN)

```bash

add this two line in package list file : /etc/apt/sources.list

deb http://deb.torproject.org/torproject.org utopic main
deb-src http://deb.torproject.org/torproject.org utopic main

#Then run

gpg --keyserver keys.gnupg.net --recv 886DDD89
gpg --export A3C4F0F979CAA22CDBA8F512EE8CBC9E886DDD89 | sudo apt-key add -

#post that, update your system and install tor using

$ apt-get update
$ apt-get install tor deb.torproject.org-keyring

```

### **FOR POLIPO:**

```bash
#install from default ubuntu base repository
sudo apt-get install polipo
```

#### **Second configure POLIPO to talk with TOR instead of acting as a stand alone proxy**

edit using vim : /etc/polipo/config

and add following line of code to instruct polipo to talk with TOR using SOCK connection

```bash
socksParentProxy = "localhost:9050"
socksProxyType = socks5
diskCacheRoot = ""
```

so far we have configured our TOR and POLIPO to communicate with each other...

* just to test if our tor/polipo setting is working or not...

1. Go to Firefox and change your proxy setting for http proxy to localhost:8123 remove all other scoks and other proxy and visit this site http://check.torproject.org/
2. If everything is setup correctly , you should see a message that this browser is configured properly to use tor network

### **Now comes the main part where you want to change the setting in your SCRAPY project to use this polipo/tor setup**

* ***add following code in your settings.py file***

```bash
#More comprehensive list can be found at
#http://techpatterns.com/forums/about304.html
USER_AGENT_LIST = [
    'Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/535.7 (KHTML, like Gecko) Chrome/16.0.912.36 Safari/535.7',
    'Mozilla/5.0 (Windows NT 6.2; Win64; x64; rv:16.0) Gecko/16.0 Firefox/16.0',
    'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_3) AppleWebKit/534.55.3 (KHTML, like Gecko) Version/5.1.3 Safari/534.53.10',
    ]

HTTP_PROXY = 'http://127.0.0.1:8123'

DOWNLOADER_MIDDLEWARES = {
    'myspider.middlewares.RandomUserAgentMiddleware': 400,
    'myspider.middlewares.ProxyMiddleware': 410,
    'scrapy.contrib.downloadermiddleware.useragent.UserAgentMiddleware': None,
}
```

* ***Create a middlewares.py file in your project root directory and add following line of code***

```bash
import random
from scrapy.conf import settings
from scrapy import log


class RandomUserAgentMiddleware(object):
    def process_request(self, request, spider):
        ua = random.choice(settings.get('USER_AGENT_LIST'))
        if ua:
            request.headers.setdefault('User-Agent', ua)
            #this is just to check which user agent is being used for request
            spider.log(
                u'User-Agent: {} {}'.format(request.headers.get('User-Agent'), request),
                level=log.DEBUG
            )


class ProxyMiddleware(object):
    def process_request(self, request, spider):
        request.meta['proxy'] = settings.get('HTTP_PROXY')

```

* ***now you are all set to run your scrapy spider using Proxy(tor + polipo and random user-agent)***

Happy Scraping ,use your bot responsibly , follow robot.txt rules strictly ..and avoid banning your spider self, use proper download delay ( as per scrapy recommendation more than 2)..

* **references:**

>1. http://ubuntuguide.org/wiki/Tor
>2. http://doc.scrapy.org/en/latest/topics/architecture.html
>3. http://pkmishra.github.io/blog/2013/03/18/how-to-run-scrapy-with-TOR-and-multiple-browser-agents-part-1-mac/


**useful commands:**

```bash
sudo service polipo start/stop/restart
sudo service tor start/stop/restart

scrapy shell --spider=spidername URL
#and then use all different commands to view and check the request and reponse

#check the proxy being used by firing this two command
request.meta
response.meta

#to view downloaded response body in browser
view(response)
```

<div class="message">
  Author of this article does not encourage IP infringement in any-form whatsoever...and Author is not responsible for any consequence of using methods ,mentioned above.
  this article is only for those who want to implement http middleware feature of Scrapy Framework..
  Respect others IP , scrap only if it is allowed to..respect ROBOT.txt rules strictly...with that being said...
  Happy Scrapping :D
</div>