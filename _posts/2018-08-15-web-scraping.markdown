---
layout: post
title: "Web Scraping with Beautiful Soup"
date: 2018-08-15 10:34:25
categories: Maven Java Build
tags: featured
image: /assets/article_images/web-scrape/soup.jpg
---

Web scraping is the targeted collection of data from a website. Recently, web scraping made major headlines when a programmer was able to scrape LinkedIn, and identify employees of Immigrations and Customs Enforcement (ICE). Read the Vice artice [here.](https://motherboard.vice.com/en_us/article/435myg/programmer-used-linkedin-to-find-ice-employees-database) While this is not the most ethical example of its use; web scraping is a very powerful and interesting tool.

In this article I will explain web scraping using the Python library – Beautiful Soup. Not only does this library have an awesome name, it is also pretty easy to get working. All the examples will be scraping data from Craigslist, as I am currently working on a nationwide car search app using Craigslist postings.

# Getting Started

Some over-simplified background info:

- A website's data can be found in the HTML for that site
- In Chrome, right-clicking and then choosing “view page source”, will let you see the HTML

The following Python3 code will get you the HTML to Craigslist’s home page:

{% highlight python %}

import urllib.request
from bs4 import BeautifulSoup

request = urllib.request.Request('https://www.craigslist.org/about/sites')
response = urllib.request.urlopen(request)
page = BeautifulSoup(response.read().decode('utf-8'), "html.parser")

{% endhighlight %}

The next step is to locate and retrieve the data you want to scrape.

# Scraping URLs

As you saw above, in order to web scrape you need a URL. Craigslist’s main page has links to different regions around the US. Looking through the raw HTML it seems the links for each country are organized in HTML **\<div>**’s with the class “colmask”. The US section is first on the page and can be found with the following code

{% highlight python %}

USSection = page.find("div", {"class": "colmask"})

{% endhighlight %}

Here the **find()** function is return the first occurrence of a **\<div>** with the class “colmask”. Within the US column each state is within a **\<h4>** tag, followed by the links for the regions in **\<ul>** tags. The following code scrapes the HTML, creating a dictionary with the state names as keys, and an array of region URLs as values:

{% highlight python %}

data = {} # Remove territories
stateList = USSection.find_all("h4")[:-1]

for idx, state in enumerate(stateList):
regionHTML = USSection.find_all("ul")[idx].find_all("a")
regionList = []

    # iterate through list of region URLs
    for ii in regionHTML:
        # get URL for region
        regionList.append(ii['href'])

    data[state.text] = regionList

{% endhighlight %}

Example, abbreviated return:

{% highlight json %}
{
'Alabama': ['https://auburn.craigslist.org','https://huntsville.craigslist.org'],
'Alaska': ['https://anchorage.craigslist.org', 'https://fairbanks.craigslist.org'],
'Arizona': ['https://flagstaff.craigslist.org', 'https://mohave.craigslist.org']
}
{% endhighlight %}

# Scraping Posts

Now that you have a bunch of URLs it is time for the fun stuff. This example will cover the scraping of car postings. However – Craigslist has a ton of weird, interesting stuff you might want to check out. Using one of the base URLs we found above, we will find the post data for "tesla" in Auburn, AL:

{% highlight python %}

url = 'https://auburn.craigslist.org'
searchString = ‘/search/cta?query=tesla’

request = urllib.request.Request(url + searchString)
response = urllib.request.urlopen(request)
page = BeautifulSoup(
response.read().decode('utf-8'), 'html.parser')

posts = page.find_all('li', {'class': 'result-row'})

{% endhighlight %}

The posts are found in **\<li>** tags with the class “result-row”. The **find_all()** function returns a list of all the car post data for that URL. Using this data you can find the post locations, prices, pictures etc. It would be interesting to do some data analysis on some of the stuff in the future.

# Legal Stuff

Not all sites on the web are safe to scrape. Many have policies that make it illegal to “borrow” their data. It is advisable to check the web before trying to scrape a site.
