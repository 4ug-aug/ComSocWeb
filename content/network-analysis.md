---
title: Network analysis
prev: data-description
next: text-analysis
---

# Initial Graph Analysis
Now that we have presented our data, cleaned it we move on and create graph representations for each rolling window. Following this we provide a brief preliminary analysis of the graphs before moving on with the main analysis.

Let's build some graphs! :-) The graphs are constructed for each decade, defined as a 10 year interval. The nodes are the papers and the edges are the references between them. Only the papers and referenced papers that are in the decade are included in the graph. The grapsh are constructed using the NetworkX library.

After constructing the graphs we take a quick look at summary statistics for each graph to make sure nothing seems wrong:

|      | Graph 1  | Graph 2  |  Graph 3 |  Graph 4 |
|---|---|---|---|---|
| # nodes | 19427 | 27399 | 31931 | 12881 |
| # edges | 25538 | 43972 | 50658 | 21919 |
| mean degree | 2.63 | 3.21 | 3.17 | 3.40 |
| median degree | 2.0 | 2.0 | 2.0 | 2.0 |
| min degree | 1.00 | 1.00 | 1.00 | 1.00 |
| max degree | 152 | 287 | 151 | 106 |

From above summary statistics we see that the general trend is an increase in nodes and edges over each decade - expect for the last decade. This is due to the fact that the last 'decade' only spans 3 years, 2020 - 2023, where 2023 also has yet to finish. If we scale by the amount of years in each decade we get the following:

|      | Graph 1  | Graph 2  |  Graph 3 |  Graph 4 |
|---|---|---|---|---|
| mean nodes | 1942.7 | 2739.9 | 3193.1 | 4293.7 |
| mean edges | 2553.8 | 4397.2 | 5065.8 | 7306.3 |

We see that the mean number of nodes and edges is increasing over time, which is what is expected from the trend.

The mean and median degree seems to be pretty stationary across the years, which is interesting as it suggests that the topic of artificial intelligence is becoming more and more fractured. As more papers are released it does not seem to be all about the same topic, otherwise we would see that the degree would increase as well.

As a last investigation before moving on to the main analysis we plot the degree distribution of the four graphs.

![Degree distribution](/images/degreeDistributions.png)

We find that the structure of all the networks seem to follow the power law with most nodes having a small degree and a rapidly decreasing amount of nodes having larger degrees. This very well matches the summary statistics above, and despite having more nodes in the first 3 full decades resulting in a higher range on the y-axis, the distributions look quite similar throughout the decades.

<!-- # Main Graph Analysis -->
Now that we have gathered our dataset, cleaned and preprocessed it, and made graph representations for each decade, we move on with the actual analysis. 
Let's recall our goal of this project; to investigate how the field of AI evolves over time. For this we start by investigating both the modularity of the louvain split as well as the temporal evolvement in relative size of the largest communities from this partitioning throughout the decades.

For this we start by extracting the largest connected component of each decade graph. From this we split the giant components based on the louvain partition, compute the modularity and extract the three largest communities. The results are shown in the table below:

|      | Community 1  | Community 2  |  Community 3 |
|---|---|---|---|---|
| Graph 1 | 969 (0.05%) | 751 (0.04%) | 555 (0.03%) |
| Graph 2 | 1461 (0.05%) | 1050 (0.04%) | 998 (0.04%) |
| Graph 3 | 2069 (0.06%) | 1537 (0.05%) | 1471 (0.05%) |
| Graph 4 | 959 (0.07%) | 872 (0.07%) | 817 (0.06%) |

The percentage in the paranthesis is the size of the community compared to all the nodes in the decades graph. The relative size of each community within each decade can also be seen in the following figure:

![Community sizes](/images/relativeSizeOfCommunities.png)

