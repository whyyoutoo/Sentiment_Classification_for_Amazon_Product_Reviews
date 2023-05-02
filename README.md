# Sentiment_Classification_for_Amazon_Product_Reviews
**Authors**: Wesley Yu

| ![header_image](./images/header.jpg) | 
|:--:| 
| Photo by <a href="https://unsplash.com/@thetrafficcompany?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Maurice Lourens</a> on <a href="https://unsplash.com/photos/5jAxu-x08Qo?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a> |


## Overview
Topic modeling and sentiment analysis can help businesses better understand their customers' feedback on products. By analyzing large sets of product reviews, we can identify the key topics that customers are talking about and determine the sentiment of each comment. This information can be used to improve product design, marketing campaigns, and customer service. 

Trained on over 100,000 product reviews of around 400 different heaphones listed on Amazon, my final model was able to identify 5 key topics mentioned by customers and was able to predict positive or negative sentiment with an f1 macro score of 85%.


## Business Problem

Good Ears a new audio company is planning to launch their first headphone through Amazon. We are tasked to analyze the headphone market on Amazon to see if any insights can be found to assist the marketing department.

## Data

Data for this project was obtained from Amazon Review Data, made avaliable by [Jianmo Ni et al](https://cseweb.ucsd.edu/~jmcauley/datasets/amazon_v2/) which includes a large-scale collection of customer reviews of products sold on Amazon.

Note: the dataset is too large to be uploaded on github, below is list of datasets to used in these notebooks.

* "Electronics_5.json.gz" [link to download](https://jmcauley.ucsd.edu/data/amazon_v2/categoryFilesSmall/Electronics_5.json.gz)
* "meta_Electronics.json.gz" [link to form](https://forms.gle/UEkkJs69e7Z5A5Ps9)

Dataset contained around 6.7 million reviews of products from the electronics category. For the purpose of this project I have subsetted dataset to include only headphone and earphone products with 200 or more reviews. Resulting in a collection of 189,482 reviews from June, 2000 to October 2018. Each review includes the review text, as well as additional metadata such as the product ID, reviewer ID, rating, and helpfulness votes.

## EDA

Majority of product reviews are 5 star reviews, making up to around 60% of the total reviews.

![image1](/images/star_counts.png)

In order to reduce this problem to a binary classification. I will ultilize NLTK's VADER library, which is designed to provide a sentiment intensity score for a given text, to validate positive sentiment with high ratings and negative sentiment with low ratings. Vader uses a lexicon-based approach, where it matches words and phrases in the text to a pre-defined set of positive and negative words, along with intensifiers and negators. Plot of VADER's compound metric (measuring how strongly positive or negative the sentiment is on the scale of -1 to 1) show that as star ratings increase positive sentiment also increases.

![image2](/images/vader.png)

Negative reviews tend to be slightly longer than positive reviews. This may explain that people are more descriptive when they feel negativley towards a product.

![image3](/images/sentiment.png)

Average word count of reviews is around 90, with median word count at 49. Very few outliers observed with word counts over 4000. Text cleaning will be needed.

![image4](/images/word_count.png)

By examining the most common words we can get a sense of topics that may be most prominent. From the most common unigrams we can infer a couple topics will be about sound quality, comfort of product, and price.

![image5](/images/unigrams.png)

Examining bigram frequency could help us identify common phrases that customers use when describing the product. Important phrases found most common are sound quality, noise cancel, battery life, and customer service.

![image6](/images/bigrams.png)


## Methodology

Due to the massive amounts of reviews avaliable, it is too time consuming to examine each and every data. Topic modeling and sentiment analysis are two powerful techniques used in natural language processing and machine learning to analyze text data and gain insights into customer feedback and preferences.

LDA assumes that each document is a mixture of multiple topics and that each word in the document is associated with a particular topic. The model then attempts to identify the most likely topic distribution for each document and the most likely word distribution for each topic. I will be using Gensim's library to conduct LDA topic modeling.

First I will validate the relationship between star ratings and sentiment with VADER. Then I will proceed to test out different methods of vectorizers and classification algorithms to find the best model that can predict whether a review is positive or negative.

## Results

From examining the keywords from each topic from visualization, I came to the below conclusions for topic labels.

* Topic 1: Design
* Topic 2: Battery / Connectivity
* Topic 3: Sound Quality
* Topic 4: Customer Service
* Topic 5: Comfort




Topic with this most positive sentiment was found to be Sound Quality. The topic with the least positive sentiment is Comfort.

![image](/images/topic_sentiment.png)

## Recommendation

* <b>Focus on customizable comfort</b> - Comfort was found to be the most popular topic disscussed in product reviews, it also contained the highest percent of negative reviews with one of the top negatively associated word found to be uncomfortable. Providing changable earbud plugs or head phone cushions can help improve comfort of product no matter the customer.

* <b>Improve Customer service</b> - The second highest percent of negative reviews was found to be associated with customer service. A few of the top terms associated with the topic were "send replacement", "warranty", "feedback", "update review". Addressing specific issues raised by customers or making broader changes can improve overall satisfaction.

* <b>Adjust Marketing Strategies</b> - Battery / Connectivity was found to have higher negative sentiment compared to design or sound quality. Focusing on marketing products with longer battery life or more stable bluetooth connections can help address customers that feel negatively towards this topic.

## Conclusion

Analyzing product reviews can help get a better sense of the market. Based on my this project we are able to identify meaning full insights of what customers think about certain products. Reviews related to comfort and sound quality make up around 60% of the total reviews in this data. 

Comfort, the topic with the most reviews, also has the highest percent of negative reviews. Which makes sense as people come in all different sizes and shapes, it is very difficult for any one product to fit comfortably on everyone.

Interstingly the second most popular topic, sound quality, has the highest percent of positive reviews. 

Through this project I was able to confirm that products with higher ratings generally have a higher positive sentiment and  products with lower ratings generally have a negative sentiment. 

### Limitations

Due to the nature of Amazon reviews, they are unable to be an exact representation of the overall market:

* Companies may offer discounts or free product for high reviews or there can be a high amount of fake reviews generated by algorithms.

* Only the most vocal will be heard, there are many customers that will like or dislike a product but not leave reviews.

Other limitations deal with my processing of text data.

* Best model was found to be TF-IDF vectorizer with logistic regression, however this method only focuses on term frequency. It is unable to capture semantic relationship between words.

* My text cleaning methods did not address words with typos or nonsensical words, with may lead to increased feature dimensionaltiy during training and effect results.
 
### Next Steps

* Try different methods for topic modeling, such as Top2Vec. LDA works by assuming that each document is generated by a random process involving the selection of topics and words from those topics. Top2Vec, on the other hand, is a neural network-based method that clusters similar documents and identifies representative topics, which can help to better capture semantic relationships between words.

* Make use of recurrent neual network with LSTM for classification. 


## For More Information

Please review our full analysis in [our Jupyter Notebook](/Time_series_analysis.ipynb) or our [presentation]().

For any additional questions, please contact **Wesley Yu at to.wesleyyu@gmail.com**

## Repository Structure

```
├── README.md  
├── Subsetting_data.ipynb 
├── EDA.ipynb
├── Sentiment_Analysis.ipynb
├── Presentation.pdf        
├── data                         <-----Create this folder and download all data                                
└── images                              
```