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

The web is full of wonderfull and freely available information. Some of it is readily available and neetly organized (see (this repo)[https://github.com/caesar0301/awesome-public-datasets]) and some which is _really_ interesting is hiding in plain sight. I am speaking obout unstractured data on websites, which has either never been neatly organized and sits there locked away in html files.
Some of it is publically awailable and comes from a state of the arte database, but there is no easy way to access it, such as airbnb.com. 
The listings are freely accessible to anyonw who takes the time to brows their really nice portal, but if we wanted to do some statistical analysis then there is no easy way to get the data. This is where (web scraping)[https://en.wikipedia.org/wiki/Web_scraping] comes in.

I have allways had some questions I wanted to get from airbnb data, for example how many of them are in my city? What is the average price? Do lots of people leave reviews? Is it true that most reviews are positive? and so many more, and I am sure that you can come up with your own set of questions you would like to tickle out of such data.

So here I walk you through how I got *some* of the data, to answer some of these questions.

{:toc}

## The Plan

So do some data science on Airbnb data, we need a few things:

- A web scraping framework to get the data
- a Database to put this data into
- a server (could be your laptop) to operate the operation from.

First we are going to set up the environment to get (scrapy)[scrapy.org] to work, then write some python code to get our spider to do the tedious task of scraping for us, then we are going to do some exploratory analysis with the data.

Sounds good?
Here we go!

## Setting up the system





##


```python
class AirbnbSpider(scrapy.Spider):
    def parse(self, response):
        name = "airbnb"
        allowed_domains = ["airbnb.com"]
        
```

