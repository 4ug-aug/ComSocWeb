---
title: Data description
prev: "/"
next: network-analysis
---

# Understanding the dataset

Now that we have our raw dataset, let's investigate and clean it based on our findings before moving on with further analysis. 

For readability we briefly present the structure of this section. We start by inspecting our collected data as a whole, examining the number of papers, referenced papers, and potential data issues regarding missing values. From these findings we motivate our choice of data cleaning. We then move on and examine the cleaned dataset grouped by year, to examine the number of papers and references within these. From this we decide on a yearly grouping strategy to introduce the temporal aspect of our further analysis. Lastly we create graph representations of these data groupings and provide an graph analysis on these. 

## Preprocessing
In order to make later analysis using TF-IDF faster, all abstracts in the dataset were preprocessed by adding a tokenised version of the abstract to each paper in the database. The tokenisation is based on the NLTK word_tokenizer, which essentially just splits the document based on white space. We then imported a dictionary of stop words, and defined our own filter on characters to further filter the tokens. This way we got a more indicative list of words used in each abstract.

## Data inspection
Loading and inspecting the data, we found the data has,

- *Number of papers: 315391*

- *Number of referenced papers: 6568377*

- *Number of referenced papers without duplicates: 3233444*

As can be seen from the numbers above, we have a lot more referenced papers than we have main papers in our dataset, even when removing duplicates. This means that many of the papers references other papers that have not been found within our initial search. However, the fact that we have so many duplicates indicates community structure, as multiple papers reference the same papers.

As we need the abstracts for our later analysis, we now examine potential issues with missing values, before moving on to a more in depth data analysis. For this we look up the rows in the data where the abstract is missing. From this we found that
66078 papers were without abstract.

We find that quite a lot of our collected papers have no abstract. Since the abstracts are super important for our analysis we choose to remove them from our dataset. We clean our data from missing values by always querying with,

```javascript
{"abstract": {"$ne": null}}
```

Now that we have cleaned our data from missing values, let's once again take a look at the number of papers and referenced papers. We still have quite a lot of papers, and a lot more referenced papers. Let's dig into this and examine the amount of referenced papers already collected in our main papers list.

We find that only 316.668 or 6.43% of the 4.922.432 references refer to papers that already exist in our dataset. We could choose to make a query for these papers and add them to our dataset, however as they may not be relevant to the main task, and due to the fact that we already have enough data to carry out our analysis, these references are ignored. It is also worth noting that only 30.41% of the papers in the dataset is referenced by one or more other papers present in the graph. This indicates that the graphs that can be constructed from this dataset most likely not going to be very dense.

Now that we have cleaned our data from missing values, we investigate the number of papers and referenced papers within each year. 

![Picture](/images/numberOfPapers.png)

As seen from the plot above, the amount of papers in our cleaned dataset seem to increase slightly from the first year up until around year 2012 whereafter a slight decrease is spotted. We group these years by decades and carry out our analysis with respect to these decades.  As such, we group the papers by four decades: [1990-1999], [2000-2009], [2010-2019] and [2020-present]

![Picture](/images/papersByDecade.png)

It should not come as a surprise that the last decade contains much fewer papers, as it is not finished as of the making of this project. This fact will be kept in mind during the analysis.

Before we start making graph representations for each decade, let's just examine the number of referenced papers in each time window included in the analysis.

![Picture](/images/refInTimeWindow.png)

The plot clearly shows that just a fraction of the papers in each decade are referenced by another paper from the same decade in the dataset.

Since only a small fraction of the papers in each decade are referenced by another paper from the same decade, we would expect to find many small components in the dataset. These components are not of great interest by themselves, but they still provide text that is useful for the TF-IDF analysis.