---
layout: post
title:  "Sentiment Analysis for Sudanese Dialect Arabic"
date:   2018-01-29 13:29:16 +0200
author: Rua Ismail
---

 Now day People are continually posting their experiences, feedback and share their opinions in blogs, review sites and other social media sites like Twitter and Facebook, which leads to generate huge volumes of structured and unstructured data, such data has a very high potential for knowledge discovery, which can lead to critical information for decision making in various domains.
 
   Sentiment analysis is a recent area of research performed to extract opinion and subjective knowledge from online text, formalized this knowledge discovered and analyzed it for a specific use. 
  
 The application of sentiment analysis can be classifying online product reviews, services, events or issues as positive or negative. Sentiment analysis can also be employed to process points of view and opinions of the public for political concerns as a part of a public opinion analysis system. 


# what is sentiment analysis? # 
   Sentiment analysis is a series of methods, techniques and tools for detecting and extracting subjective information from online text. 

   We use it to determine attitude or opinion of a speaker or writer with respect to a certain topic, the attitude could reflect a judgment, opinion or evaluation, how the writer feels at the time of writing or the intended emotional communication.   

We can use several techniques for sentiment analysis tasks such as subjectivity detection, sentiment classification, sentiment lexicon generation ...
#Sentiment analysis applications#
 In the following points, there are some important applications of sentiment analysis: 

    1.Determining critics’ opinions about products by classifying online product reviews. 
    2.In market Research sentiment analysis provides a tool to analyze user reviews that help companies improve their quality of products and services. They can identify which particular product or which product feature is more suitable for particular geographic or demographic region. 
    3.Recommendation Systems, since those systems, should not recommend something that receives negative feedback. 
    4.Opinion Spam Detection refers to activities that try to deliberately mislead readers or automated opinion mining systems by giving undeserving positive, unjust, malicious or false negative opinions to other objects. 
    5.Helps governments to discover any violence at an early stage and to begin to deal with it before it expands. 

why to work with Sudanese Dialect Arabic? we have two reason firstly there are no studies on sentiment analysis for Sudanese Dialect Arabic. Secondly, the its history, culture and heritage related to this language.
  
 what we have done
 
   1. First Sudanese Dialect Arabic corpus. 
   2. First domain specific sentiment lexicon for Sudanese Dialect Arabic.
   3.  we conducted a comparative analysis on the performance of different machine learning algorithms.    
 
# The challenges of Analysis Arabic Text #
Arabic is a challenging language because of the properties it has. This can be explained in the following points:

  1. The root for Arabic words could have multiple forms based on the context such as  ﻛﻼم,ﯾﺘﻜﻠﻢ,ﻛﻠﻤﺎت

  2. Arabic has the property of having the same word spelling but with a different meaning depending on its punctuation.
  
  3. Repeating the letter more than once to intensify the meaning or feeling (informal) such as ﺟﺪاااااااااااااااا, in Modern Standard Arabic (MSA) is written as      ﺟﺪا which means extremely too much. 
  
  4. Negation words that are used to negate the past or present tense verbs, which change the meaning of the verb to exactly the opposite. e.g.ﻟﻢ أﻋﺠﺐ ﺑﮭﺬا اﻟﻜﺘﺎب. “I didn’t like this book.” 
   
  6. Arabic language is highly inflectional language which makes monophonically analysis a very complex and difficult task. 
 
# Our Journey #
## Data collection ##

  We collected data using Twitter API which is a set of subroutines, definitions, protocols, and tools that allow access many features of Twitter.This API allows streaming and filtering tweets using ‘searchTwitter’ method, this method issues a search on twitter based on the supplied search string. The arguments for this method include the search query, the maximum number of tweets to return, users location within a given radius of the given latitude/longitude and languages.

  We searched on Twitter using a specific search query such as ‘@ZainSudan’, ‘@MTNSudan1’, ‘@Sudani_sd’, ‘#telecomservicesinsudan’, ‘# اﻻﻧﺗرﻧت_ﻓﻲ_اﻟﺳودان ’, ‘#ام_ﺗﻲ_ان’, ‘# '.ﻣﻘﺎطﻌﺔ_زﯾن_اﻟﺳودان.

 using python ‘tweepy’ package we collect 4713 tweets written from 2012 to 2017.
## Labelling##  

For labeling the dataset, we made three copies of the data so that they can be label by three individuals. we labeled the tweets into three classes according to sentiments expressed in tweets: positive, negative and objective. 

   We provides our lablers with general guidelines to help them in the process.
 
   •**Positive**: If the tweet has a positive, happy, excited, joyful attitude or if something is mentioned with a positive embodiment. Also, if more than one sentiment is expressed in the tweet but the positive sentiment is more dominant.  
   •**Negative** : If the entire tweet has a negative, sad, displeased attitude or if something is mentioned with a negative embodiment. Also, if more than one sentiment is expressed in the tweet but the negative sentiment is more dominant.  
   •**Objective**: If the creator of tweet expresses no personal opinion in the tweet and merely transmits information.  
          
 Beside this, labellers will be instructed to keep personal biases out of labelling and make no assumptions, i.e. judge the tweet not from any past extra personal information and only from the information provided in the current individual tweet. 

  To ensure the reliability of data we will use Krippendorff’s Alpha-Reliability which is a reliability coefficient developed to measure the agreement among observers, coders, judges or raters. 
        
we used R package ‘irr' and kripp.alpha method. The results indicate that the degree of agreement (alpha = 0.317) between our labelers is fair
           



 We associated a label with each sentence based on the majority vote over the three provided labels for that sentence. If a sentence has at least two  negative label then we label it as negative. If it has at least two annotators choosing the positive label then we
 label it as positive and so for the objective label. In the absence of gold-standard labels, the researchers used this majority-voting labels set as a gold-standard.

 After going through majority-voting we arrived at the following statistics for each class:
            
             positive  Negative objective 
               716      3358         638