We see **not** surprisingly that the community with the least amount of nodes, for the timeframe 2020-2023 has the highest relative size. This is due to the fact that the timeframe only spans 3 years, and the community sizes are computed as the amount of nodes in the community divided by the total amount of nodes in the graph. Although, this could indicate that the papers writting in the period of 2020-2023 are more community based than the papers written in the other decades, we can check to see if this stands true by looking at the modularity of the louvain split for each decade. The results are shown in the table below:

|      | Largest Connected Component  | Modularity  |
|---|---|---|
| Graph 1 | 10450 | 0.88 |
| Graph 2 | 18000 | 0.89 |
| Graph 3 | 23813 | 0.89 |
| Graph 4 | 10947 | 0.79 |

Here we see that the graph for 2020-2024 actually has the lowest modularity, which means it is less dense than the other graphs. Although, this could just be the result of a shorter time period, and we would most likely expect the modularity to land at around 0.89, if we were to include the next 7 years.

Let's visualize the giant components for each of the four 'decades' to better see whats going on. For each century we provide two plots; one where all communities found by the louvain split have been colored, and tone where only the three largest communities found by the louvain split are marked by color. In the code we have only run the analysis for the case where we set the color/group attribute of the nodes for all communities,  but to change this one should simply change the argument "only_paint_top_3 "in "mini_graphalyzer" to be true. 

<div style="display:flex">
  <figure style="margin:0">
    <img src="/images/1990_1999.png" style="width:85%">
    <figcaption style="text-align:center">1990-1999</figcaption>
  </figure>
  <figure style="margin:0">
    <img src="/images/1990_1999_top3.png" style="width:250%">
    <figcaption style="text-align:center">1990-1999 Largest 3 Communities</figcaption>
  </figure>
</div>

<div style="display:flex">
  <figure style="margin:0">
    <img src="/images/2000_2009.png" style="width:90%">
    <figcaption style="text-align:center">2000-2009</figcaption>
  </figure>
  <figure style="margin:0">
    <img src="/images/2000_2009_top3.png" style="width:180%">
    <figcaption style="text-align:center">2000-2009 Largest 3 Communities</figcaption>
  </figure>
</div>

<div style="display:flex">
  <figure style="margin:0">
    <img src="/images/2010_2019.png" style="width:100%">
    <figcaption style="text-align:center">2010-2019</figcaption>
  </figure>
  <figure style="margin:0">
    <img src="/images/2010_2019_top3.png" style="width:100%">
    <figcaption style="text-align:center">2010-2019 Largest 3 Communities</figcaption>
  </figure>
</div>

<div style="display:flex">
  <figure style="margin:0">
    <img src="/images/2020_present.png" style="width:100%">
    <figcaption style="text-align:center">2020-present</figcaption>
  </figure>
  <figure style="margin:0">
    <img src="/images/2020_present_top3.png" style="width:95%">
    <figcaption style="text-align:center">2020-present Largest 3 Communities</figcaption>
  </figure>
</div>


om the plots above, we clearly see the community structure as found by the louvain algorithm fitting well together with the high modularity we found. 

As a last thing before we move on to the text analysis, we investigate how the average citation count within the largest 3 communities compares to the average citation count of the entire giant component of their corresponding decade. With this we hope to verify that using the size of the community for choosing relevant communities makes sense.

|     | Average Citation Count  | Average Citation Count in Largest Community  | Average Citation Count in Second Largest Community  | Average Citation Count in Third Largest Community  |
|---|---|---|---|---|
| Graph 1 | 107.31 | 201.79 | 74.38 | 140.66 |
| Graph 2 | 88.66 | 118.83 | 140.37 | 57.21 |
| Graph 3 | 53.33 | 47.00 | 43.28 | 30.92 |
| Graph 4 | 16.71 | 15.93 | 21.95 | 12.00 |

We find that the average citation count within the communities match fine with the average citation count within the entire component, even exceeding it in most cases. With this we believe that the choice of using size for choosing communities will work fine in terms of choosing relevant communities.