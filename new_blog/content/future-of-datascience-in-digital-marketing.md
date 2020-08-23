---
title: The Future Of Data Science In Digital Marketing
date: 2020-04-13
description: Guide to emoji usage in Hugo
tags: ["Data Science", "SEO", "Digital Marketing"]
---

Before I start, let me admit something honestly...

The original title of this article was going to be-

>"How I Performed a Proper Keyword Research And Optimized A GoogleAds Campaign Using Data Science and a Bit of Machine Learning for the largest financial lead generating company in the world-The Investoo Group"

But I figured that the current one would get me more clicks, and you did click on it, so here we go...😆

Due to lack of space, had to break the whole article down into 2 parts: Part 1 will detail out what I did, and part 2 will contain the complete Python code...

## Future Of Data Science

Data science has been a core component in organizations of all kinds and everywhere, and still continues to evolve as one of the most promising and in-demand career paths for skilled professionals.

But one place it's NOT dominant currently, is in the field of Digital Marketing.

But I see that going to change soon.
So let's start with just one of the uses of Data Science in Digital Marketing, which is performing proper keyword research, tracking and optimizing a GoogleAds campaign.

Here I will be describing the procedure which I used, to find the optimized keywords around the seed keyword "Bitcoin" and set-up the perfect ad-campaign. It involved a basic understanding of Data Science, Python and Machine Learning (a bit of the feature selection algorithms and PCA).

Data Gathering
I used SEMRush's Keyword Magic Tool to find out all the secondary keywords around the term "bitcoin". The search yielded 50K keywords of all kinds.

SEMRush Keyword Tool 
For each of the keywords, SEMRush provides the following metrics too:

* *Volume:* Average number of monthly searches over the past 12 month period.
* *Keyword Difficulty (%KD):* Keyword Difficulty Index is a percentage from 0-100% which shows you how hard is it to rank for a particular keyword organically on Google's search results.
* *Competitive Density (CD):* Competitive Density is a number between 0 to 1.00 which shows the level of competition between advertisers bidding for a specific keyword within their PPC campaigns.
* *Results:* The number of URLs displayed in the organic search results for the given keyword.
* *Cost Per Click (CPC):* Average price in $ the advertisers pay for a single click on the ad.

The data could be exported to Excel from SEMRush and imported to Python.

## Data Categorization
The next step involves making groups of these keywords and categorizing them based on their intent and secondary keywords

I made a Python program to go thru the entire list and find out all the secondary keywords around the main keyword Bitcoin, and divided the entire data based on their secondary keywords into 37 groups. 

Then I repeated the whole process again and divided these groups further into 87 subgroups.

![this is a an alt](/static/0.png)

This was achieved by using the NLTK library in Python using Tokenization and Lemmatization. (To be explained in the part-2 of this article, with the Python code)

## Data Cleaning
The process of data cleaning involves 2 steps:

### 1. Data Cleaning by Volume

I made a Python program to iterate over all the subgroups and choose the most popular keywords by either having 500+ volume OR the being the top 10 of their respective group (if group didn't have 10 keywords with a 500+ volume).

Now we have taken the best entries from each sub-group. We have ensured that the keywords we now have, have high volume, and also ensured that each subgroup gets represented in the final set.

This reduced the original list of 50k to 1.5k.

### 2. Data Cleaning by Trend

The trend gives a list of 12 numbers which signify the relative popularity per month on a scale of 0 to 1. 

Example of that data is-

0.20, 0.30, 0.37, 0.25, 0.20, 0.16, 0.16, 0.16, 0.16, 0.20, 0.30, 1.00 

As we can see that this keyword is gaining popularity in the later months, (increasing from 0.16 to 0.20 to 0.30 to 1.00). This is a kind of keyword we should consider, even if it has less volume, as its gaining popularity recently. 

Conversely, we should drop keywords losing significance in the latest months as they seem no longer relevant currently.

I ran a code to iterate over each list and remove entries that were losing significance in recent times.

>This left my final list down to 957 keywords.

## The Mathematics Involved

Now I'll just be keeping the data of Volume, Keyword Difficulty(KD), Competitive Density(CD) and CPC. We need to "score" every keyword one these parameters to find the best keywords.

So I did a brief analysis of the data to get statistical information such as-

No alt text provided for this image

The information about the mean, median along with the max and minimum gives us a general idea of how the data is distributed.

Since the range of each feature varies a lot, like for example volume is in thousands, KD is 0-100, CD is 0-1) so we need to normalize all these to one single scale

## Normalization Of Data

There are 3 formulas used for normalization

No alt text provided for this image
No alt text provided for this image
No alt text provided for this image

The decision on which of these 3 formulas to use is based on many things I had to consider manually such as the range, mean, variance, median, zeroes in the data and outliers among other factors.

## Scoring

Now I assigned every keyword a score indicating the degree to which we should push to bid on it.

Before calculating the final score, I divided it into two intermediary scores: the Competition Score (based on how difficult it is to rank) and the Cost Score (based on how worth that keyword is compared to others).

No alt text provided for this image
No alt text provided for this image
No alt text provided for this image

How did I get these formulas?

And why did I only use these 6 features?

Well, that's from something known as Feature Selection from the sklearn library in Python and specifically using the Feature Importance and Correlation Matrix.


Will upload the detailed explanation along with the Python code snippets in the next article same time next week.

Stay tuned and follow me, Charandeep Kapoor, so that you don't miss out!!!
