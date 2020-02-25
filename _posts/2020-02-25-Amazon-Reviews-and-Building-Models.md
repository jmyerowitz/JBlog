---
layout: post
title: "Amazon Reviews: Learning from mistakes or: I did all this work and still have an inaccurate model?!?"
date: 2020-02-25
---
##### Blog post in process, under construction

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

This is Figure 1, showing the balanced classes that I am trying to predict. Also note that I wanted to use 3000 tokens, but ended up with 1000 tokens. I firmly believe that sticking with 3000 would have led to more accurate models. But alas, you live and you learn.

Below is a quick summary of how I was able to cerate Document-Term-Matrices (DTMs)
 
### Methods

    The basics of natural language processing were employed to create the feature spaces. Preliminary sentiment
    analysis was conducted via both the TextBlob and Vader python packages in an unsupervised way before being 
    compared with the actual y-response (Class/Rating). Feature spaces for machine learning were created via 
    Document-Term Matrices (DTMs) from stemmed tokens of the actual reviews. Tokens were created via the nltk 
    python package with the use of the word_tokenize function and PorterStemmer function. Each word of a review
    was lower-cased (if needed) and stemmed to form a token. CountVectorizer (from sklearn package) created 
    ngrams of length one and extracted the 1000 most frequent tokens.  These 1000 tokens became the features for
    each review in the 100,000-review sample. If a feature token appeared in a review, it was recorded once. As 
    such, the first DTM created was a frequency DTM, which can be seen in Figure 2. The second DTM consists of
    weighting with L2 Regularization, and the third and final DTM weights using L1 Regularization. 

![Image2](https://github.com/jmyerowitz/jmyerowitz.github.io/blob/master/assets/img/Capture1.PNG)

This is a frequency DTM--it counts the amount of times a work (or rather, token) appears in a review. 

You guys want to see some code!?!

    ## Importing nltk dependecies
        from nltk.tokenize import RegexpTokenizer
        from nltk.corpus import stopwords
        from nltk.stem.porter import PorterStemmer
        from nltk import wordpunct_tokenize

    ## Setting up stop words and Porter Stemmer
        en_stop = stopwords.words('english')

        en_stop.extend([".","-","(", ")","/", ",", "’", "”","“", "\n", "'", "!"])

        en_stop.extend([";", ".(", ",(", "?", "?)", "),", ")."])

    ## One last stop word extension
        en_stop.extend(['#', '$', '%', '&', "''", "'d", "'ll", "'m", "'re", "'s", "'the", "'ve", '*', '+', '--', '..', '...', '.i',
                '.it', '.the', '0', '1', '1.', '1/2', '1/4', '10', '100', '11', '12', '13', '14', '15', '16', '17', '18', 
                '1980', '1st', '2', '2-3', '2.', '20', '200', '2000', '2003', '2005', '24', '25', '2nd', '3', '3.', '30', 
                '300', '35', '3d', '3rd', '4', '40', '45', '4th', '5', '50', '500', '6', '60', '7', '70', '8', '80', '9', 
                '90', ':', '<', '=', '>', '@', '[', ']', '`', '``'])

    # Create p_stemmer of class PorterStemmer
        p_stemmer = PorterStemmer()


