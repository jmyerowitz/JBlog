---
layout: post
title: "Amazon Reviews: Learning from mistakes or: I did all this work and still have an inaccurate model?!?"
date: 2020-02-25
---

Near the end of our last semester, one of our professors gave us a case analysis and dataset of Amazon reviews. Our tasks were two-fold: Using basic natural language processing, we were to analyze sentiment and cluster The format of this blog post will be a little different—I will be including excerpts from the report that I wrote, followed by comments/frustrations that I had throughout the assignment. 
I wanted to share the imperfect process that is machine learning, and how I learned from my mistakes. This was also my first exposure to a “big” dataset—that is, it’s not data that is so big that it must be run on the cloud, but my local machine had quite a few processing issues. 

Below is a quick description of the problem and an overview of the data:

### Description
    Amazon.com offers hundreds of thousands of products in their vast catalog. Customers of Amazon.com can review 
    purchased products on a 1 to 5-star scale, and they can read reviews left by other customers as a measure of 
    product quality and satisfaction. Such a rating system is subject to a customer’s subjectivity—a 4-star 
    product to one person may be a 5-star product to another, and a customer’s language to describe a product is 
    also subjective. Despite these limitations, we ask ourselves the question: Can a machine learning algorithm 
    accurately predict the star-rating of a review based on the words used in the review itself? Using natural 
    language processing, dimension-reduction techniques, and different machine learning classification algorithms,
    we seek to build an accurate model. 

### Overview of Data
    The data set consists of 3 million Amazon reviews from a span of 18 years. The original data set consists of three
    columns—a star-rating, a short title, and a paragraph (the review). The distribution of the population of Amazon 
    reviews is unknown, but the distribution of the data set is uniform. Due to limitationsof processing power, 
    100,000 reviews were taken and analyzed from the original dataset. Initially, the feature space was to be 
    constructed from 3000 tokens, but processing power limited the tokens to 1000. 
 
![Image1](https://github.com/jmyerowitz/jmyerowitz.github.io/blob/master/assets/img/Capture.PNG)
This is Figure 1, showing the balanced classes that I am trying to predict. 
 
