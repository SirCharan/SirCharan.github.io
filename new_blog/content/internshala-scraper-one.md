---
title: How To Use a Python Code To Scrape Internshala 
date: 2020-04-14
description: A brief description of Hugo Shortcodes
tags: ["Web Scraping"]
---

## And Automatically Apply To Each Internship Above 5K In Your Preferred Job Profile 
| Part 1-of-2
 
## Import The Necessary Libraries

Selenium is one of the most popular packages used for Web-Scraping, along with BeautifulSoup. Apart from simple Web-Scraping, Selenium provides the added advantage of being able to simulate the human behavior of scrolling and clicking.

Pandas is a common library used for data management. The Time and Random libraries are used to automatically delay and schedule tasks so that the website is not able to know that it's being operated by a bot.

{{< highlight python >}}
from selenium import webdriver
from bs4 import BeautifulSoup
import pandas as pd
import time
import random
{{< /highlight >}}

You may need to install some of these libraries with the pip install command.

## Open An Automated Chrome Window Using Webdriver

You will need to install ChromeDriver, based on the version of your Chrome Browser, and then provide the path to its directory.

{{< highlight python >}}
internshala = webdriver.Chrome("path/chromedriver_win32/chromedriver.exe")
{{< /highlight >}}

## Open Internshala

{{< highlight python >}}
internshala.get('https://internshala.com')
{{< /highlight >}}








Add alt text
No alt text provided for this image

## Understanding The HTML Elements

You will now need to access individual HTML elements on the page. To do so, simply select any field you want, i.e. stipend and select the text and right-click over it and click "Inspect".








Add alt text
No alt text provided for this image

Hover your mouse pointer over the HTML code and you will see the corresponding parts of the page highlighted. These are the HTML elements corresponding to each of the text fields on the pages.








Add alt text
No alt text provided for this image

## Scraping Data Using Selenium

{{< highlight python >}}
Stipend=internshala.find_elements_by_xpath('//span[@class="{}"]'.format("stipend"))
{{< /highlight >}}

This command will return a list of Selenium web.elements to "Stipend".








Add alt text
No alt text provided for this image

To get the stipend amount, you need to:

1. Access the first element of the list
2. Convert it to text by using .text method
3. Split to get the stipend amount as a number







Add alt text
No alt text provided for this image

The whole process can be simplified and written in one line as:-

{{< highlight python>}}
stipend_amount=internshala.find_elements_by_xpath('//span[@class={}"]'.format("stipend"))[0].text.split(' ')[0]
{{< /highlight >}}

Similar commands for each of the fields "Profile", "Company Name"

{{< highlight python>}}
profile_role=internshala.find_elements_by_xpath('//div[@class="{}"]'.format("heading_4_5 profile"))[0].text

company_name=internshala.find_elements_by_xpath('//div[@class="{}"]'.format("heading_6 company_name"))[0].text
{{< /highlight >}}

You can use a For Loop and .append method to append every element in text form to a new list.

{{< highlight python>}}
for i in range(len(stipend):
stipend.append(stipend_amount[i])
role.append(profile_role[i])
company.append(company_name[i])
{{< /highlight >}}


Using the above 3 lists, we can create a DataFrame, with the same Titles

{{< highlight python>}}
df={"Stipend Amount":stipend, "Profile Role":role, "Company Name":company}
df=pd.DataFrame(df)
{{< /highlight >}}







Add alt text
No alt text provided for this image

You can sort the list by the stipend amount. This will sort the whole DataFrame in decreasing order starting from the maximum stipend.

{{< highlight python >}}
df.sort_values(by=['Stipend Amount'], ascending=False)
{{< /highlight >}}

Then save it in an excel file

{{< highlight python >}}
df.to_excel('path/file.xlsx')
{{< /highlight >}}








Add alt text
No alt text provided for this image

Or a CSV

{{< highlight python >}}
df.to_csv('path/file.csv')
{{< /highlight >}}

Once in Excel, you can sort them in any way you want and add filters that Internshala doesn't have on their platform.

PS: Had to divide this post into 2 parts due to lack of space. The second part of this post will contain how to automatically apply and will be out next Friday the 19th, 5 PM.

Connect or "Follow" me to make sure you don't miss it. I will upload the full working code on GitHub soon.
