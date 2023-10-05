# Python with BeautifulSoup for Web Scraping

## Table of contents

+ [Introduction](#introduction)
+ [Before deploying any code](#before-deploying-any-code)
+ [Good to code](#good-to-code)
+ [Inspecting the HTML page and noticing patterns](#inspecting-the-html-page-and-noticing-patterns)
+ [Basic data cleaning and dataframes extraction](#basic-data-cleaning-and-dataframes-extraction)
+ [Epilogue](#epilogue)

## Introduction

The purpose of this repository is to showcase a basic web scraping case and their best practices.

Please beware that **web scraping** can become pernicious to their web owners and therefore **mustn’t be practiced without knowing which permissions we are granted by them beforehand.**
&nbsp;  
&nbsp;

## Before deploying any code


Prior to retrieving any data from any website, we must know whether or not that website allows to do so. Under the `terms and conditions of service` of the website/service of most websites, it is normally specified whether they allow web scraping or not. 

Another way to acknowledge the legitimacy of our web scaping practices is to check whether or not the web directory we’re trying to access is permitted to be scraped. We can check this by adding `robots.txt` at the end of the root directory of their website. 
For instance, in this case it is:
&nbsp;    

![image](https://github.com/GBlanch/BeautifulSoup-and-Python-for-Web-Scraping/assets/136500426/ac71c1bb-ce67-4713-bd88-a16a01916461)

&nbsp;   

And if we check `eBay`'s `robots.txt` file, we can verify that the access to this directory is allowed, as shown below:

![image](https://github.com/GBlanch/BeautifulSoup-and-Python-for-Web-Scraping/assets/136500426/3a6c0cbf-9f1d-4323-ad33-5e0031b7e3d9)


Last but not least, and since there are some server and performance costs for the website owners every time their data gets fetched, it is a nice and considered practice to avoid sending a big amount of URL requests.

There's much more information about Web Scaping that can be found in the  website [ZenRows Blog - Web Scraping Best Practices and Tools 2023](https://www.zenrows.com/blog/web-scraping-best-practices#respect-robots-txt-sitemap)
&nbsp;    
&nbsp;    
[Back to Table of Contents](#table-of-contents)
&nbsp;    
&nbsp;  

## Good to code

As usual, we first import the needed libraries we will be needing. 

These happen to be: `BeautifulSoup` to interact and handle the data within the `html file`, `urllib.request` in order to get this `html file` into a `Python` variable named `client`, and not unexpectedly, we also will utilize `Pandas` and `NumPy` to create and manipulate our Dataframes as a matter of course.

And so we also proceed by defining the variable for the `html file` by passing its URL address into a Python variable `url`. This is to code:

![image](https://github.com/GBlanch/Python-with-BeautifulSoup-for-Web-Scraping/assets/136500426/c1d25f0c-2979-4d2d-8a96-22cd53b0c94d)


Please notice that we can also assign a variable `key_word_search` to replace anytime we need the content of key word `nkw` on the URL address we have just passed. We have placed some curly brackets `{}` in its place. This way the target of our scraping script shall be modified without having to access to any web browser, or even if we just decide to automate other processes.

Next we load the `html file` into memory with the function `uReq` from the library `urllib.request`. For that we will define the variable `client` which will contain the http client object. We also can have a look at the content of this object, as follows below :

![image](https://github.com/GBlanch/BeautifulSoup-and-Python-for-Web-Scraping/assets/136500426/35c9b713-cd09-4cba-8bfa-c1689472e055)


As you may certainly know, this output (html page) is rather large and not easy to read, and here's where `BeautifulSoup` will come extremely handy. Once the variable `html_page` is finally read/assigned as a html file, we will also close the client object:

![image](https://github.com/GBlanch/BeautifulSoup-and-Python-for-Web-Scraping/assets/136500426/f11969e2-75e5-412d-a4d7-21f31b6e83e5)



And so we have our data ready to be parsed with `BeautifulSoup`. We create a new variable `page_soup` and we will assign to it the last variable `html_page` which contais the html file as explained before. This results as follows: 

![image](https://github.com/GBlanch/BeautifulSoup-and-Python-for-Web-Scraping/assets/136500426/51cf6a9a-764c-47af-84e1-81792ba8b26e)

Now that we have our soup object ready to be manipulated, we are finally ready to move onto the next stage.

[Back to Table of Contents](#table-of-contents)
&nbsp;    
&nbsp;  

## Inspecting the HTML page and noticing patterns


We open `Google Inspect` (Ctrl + Shift + C) to start knowing more about how the html page was architected.
When highlighting and inspecting any element of the website, i.e. _USD price_ for a _Hiking Pocket Compass_, we can see the `tag` and `class` that define each of them :

![image](https://github.com/GBlanch/BeautifulSoup-and-Python-for-Web-Scraping/assets/136500426/2b3d8574-5efe-4b2e-a501-81c09d8a6d4d)

And so we can identify that for _this item_, its `tag` and `class` are `span` and `s-item__price` respectively. 
These define the price in the HTML code, and so we can insert them as arguments into the `findAll()` function to track the price down. We can fetch therefore the values as a whole list - whose type is `bs4.ResultSet`- , as an interval, or even individually. This is to code:

![image](https://github.com/GBlanch/BeautifulSoup-and-Python-for-Web-Scraping/assets/136500426/98911b97-407b-4828-a092-481a89e544e2)

We can also even isolate only the price value with the currency sign of a single observation as shown below with the `BeautifulSoup` method `.text`. Also, looking into the type of a single element of the list, we confirm they are strings:

![image](https://github.com/GBlanch/BeautifulSoup-and-Python-for-Web-Scraping/assets/136500426/1310a4ab-b566-4ad1-95a8-288b4db3d2fc)

NB: In this markdown file, I've just showcased a portion of the entire workload of HTML code inspection ,data manipulation and cleaning for this project. You can `find the rest of this work` in my original [`scraping script here`](https://github.com/GBlanch/Python-with-BeautifulSoup-for-Web-Scraping/blob/main/1.ebay/web_scrap_ebay_script.ipynb). Likewise, in this script you can find more coding in regards to other types of `tags` and `classes`, and how to navigate through these in a HTML page.


[Back to Table of Contents](#table-of-contents)
&nbsp;    
&nbsp;  




## Basic data cleaning and dataframes extraction


Since we want to apply theses filtering and the rest of the cleaning procedures to the entire findings - not just to one single observation -, we will store the whole list in a variable named `span_tag` so that we can perform the same operations to them all. 

To do this, we will declare the an empty list `prices` and we will run it into a for-loop. In this iteration, we will append the whole value of each `span_tag` string, except for their 1st position. All this is:


![image](https://github.com/GBlanch/Python-with-BeautifulSoup-for-Web-Scraping/assets/136500426/79451d53-b920-43a3-a726-e31f8326c398)



Please notice the omission  of the 1st position -`$` symbol- of each string in the for-loop by means of the indexing `[1:]`. We could have used the `.strip()` method to achieve this end as well. 

Taking a short brake from this example for the list `prices`, we look briefly just into another example of some other operations of data manipulation. 

I.e., to get the `shipping price` of the same website, and after having identified the `tag` and `class` that define them in the HTML page ( following image ), we can code as follows in the second image below:

![image](https://github.com/GBlanch/Python-with-BeautifulSoup-for-Web-Scraping/assets/136500426/605ee04b-b5ee-45e8-ad88-e011fc1409e7)


![image](https://github.com/GBlanch/Python-with-BeautifulSoup-for-Web-Scraping/assets/136500426/1df7183b-bb33-411a-950a-96c946f34089)

The word `shipping` as well as the `$` symbol is appearing in the result of the list `shipprice`. Hence we need to apply the `text` and `replace` functions, respectively. This reads as follows:

![image](https://github.com/GBlanch/Python-with-BeautifulSoup-for-Web-Scraping/assets/136500426/7a32d6ee-e58b-4e2c-ab28-484d2750d726)

And so we have obtained solely the value of the price without any other irrelevant data.

Having mentioned this other case and going back to our list `prices` - and as we saw before -, the type of each element within the list is still a string, therefore we ought to cast them into a numeric value. We will utilize the function `to_numeric` from `Pandas `to attain this:


![image](https://github.com/GBlanch/BeautifulSoup-and-Python-for-Web-Scraping/assets/136500426/234fae45-b34d-4abd-b7a7-0daefa0dc06b)


And so Python complains about not being able to parse the non-numerical strings as shown in the Console output. That is why we are going to utilize the argument `coerce` within the mentioned function `to_numeric`, as the script reads below:

![image](https://github.com/GBlanch/BeautifulSoup-and-Python-for-Web-Scraping/assets/136500426/f4085677-3651-4d2d-8a0a-8d0b4125fe79)


We next get rid of the `NaN` values. We confirm there are 3 amongst the original dataframe `df`, and after having declared a new dataframe `df_hike_gear_p` , we will remove these and we confirm they don't exist anymore. This is to code:

![image](https://github.com/GBlanch/Python-with-BeautifulSoup-for-Web-Scraping/assets/136500426/d7638311-c448-489c-9e09-2575a94e31a3)

We will perform some quick data manipulation in order to give the future csv file an `index` column, as well as a column name for the data to be extracted. Both of these operations result as:

![image](https://github.com/GBlanch/Python-with-BeautifulSoup-for-Web-Scraping/assets/136500426/98133f7f-5f7c-4113-a579-ece3b1626750)


We will finally store this data into a csv file. Before we do so, we double check there are no null values after some data manipulation. After this, we can parse this dataframe `df_hike_gear_p` into a `csv` file with the method `to_csv` .This new csv file `df_hg_price` will be stored in the local directory where this web scraping script is running:

![image](https://github.com/GBlanch/Python-with-BeautifulSoup-for-Web-Scraping/assets/136500426/dd47746b-e322-47aa-9dc4-bf884e66d256)

![image](https://github.com/GBlanch/Python-with-BeautifulSoup-for-Web-Scraping/assets/136500426/9c720db0-65f4-4d2a-bce5-89ebef5e8dca)

In regards of how to mention dataframes and their csv files, there is a specific note at the beginning of the script I mentioned in this last chapter `Epilogue`, which follows below.
&nbsp;    
&nbsp;  

## Epilogue


To check out more details and operations performed during this brief project, you can have a look [`here`](https://github.com/GBlanch/Python-with-BeautifulSoup-for-Web-Scraping/blob/main/1.ebay/web_scrap_ebay_script.ipynb) to the entire `script` I elaborated in order to create part of this repository. 

Feel also free to browse [`this repository`](https://github.com/GBlanch/Python-with-BeautifulSoup-for-Web-Scraping/tree/main) to see other `web scraping works` that I'm currently developing. 

Thanks for reading this!

[Back to Table of Contents](#table-of-contents)







