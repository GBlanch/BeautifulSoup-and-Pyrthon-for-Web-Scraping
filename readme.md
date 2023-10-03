# BeautifulSoup and Python for Web Scraping

## Table of contents

+ [Introduction](#introduction)
+ [Before deploying any code](#before-deploying-any-code)
+ [HTML variable peparation]()
+ [Patterns and Coding]

## Introduction

The purpose of this repository is to showcase a basic web scraping case and their best practices.


## Before deploying any code

Prior to retrieving any data from any website, we must know whether or not that website allows to do so. Under the terms and conditions of service of the website/service of most websites, it is normally specified if they allow web scraping or not. 

Another way to technically know if we can fetch certain website data is to check whether or not the web directory we’re trying to access is allowed to be scraped. We can check this by adding `robots.txt` at the end of the root directory of their website. For instance, in this case it will be:

![image](https://github.com/GBlanch/BeautifulSoup-and-Python-for-Web-Scraping/assets/136500426/ac71c1bb-ce67-4713-bd88-a16a01916461)

And if we check the `robots.txt` file, we can verify that the access to this directory is allowed by eBay, as shown below:

![image](https://github.com/GBlanch/BeautifulSoup-and-Python-for-Web-Scraping/assets/136500426/3a6c0cbf-9f1d-4323-ad33-5e0031b7e3d9)


Last but not least, and since there are some server and performance costs for the website owners everytime their data gets fetched, it is a nice and considered practice to avoid sending a big amount of URL request.

There's much more information about Web Scaping that can be found in the  website [ZenRows Blog - Web Scraping Best Practices and Tools 2023](https://www.zenrows.com/blog/web-scraping-best-practices#respect-robots-txt-sitemap)

As usual, we first import the needed libraries we will be needing. These being: `BeautifulSoup` so that we can interact and handle the data within the html website file, and `urllib.request` in order to get the website html file into a `Python` variable. Of course we'll also need `Pandas` to create and handle our Dataframes.

And so we begin by defining the variable for the html file:

![image](https://github.com/GBlanch/BeautifulSoup-and-Python-for-Web-Scraping/assets/136500426/951df0c8-ef6e-4315-91fd-a5e8f3ea6cd4)

Note that we can also assing a variable to the key word `nkw` on the URL address so that our script can be modified without having to access to any web browser.

Next we load the html file into memory with the function `uReq` and also to read and cloe the actual html file in our IDE:

![image](https://github.com/GBlanch/BeautifulSoup-and-Python-for-Web-Scraping/assets/136500426/914bbe90-bd0b-4333-bc31-c70953304071)

And so we have our data ready to be parsed with BeautifulSoup. We create a variable wirth the last variable we created above

![image](https://github.com/GBlanch/BeautifulSoup-and-Python-for-Web-Scraping/assets/136500426/51cf6a9a-764c-47af-84e1-81792ba8b26e)

When highlighting and inspecting any element of the website, we can see the `tag` and `class` that define them

![image](https://github.com/GBlanch/BeautifulSoup-and-Python-for-Web-Scraping/assets/136500426/2b3d8574-5efe-4b2e-a501-81c09d8a6d4d)

Now that we know the `tag` and `class` names, we can insert them as arguments into the `findAll()` function. We can fecth the values as a whole or individually, this is:

![image](https://github.com/GBlanch/BeautifulSoup-and-Python-for-Web-Scraping/assets/136500426/a8cde13e-987e-4231-bde1-6fa0cc1bdfc9)

We can also isolate only the numeric value with the currency sign

![image](https://github.com/GBlanch/BeautifulSoup-and-Python-for-Web-Scraping/assets/136500426/f87ffc1f-74f1-4312-84db-cf243aa34f9c)



