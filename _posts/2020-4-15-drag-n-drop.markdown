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

Many languages already have libraries for various types of file conversion. In this case, Python has libraries like tabula and pdfminer [4] for the conversion of PDF to Excel. However, these libraries can be harder to implement and less effective on certain types of files. This leaves the use of the previously mentioned file conversion websites. One such website is [smallpdf.com](https://smallpdf.com/pdf-to-excel) which has a OCR based tool for the conversion of PDF to Excel. It is also closed-source and does not have an API, making it a good candidate for this kind of automation.

## Steps


![the Smallpdf ui](/assets/article_images/drag-n-drop/smallpdf.png)

When doing webscraping / automation, a useful approach is to start by detailing the steps you would use to do that task manually.

The basic steps to use the Smallpdf site are:

1. Load the site in the browser
2. Upload the file using drag'n'drop or file explorer
3. Download the converted file

With these steps layed out the next step is translate these into Python code that uses Selenium to automate the process.

## 1. Load the site in the browser


Selenium works using something called a WebDriver - a "browser automation framework"[2] that is able to control a web browser (Chrome, Firefox, etc.).
In this case, Python will be used to control the WebDriver and send the desired commands to the browser.

The following code will instantiate the a Webdriver for Firefox:
```Python
profile = webdriver.FirefoxProfile()
profile.set_preference('browser.download.manager.showWhenStarting', False)
profile.set_preference("browser.helperApps.neverAsk.saveToDisk",
                          "binary/octet-stream")
                          
driver = webdriver.Firefox(firefox_profile=profile)
```

Firefox has a default prompt that asks users before downloading and saving a file to disk.
As shown, a custom WebDriver profile can be used to prevent this prompt from being displayed.
This profile can also be used to configure where files are downloaded by default.

The website can be loaded using the created WebDriver:
```Python
driver.get("https://smallpdf.com/pdf-to-excel")
```

The Firefox browser should pop up on your machine. Note: Selenium allows the browser to be run in the background if desired.

## 2. Upload the file using drag'n'drop or file explorer


The following code will upload you pdf file to the Smallpdf site:

```Python
upload_box = WebDriverWait(driver, 60).until(
                    EC.visibility_of_element_located((By.ID , "__picker-input"))
                )
upload_box.send_keys("filename.pdf")
```

The ```WebDriverWait``` object, allows your driver to wait for elements to be visible, clickable, etc.
This will prevent your driver from giving commands to use web elements that are not yet rendered by the DOM.
In this case we are waiting for the file input form to load before we upload our file.

In a similar fashion, the convert button is then clicked by XPATH:

```Python
convert_to_excel_btn = WebDriverWait(driver, 60).until(
                    EC.element_to_be_clickable((By.XPATH , "//div[contains(string(), 'Convert to Excel')]"))
                )
convert_to_excel_btn.click()
```

If you are not familiar with XPATH it is used to query and locate elements in the HTML. [3] It comes in handy when doing anything with the web.

## 3. Download the converted file


Now that our file has been converted by the site it can be downloaded with the following code:

```Python
choose_btn = WebDriverWait(driver, 60).until(
                    EC.element_to_be_clickable((By.XPATH , "//button[contains(string(), 'Choose option')]"))
                )
choose_btn.click()

download_btn = WebDriverWait(driver, 60).until(
                    EC.element_to_be_clickable((By.XPATH , "//a[contains(string(), 'Download')]"))
                )
download_btn.click()

driver.close()
```

This chooses to download the pdf to disk. Smallpdf can also upload to things like Google Drive and Dropbox.

While this process is somewhat focused towards this specific site, the general approach is applicable to other file conversion sites such as image conversion, Powerpoint to PDF, etc.

## Sources

1. [Introduction to Selenium](https://www.guru99.com/introduction-to-selenium.html)
2. ["So what is Selenium Webdriver"](https://medium.com/@marikalam/so-what-is-selenium-webdriver-2a83a8b954bd)
3. ["An Introduction to XPATH]("https://blog.scrapinghub.com/2016/10/27/an-introduction-to-xpath-with-examples)
4. ["Python for Pdf"]("https://medium.com/@umerfarooq_26378/python-for-pdf-ef0fac2808b0)