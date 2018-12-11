+++ 
draft = false
date = 2018-10-29T18:27:14-06:00
title = "Text Mining the Poetry of World War I"
slug = "wwi-poetry" 
tags = ["R", "tf-idf", "data analysis"]
categories = []
+++

**Text Mining the Poetry of World War I**  


Nov. 11, 2018 marks the 100th year since World War I ended. Soldiers, mostly educated British officers, transformed war poetry through uncompromisingly realistic depictions of life in the trenches. Poets like Siegfried Sassoon, Robert Graves, and Wilfred Owen, for one the first times in history, depicted war in horrific, dark language. An analysis using R's tidy text library shows how they wrote about their experiences.

**Data**  

[The Poetry Foundation](https://www.poetryfoundation.org/) published a list of the war's essential poems by year. This analysis uses 114 of the poems, those of which I could find in JSON format. Each poem also has the year, keywords, period the poem was written in, and its region of origin. Ideally, the corpus used would be much larger to help eliminate outliers, but this should get us a fairly robust body of texts.

**What Words do Poets Use Most?**  

One of the simpler ways to use tidy text is to chart the frequencies words appear in the corpus. Not surprisingly, words like "dead", "night," and "mud" are among the most common. Revealing the more tender side of things, "love" and "day" also are fairly common.

![freq](posts/graphics/word-freq.png)

Taking this simple method one step further is an analysis of bigrams in the corpus. Many text analyses are based on the relationships between words, and those that tend to occur immediately after one another within the same documents. "Song" and "mud" appear the most frequently next to each other, followed by "rendezvous" and "death" and "fire" and march"

![freq](posts/graphics/bigrams.png)

**How do Different Poets Use Words?**  

Let's take a look at three of the most famous WWI poets: Siegfried Sassoon, Isaac Rosenberg, and Wilfred Owen. Sassoon is one of the most prolific of the English war poets, along with Rosenberg and Owen, even though they both died in the trenches. Term Frequency-Inverse Document Frequency, or TF-IDF, is a metric used to identify which words in documents stand out against all others. It points out common words in specific documents that are also rare throughout the whole corpus.

![freq](posts/graphics/tf-idf-poets.png)

The language used in these poet's writings are not as dark as the overall term frequency. "Moses," "Tier", and "Tut" are Rosenberg's, Sassoon's, and Owen's highest TF-IDF words, respectively. Looking at the lower-ranking words tells a different story. Sassoon's poems tell of the condition of the trenchs -- "crammed," "stalls," "cursing," and "slogged". Rosenberg makes refers to the war through classic literature and uses words that at face value are more uplifting than usual war poetry. Owen, like Sassoon, also uses words that are grittier than Rosenbergs -- "grimly," "creep," "yells."