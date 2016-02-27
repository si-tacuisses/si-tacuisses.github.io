---
layout: post
title: "Webscraping Airbnb with scrapy"
modified:
categories: blog
excerpt: "Getting data from Airbnb and do some interesting analysis"
tags: [tutorial, python, webscraping]
image:
  feature: 
date: 2015-05-16T10:41:03+02:00
comments: true
share: true
math: false
code: true
mma: false
---




```python
class AirbnbSpider(scrapy.Spider):
    def parse(self, response):
        name = "airbnb"
        allowed_domains = ["airbnb.com"]

```

