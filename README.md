# lln - lingo(nlp) loom(models) novitiae(beginning)

Welcome to my repository, featuring all the foundational projects I've completed while learning about NLP and LLMs. 

This readme file is more like a blog, where I mention each of the project links along with what I've learnt from working on the same. 

I've honed my skills by diving into blogs and documentation, and I'll be including those references as well.

Hope this is useful and enjoyable. 

-------------------------------------------------------------------------------------------------------------------------------

### [NLP for analyzing disaster tweets](https://github.com/KamalamSivakumar/lingoloom_novitiae/blob/main/NLP%20with%20Disaster%20tweets.ipynb)

Tried out preprocessing with both NLTK and spaCy libraries.
1.	Preprocessing text to remove unnecessary characters.
2.	Preprocessing text to tokenize, remove stop words and stem/lemmatize.

Used Multinomial NB and a pretrained BERT Model for Text Classification.

For Multinomial NB, used the preprocessed input as TF-IDF vectors and applied Multinomial NB to get the predicitons.

For BERT Model, used the transformers library from huggingface, used the preprocessed input as encoded tensors.

Configured training and classification used “BertForSequenceClassification” which has a linear classification layer, classifying as disaster or not.

Using PyTorch libraries, ran training and validation, to get the predicitons.

Nuances learnt: 
1.	How the batch training and validation sets are configured,
2.	How the hyperparameters (learning rate) can be fine-tuned or scheduled.

[Kaggle reference link](https://www.kaggle.com/competitions/nlp-getting-started)

----------------------------------------------------------------------------------------------------------------------------------------

### [Sentiment Analysis](https://github.com/KamalamSivakumar/lingoloom_novitiae/blob/main/Sentiment%20Analysis.ipynb)

Learnt about the basics of Sentiment Analysis:
1. Components of a review (Opinion, Subject, Entity), sentiments can be classified based on document (entire text), sentence (given sentence) or aspect (which part of sentence, eg a phone review, “the display is good, but the battery strength is poor”)
2. Valence of a sentence (polarity and subjectivity)
3. Rule based and ML based classification
              
Worked on “Sentiment Analysis, classify a review as positive or negative” problem using Rule based and ML based approaches.

Rule based approach: VADER

ML based approach: NB Classifier, Logistic Regression and KNN

Nuances learnt:
1. Text Classification vs Sentiment Analysis:
               While Sentiment Analysis is a Text Classification problem, it aims at understanding the tone of the document being analyzed. With the Disaster Classification problem, I did not aim at finding how the tone of the tweet was, while the Sentiment Analysis problem revolves around finding the tone of the said document.
2. It’s very important to pre-process the text effectively, before applying any type of model to get effective results.
3. As VADER is mainly trained on social media (tweets/comments etc), it did not classify movie_reviews effectively, tried to compute the VADER scores for each sentence in a movie review, with a compound measure that indicates the normalized or aggregated polarity score for that sentence. The result did come out better. 
4. Extracted features that can be used to train the ML models, positive scores and compound scores, the feature extraction can also be extended to most frequent words used in a positive/negative review.

References:

https://github.com/cjhutto/vaderSentiment

https://towardsdatascience.com/a-guide-to-text-classification-and-sentiment-analysis-2ab021796317

----------------------------------------------------------------------------------------------------------------------------------------------------------

### [Aspect Based Analysis](https://github.com/KamalamSivakumar/lingoloom_novitiae/blob/main/ASBA%20using%20spacy%20and%20VADER.ipynb)

Why ASBA?

Often, a business requirement is to understand and analyze customer reviews. When we can comprehend the reviews the “product”, “component” or “aspect” wise, we can make more use of the reviews.

ASBA has 3 steps (in an overview):
1. Extract aspect candidates.
2. Classify the aspect candidates as aspects or non-aspects.
3. Associate a polarity to each extracted aspect.

Performing ASBA with spaCy and VADER:  
With spaCy’s inbuilt language models, it is easier to extract the token’s Part-Of-Speech (POS) tag.

An assumption made: Usually the features of products and services are mostly nouns and compound nouns.

Accordingly, their BOI tags are considered for identifying the “target”/”aspect” and its adjective would be the corresponding “description”/”opinion”.

Once identified, the polarity scores can either be assigned by employing TextBlob/VADER libraries. In case of VADER, the threshold for classifying is considered as follows: pos-> > 0.5 & neg-> <=0.5.

Spaces for improvement: As of now, in regard with the aspect extraction, only the final occurrence of adj is considered. With regards to assigning polarity scores, non-lexical models can be experimented with. 

References:

https://medium.com/nlplanet/quick-intro-to-aspect-based-sentiment-analysis-c8888a09eda7

----------------------------------------------------------------------------------------------------------------------------------------------------------

### [Named Entity Recognition](https://github.com/KamalamSivakumar/lingoloom_novitiae/blob/main/Named%20Entity%20Recognition.ipynb)

Goal of NER: Identifying all textual mentions of the named entities. Involves two aspects namely:
1. Identifying the boundaries of the named entity.
2. Identifying the type of the entity.
     
Chunking/Shallow Parsing/Light Parsing: Inside, Others and Before (IOB Components). 

Used spaCy’s displacy for viewing the dependencies/hierarchies between the chunks. Could be done through nltk as well but couldn't install ghostscripts/standford nlp parser for viewing the hierarchy in the chunks. (admin rights required to install the same)

Tagging: Part of Speech Tagging, that could be done through in-built methods using nltk/spacy or by configuring custom POS tagger using existing methods, for example by defining a regex tagger or by defining an NGramTagger.

Used ClassifierBasedPOSTagger from nltk to build a POS Tagger that learns through a classification model (NaiveBayesClassifier)

Used spaCy’s Named Entity Recognition package and viewed the results. Used spaCy’s displacy to render the results better. 

Learnt to build a NER model by using Conditonal Random Fields (CRF). CRF is used for prediction tasks where contextual information in our case, state of the neighboring words affects the current prediction. Trained using Gradient Descent approach, (MLE) where the parameters are optimized to maximise the probability of the correct output sequence.

Nuances learnt:
1. backoff concept in taggers: backoff is nothing but when any of the words in the input sequence, don't have a corresponding tag, it's assigned None, when with backoff mentioned, the backup tagger method mentioned is used. This improves the performance of the corresponding taggers significantly. 
2. In order to use CRF for NER, the features must be defined. The following features were considered: the word, the last 3 characters, the last 2 characters, its POS tag, if it’s a digit. Additionally, [BOS] (beginning of a sentence) and [EOS] (end of a sentence) were added as well.
3. The crf_suite from scikit-learn is easier to implement with, the desired MLE algorithm can be mentioned, and if we need to consider all possible options in the CRF. The model performed quite well, further improvements could be made by extending the feature engineering and fine tuning the hyperparameters.

References:

Notebooks on NER from [Dipanjan Sarkar](https://github.com/dipanjanS)

-----------------------------------------------------------------------------------------------------------------------------------------------------
