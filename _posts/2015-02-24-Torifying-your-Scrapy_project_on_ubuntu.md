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
  Howdy! This is an example blog post that shows several types of HTML content supported in this theme.
</div>

<strong> So without any due let's dive in </strong>

## First Install TOR(port 9050) relay and Polipo(port 8123) proxy ..will explain the text part letter in this article for now read the statement as english only !

**Reason:** Scrapy does not support SOCK Proxy(only http proxy) but in order to use TOR exit , one must transfer traffic via SOCK Proxy.. As a Solution ,Install Polipo proxy (default 8123 port)..which listens as a HTTP Proxy and can forward/receive traffic to/from SOCKS proxy ( for us  to-and-from TOR relay)



## Installing TOR and POLIPO:

### FOR TOR:

use this link for installation of TOR for your distro : https://www.torproject.org/docs/documentation.html.en

> <strong>For Ubuntu <strong> : DO NOT DOWNLOAD TOR Relay from Ubuntu repository ...Include Specific TOR project PPA instead

Use this page for ppa of your project: https://www.torproject.org/docs/debian.html.en#ubuntu

* example (UTOPIC UNICORN) *