Where we notice that the dataset is unbalanced, with much more negative tweets than objective and positive ones.
             
## Features extraction ##
 the processes for creating  features for a machine learning algorithms called feature extraction, we filtered out URL links, @ mentions, redundant letters, non-Arabic letters and spelling mistakes were corrected carefully.

   For normalization processes which are removing similar letters that are used interchangeably by one of them, we used Python regular expression, this method allows checking if a particular string matches a given regular expression. 

  We used ISRI stemmer it is an arabic stemmer from NLTK, for removing morphological affixes from words, However, the ISRI stemmer does not use root dictionary. Also, if a root is not found, ISRI stemmer returned normalized form, rather than returning the original unmodified word. 

 We developed a stopword lexicon, this lexicon contains stopword from Modern Standard Arabic as well from Sudanese Dialect Arabic.
 here is an example from it
                       
                       When متين
                       Okey كويس
                       Now  دحين|هسه|حسه
       
Those stopwords are totally different from standard arabic stopwords or other arabic dialect stopwords like Egyptian. this lexicon contains 626 words.

We have filteration function to remove stopwords from dataset given the lexicon.

## Learning ##
   We used scikit learn [http://scikit-learn.org/stable/](http://scikit-learn.org/stable/) for features extraction to extract tokens from the text to be used for machine learning models. First, we used TfidfVectorizer that creates a matrix filled with token frequency to represent our tweets called document term matrix. this , it calculates term frequency-inverse document frequency value for each word(TF-IDF). Term frequency is a weight representing how often a word occurs in a document, Inverse document frequency is another weight representing how common a word is a cross document. 
  

When creating a model to predict, we have two sets of data, a training set and a testing set. Then we create TfidfVectorizer() object and fit it to the training set. After that create a document term matrix for the training set and testing set.  The testing set contains tokens not included in the training set. Therefore the document term matrix for the testing set does not have features for those tokens that do not overlap between the two datasets. 

 For classification, we used Support Vector Machine, Logistic Regression,
Naive bayes and K-nearest-neighbors.  
 
   When evaluating different hyper-parameters which are parameters whose values are not directly learned within for models, the evaluation metrics no longer report generalization performance because the knowledge about the test set can leak into the model. To solve this problem, yet another part of the dataset can be held out as a so called ‘validation set’ training proceeds on the training set, after which evaluation is done on the validation set, the final evaluation can be done on the test set. By partitioning the available data into three sets, we drastically reduce the number of samples which can be used for learning the model. 

   A solution to this problem is a procedure called cross-validation. A test set should still be held out for final evaluation, but the validation set is no longer needed when doing cross-validation. In the basic approach, called k-fold cross-validation, the training set is split into k smaller sets.
 
  The performance measure reported by k-fold cross-validation is then the average of the values computed in the loop. However, because our dataset is relatively small we perform 3-fold cross-validation.  


This work is under publication, we can't discuss the results right now, in another post i will present some of the results,discussion and sources code.

You guys can reach me through my email if you have questions, suggestions or complaints. I appreciate and encourage feedback. 

# links and references # 
Andariya writer Tagwa Warrag use our research as an example of sudan social media , andariya is a local magazine analysis [http://www.andariya.com/can-depressive-analysis-be-conducted-on-sudani-twitter/](http://www.andariya.com/can-depressive-analysis-be-conducted-on-sudani-twitter/ "Can Depressive Analysis be Conducted on Sudani Twitter?")

  

- B. Liu, “Sentiment Analysis and Opinion Mining,” no. May, pp. 1–108, 2012. 
 
-  B. Pang, L. Lee, and S. Vaithyanathan, “Thumbs up? Sentiment Classification using Machine Learning Techniques,” Proc. ACL-02 Conf. Empir. Methods Nat. Lang. Process. - EMNLP ’02, vol. 10, no. July, pp. 79–86, 2002. 

- A. Go, R. Bhayani, and L. Huang, “Twitter Sentiment Classification using Distant Supervision,”  

- E. Kouloumpis, T. Wilson, and J. Moore, “Twitter Sentiment Analysis : The Good the Bad and the OMG !,” pp. 538–541, 2011. 

- A. Pak and P. Paroubek, “Twitter as a Corpus for Sentiment Analysis and Opinion Mining,” Proc. Seventh Conf. Int. Lang. Resour. Eval., pp. 1320–1326, 2010

- R. M. Duwairi, “Arabic Sentiment Analysis using Supervised Classification,” 1st Int. Work. Soc. Networks Anal. Manag. Secur., no. August, pp. 1–10, 2014. 

- M. Abdul-Mageed, M. Diab, and S. Kübler, “SAMAR: Subjectivity and sentiment analysis for Arabic social media,” Comput. Speech Lang., vol. 28, no. 1, pp. 20–37, 2014. 

- A. Shoukry and A. Rafea, “Sentence-level Arabic sentiment analysis,” Proc. 2012 Int. Conf. Collab. Technol. Syst. CTS 2012, pp. 546–550, 2012. 

- R. M. Duwairi, R. Marji, N. Sha’Ban, and S. Rushaidat, “Sentiment analysis in arabic tweets,” 2014 5th Int. Conf. Inf. Commun. Syst. ICICS 2014, 2014. 

useful online courses 


- https://www.youtube.com/playlist?list=PL4LJlvG_SDpxQAwZYtwfXcQr7kGnl9W93
- https://www.youtube.com/watch?v=qeHZOdmJvFU&list=PLZ9qNFMHZ-A4rycgrgOYma6zxF4BZGGPW











 