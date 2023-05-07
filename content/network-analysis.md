---
title: Network analysis
prev: data-description
next: text-analysis
---

# Initial Graph Aanalysis
Now that we have presented our data, cleaned it we move on and create graph representations for each rolling window. Following this we provide a brief preliminary analysis of the graphs before moving on with the main analysis.

Let's build some graphs! :-) A graph will be constructed for each decade. The nodes will be the papers and the edges are the references between them. We will use the NetworkX library to construct the graphs.

With the graphs constructed we take a quick look at summary statistics for each graph to make sure nothing seems wrong:

|      | Graph 1  | Graph 2  |  Graph 3 |  Graph 4 |
|---|---|---|---|---|
| # nodes | 19427 | 27399 | 31931 | 12881 |
| # edges | 25538 | 43972 | 50658 | 21919 |
| mean degree | 2.63 | 3.21 | 3.17 | 3.40 |
| median degree | 2.0 | 2.0 | 2.0 | 2.0 |
| min degree | 1.00 | 1.00 | 1.00 | 1.00 |
| max degree | 152 | 287 | 151 | 106 |




