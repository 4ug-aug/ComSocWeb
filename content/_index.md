---
title: Home Page
layout: single
next: data-description
---

# Motivation 
Artificial intelligence has increasingly become a hot topic throughout the past decades. AI has moved from being an existatntial thread depicted on the silver screen depictions in dystopian science fiction thrillers such as Terminator and the Matrix, to being an intangible buzzword for pitching to investors to finally taking the world by storm with the release of complex AI driven tools such as  DALL-E, Midjourney  and ChatGPT. The graph below illustrates how the frequency of google searches on "Artificial Intelligence" has evolved during the past two decades (source: https://trends.google.com/trends/).

<center>Google Trends: Artificial Intelligence</center>

![Picture](/images/google_trends_AI.png)

From the outside, it seems that the way Artificial Intelligence is being talked about has changed a lot over the past decades, and to many people it may seem that it has not been talked about at all until recently (as suggested by the above figure). Therfore we wanted to examine these changes in a more quantitative manner, using the tools that were introduced in the DTU 02467 Computational Social Science Course.

## [Explainer Notebook](explainer-notebook.html)

# The dataset

The raw dataset collected for this project consists of the paper ID, title, abstract, year, citation count and references for 315.400 papers (645 MB) published between 1990 and 2023, though not all papers collected had information for every field queried. The data was collected by querying "Artificial Intelligence" with keyword search using the Semantic Scholar API, which limited the search depth to the first 10.000 papers. Therefore up to 10.000 papers were collected for each year examined. However, since the search was sorted by relevence, it was assumed that the first 10.000 papers found using keyword search would be sufficient to carry out the target analysis. Overall, it is worth noting that the described datacollection approach is itself a heuristic and the implications thereof in relation to the stated project goal are discussed in the final chapter.

## Motivation behind the dataset
We decided to query the Semantic Scholar API using the term "Artificial Intelligence" rather than terms like "Machine learning" or "Neural Networks" because we were more interested in getting an overview over how AI is talked about in relation to other fields and society as a whole rather than how the technical field of AI has evolved. From our personal experience, it appears that "Artificial Intelligence" is not commonly mentioned in technical papers discussing specific techniques within AI and machine learning, while, on the other hand, the term is commonly used in texts discussing the impact of the technology as a whole instead of its technical implimentations. 
Though this analysis could also have been carried out by examining texts found in many other places, we found a few perceived advantages of focusing on scientific articles. We assumed that scientific articles would be a less "dirty" data source compared to collecting information from a more wide corpus such as by searching on goolge. Thus the resulting analysis might give a more clear image about what topics were being talked about at the time of publishing, as the authors aim to write articles that are relevant at the time of publishing and are more likely to be informed about the general topic of AI. On a similair note, scientific articles are not as opinionated as many other texts found on the internet. We were not interested in finding out how people feel about AI at a given time, but rather in which context the term existed.


## Data Collection
As we expected to partition the same dataset in multiple different ways for our analysis, we found it useful to save all data in a database using MongoDB. In this way, a pandas dataframe could quickly be constructed by querying the database. Thus it was not necessary to store the same data multiple times across different .csv files. Additionally, the database could manage simultanious incomming write requests from parallel processes, which were ID'ed by paper ID, such that no duplicates were made and data integrity was protected by avoiding race conditions.

## Goal of analysis
Artificial intelligence is a phrase that many people have never heard of until recently. We would like to show the end user that it is a topic that has been talked about for decades before the release of tools like ChatGPT. At the same time, we would like to give the end user an overview of how the topic has evolved with time.