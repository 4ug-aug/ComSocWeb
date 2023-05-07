---
title: Text analysis
prev: network-analysis
---

With the graphs and communities created and analysed, we can move on to analysing the abstracts of each community. We will do this by using the [TF-IDF](https://en.wikipedia.org/wiki/Tf%E2%80%93idf) method to find the most important words in each community. To use this method we need all abstracts needs to be tokenised. The tokenised is based on the NLTK word_tokenizer, which essentially just splits the document based on white space. We can then import a dicitionary of stop words, and define our own filter on characters to further filter the tokens. This way we will get a more indicative list of words used in each abstract. In addition to this, the NLTK english_words corpus is used to filter out words that are not in the english language.

As mentioned, the analysis is based on the Term Frequency - Inverse Document Frequency approach. Let's recall what the TF-IDF means.
Term Frequence Inverse Document Frequency, is a way to quantify words' explained variance across documents. Term Frequency is simply how often a term occurs in a document. It 'explains' the weight of the word in term of a document. Inverse Document Frequency is the logarithm to the number of documents the term occurs in, out of all documents. The TF-IDF is the product of the TF and IDF, and has the following form:

$$w_{i,j} = f_{i,j} \times \operatorname{log}\left(\frac{N}{df_i}\right )$$

where tf is the term frequency of term i in document j, df_i is the number of documents that contain term i, and N is the total number of documents.
The higher the TF the more weight the word has, but if it occurs in all other documents as well, the logarithm will be 0 and the product 0, and the importance of the word for the document is therefore none. Likewise, if the IDF is high and the TF is high, the word explains much of the variance.
Therefore, for our analysis we can construct a function that takes a list of ids and gets all the tokens for the ids, and computes the TF-IDF.

With the TF-IDF computed, we can take a look at the top 3 most important words within each top 3 community for each decade. The results are shown below.

| Decade  | Community | Top term 1  |  Top term 2  |  Top term 3  |
|---------|-----------|-------------|--------------|--------------|
| 1990-99 | 1         | intelligence| systems      | artificial   |
| 1990-99 | 2         | chromosome  | gene         | yac          |
| 1990-99 | 3         | intelligence| children     | students     |
| 2000-09 | 1         | emotional   | intelligence | ei           |
| 2000-09 | 2         | artificial  | systems      | intelligence |
| 2000-09 | 3         | intelligence| cognitive    | iq           |
| 2010-19 | 1         | ai          | intelligence | artificial   |
| 2010-19 | 2         | emotional   | intelligence | ei           |
| 2010-19 | 3         | algorithm   | optimization | abc          |
| 2020-23 | 1         | ai          | intelligence | artificial   |
| 2020-23 | 2         | ai          | data         | intelligence |
| 2020-23 | 3         | covid       | 19           | ai           |

From this we see that there seem to be a clear distinction between what researchers focus on when writing about artificial intelligence. We can pair these results with the wordcloud of the abstracts to get a better understanding of what the researchers are writing about. The wordclouds are shown below.

![wordCloudsForDecades](/images/wordCloudsForDecades.png)

From these wordclouds we see that in the earliest decades there seemed to be a focus on the humane side of AI, mainly seen in the second and third largest communities. Here we see that the second community seems to revolve largely around the biological usage of AI, where the third community focuses on children and students and education. The largest community focuses on the more technical side of AI, with a focus on the mode, agent and system. This community is of interest, as in the next decade we see a new community that seems to focus on the same topics. Community 2 of 2000 focuses on many of the same topics as community 1 of 1990, which could indicate that in 2000 the focus of AI was shifted more towards the social and humanistic side. This is seen in the largest community in 2000 revolving around 'individual', 'relationship', 'emotion' and 'social'. In the third community of 2000 they seem solely focused on the model and testing part of AI.
In 2010 we see a shift towards the communities being more focused on applied AI, and problem solving with words such as 'problem', 'method', 'solution', 'results'. In this decade there does not seem to be a distringuisable community from the previous decades, but rather a mix of some of them. This shows that the field of AI, atleast in terms of the Artifical Intelligence keyword, is always evolving and the perception and focus is changing.

In the last decade of 2020 there seem to be a general focus on the model and system part, like the other decades. For the largest and second largest community, they seem to have honed in on the application and usefulness part of AI where the third largest community is more focused on Healthcare and especially covid-19. This is not surprising, as the covid-19 pandemic has been a large part of the last year, and therefore it is natural that it is a large part of the research as well.