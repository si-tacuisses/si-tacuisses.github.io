---
layout: post
title: "Webscraping Airbnb with scrapy"
modified:
categories: blog
excerpt: "Getting data from Airbnb and do some interesting analysis"
tags: [tutorial, python, webscraping]
image:
  feature: luccaairbnbmap.png
date: 2016-02-27
comments: true
share: true
math: false
code: true
mma: false
---

The web is full of wonderful and freely available information. Some of it is readily available and neatly organized (see [this repo](https://github.com/caesar0301/awesome-public-datasets) and some which is _really_ interesting is hiding in plain sight. I am speaking about unstructured data on websites, which has either never been organized or the owner does not offers easy access and sits there locked away in dusty HTML files.
Some of this wealth of data I am speaking about is publicly available and comes from a state of the art databases, but there is no easy way to access it, such as airbnb.com. 
The listings on the Airbnb are freely accessible to anyone who takes the time to brows their really nice portal, but if we wanted to do some statistical analysis then there is no easy way to get the data. This is where [web scraping](https://en.wikipedia.org/wiki/Web_scraping) comes in.

I have allays had some questions I wanted ask airbnb, for example how many of them are in my city? What is the average price? Do lots of people leave reviews? Is it true that most reviews are positive? and so many more. I am sure that you can come up with your own set of questions you would like to tickle out of such data.

So here I walk you through how to get *some* of the data, to answer some of these questions.

* Table of Contents
{:toc}

## The Plan

To do some data science on Airbnb data, we need a few things:

- A web scraping framework to get the data
- A Database to put this data into
- A server (could be your laptop)
- A statistics package to evaluate, estimate and explore the data.

First we are going to set up the environment to get [scrapy](scrapy.org) to work, then write some python code to get our spider to do the tedious task of scraping for us. After the all is said and done we are going to do some exploratory analysis with the data.

Sounds good?
Here we go!

## Setting up the system


{% gist 2947907 %}


## Getting started with Scrapy


```python
class AirbnbSpider(scrapy.Spider):
    def parse(self, response):
        name = "airbnb"
        allowed_domains = ["airbnb.com"]
        
```



## Run the Query



## Explore the data


## Plot the Data on a Map






