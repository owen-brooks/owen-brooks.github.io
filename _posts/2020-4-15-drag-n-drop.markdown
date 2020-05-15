---
layout: post
title: "Drag'n'drop File Conversion with Selenium & Python"
date: 2020-04-10 08:34:25
categories: Python Selenium
tags: featured
image: /assets/article_images/drag-n-drop/palm.jpg
---

"SELENIUM is a free (open-source) automated testing framework used to validate web applications across different browsers and platforms."[1]
It can be especially useful in the automation of file conversion websites where a user uploads their file in one format and then downloads the converted file in the desired format.

Many languages already have libraries for various types of file conversion. In this case, Python has libraries like tabula and pdfminer for the conversion of PDF's to Excel. However, these libraries can be harder to implement and less effective on certain types of files. This leaves the use of the previously mentioned file conversion websites. One such website is [smallpdf.com](https://smallpdf.com/pdf-to-excel) which has a OCR based tool for the conversion of PDF's to Excel.

## Steps

![the smallpdf ui](/assets/article_images/drag-n-drop/smallpdf.png)

When doing webscraping / automation, a useful approach is to start by detailing the steps you would use to do that task manually.

The basic steps to use the smallpdf site are:

1. load the site in the browser
2. upload the file using drag'n'drop or file explorer
3. download the converted file

With these steps layed out the next step is translate these into Python code that uses Selenium to automate the process.

## Sources

1. [Introduction to Selenium](https://www.guru99.com/introduction-to-selenium.html)
2. ["So what is Selenium Webdriver"](https://medium.com/@marikalam/so-what-is-selenium-webdriver-2a83a8b954bd)