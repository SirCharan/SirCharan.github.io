---
title: How To Use a Python Code To Scrape Internshala - Part 2
date: 2020-04-13
description: A brief guide to setup KaTeX
tags: ["Web Scraping"]
math: true
---
 
## And Automatically Apply To Each Internship Above 5K In Your Preferred Job Profile 
| Part 2-of-2
 
If you've landed here directly, and missed my previous article, take a look at Part 1 here...

And if you've already done that, you must be familiar with this code written below-

## Importing The Libraries

{{< highlight python >}} 
from selenium import webdriver
from bs4 import BeautifulSoup
import pandas as pd
import time
import random 
{{< /highlight>}}

## Opening Internshala In an Automated Chrome Window

{{< highlight python >}}
internshala = webdriver.Chrome("path/chromedriver_win32/chromedriver.exe")
internshala.get('https://internshala.com')
{{< /highlight >}}

## Scraping out the Stipend, Company Name and Profile

{{< highlight python >}}
stipend_amount=internshala.find_elements_by_xpath('//span[@class={}"]'.format("stipend"))[0].text.split(' ')[0]

profile_role=internshala.find_elements_by_xpath('//div[@class="{}"]'.format("heading_4_5 profile"))[0].text

company_name=internshala.find_elements_by_xpath('//div[@class="{}"]'.format("heading_6 company_name"))[0].text
{{< /highlight>}}

## And Saving Them All In a List

{{< highlight python >}}
for i in range(len(stipend):
  stipend.append(stipend_amount[i])
  role.append(profile_role[i])
  company.append(company_name[i])
{{< /highlight >}}

## Let's Jump Right Into The Most Interesting Part Now!

We'll be utilizing the real power of Selenium, which is the ability to simulate human behavior!

But for that, we need to filter out and select the internships we need to apply for.

## Filtering out Internships of our preference

Since we already have the internship details stored in 3 lists from the previous post (namely stipend, role and company) we'll run a for loop over all the internships offered, and since our original target was to automatically apply for every internship above 5k/month, let's create an if statement for that.

I like to apply for "SEO", so I'll create another if to filter that out.

{{< highlight python >}}
for i in range(len(stipend)):
  if(int(stipend[i]>5000):
    if(role[i]=='SEO'):
{{< /highlight >}}     
                        
But wait a min...

There are many stipend amounts which are not in integer format, like the 'Unpaid' and 'Performance-based' ones. You need to take special care of them, or else you'll run the risk of getting an error.

A very simple way to do this is to use an if statement like-

{{< highlight python >}} 
if(str(stipend)!='Unpaid' and int(stipend)>5000): 
{{< /highlight >}}
 
Now that we've filtered out the internships, lets finally learn how to apply!

## How To Apply

To simulate the human behavior of clicking, simply use the inbuilt .click() method in Selenium.

{{< highlight python >}}
for i in range(len(stipend)):
  if(role[i]=='SEO'):
    if(int(stipend[i])>5000):
      company[i].click()
{{< /highlight>}}
  
To click on the apply now button, repeat the same process used in the last article. Right-click and inspect to get the HTML element, and then use the .click() method.








Add alt text
No alt text provided for this image

A bit of hit-and-trial would tell you that you have to use index [1] instead of [0].

{{< highlight python >}}
apply_now=internshala.find_elements_by_xpath('//div[@class="{}"]' .format("buttons_container")

apply_now[1].click()
{{< /highlight >}}

Repeat the same process to "click" on the "Proceed to application" button.








Add alt text
No alt text provided for this image

{{< highlight python >}}
application_button=internshala.find_elements_by_xpath('//div[@id="{}"]' .format("application_button"))


application_button[0].click()
{{< /highlight >}}

You can throw in a random sleep function with a random time delay to "confuse" the website.

{{< highlight python >}}
time.sleep(random.randint(1,5))
{{< /highlight >}}

This will make it almost impossible to detect that the actions are being performed by a bot!!!
This function would delay the action by a new random number between 1 and 5 seconds everytime.

{{< highlight python >}}
time.sleep(random.randint(1,5))
{{< /highlight >}}


You have now reached your final screen. 

Just 2 more clicks, and we're done!

Select the option "Copy from your last Search Engine Optimization (SEO) application & edit".








Add alt text
No alt text provided for this image

Be careful, this time it is an 'a' element instead of a 'div' element, but the process remains the same.

{{< highlight python >}}
time.sleep(random.randint(1,5))

application_text=internshala.find_elements_by_xpath('//a[@class="{}"]'. format("copyCoverLetterTitle"))

application_text[0].click()
{{< /highlight >}}

Finally, click on the submit button to end the show.








Add alt text
No alt text provided for this image
BUT
But if you've used the platform before, you'll know a very irritating popup comes up which shows you the "Similar internships you may apply to".








Add alt text
No alt text provided for this image

But anyway, a good coder should be able to solve anything, even an "UnexpectedAlertPresentException" (that's just a fancy name give to the popup which appears, don't worry, just copy).

So here we go..

{{< highlight python >}}
try:
  submit=internshala.find_elements_by_xpath('//div[@class="{}"]'.format("submit_button_container"))  
  submit[0].click()
except UnexpectedAlertPresentException:
  time.sleep(ra)
internshala.get('https://internshala.com/internships/matching-preferences')
{{< /highlight >}}

And we're done!!!
For further security, we can try many ways to hide our fingerprints such as auto-proxy switching, multi-threading and auto time-zone change.


Connect with me so that you don't miss out!
