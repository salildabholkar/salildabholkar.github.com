---
layout: post
category: projects
title: "SarcDetect: Sarcasm detection with transfer learning"
tagline: "I am not sarcastic!"
description: Using ULMFiT for sarcasm detection yields great results out-of-the box
keywords: nlp, deep learning, sarcasm detection, ulmfit, semeval, transfer learning
---

[ULMFiT]({% post_url 2018-06-10-universal-language-model-fine-tuning %}) is a great technique for applying transfer 
learning in nlp. It has shown to achieve great results with small amounts of data. So, when I came across
the [SemEval2018 task for irony detection](https://competitions.codalab.org/competitions/17468),
I wanted to put it to the test.

### Table of Contents
{:.no_toc}

* Toc
{:toc}

Usually in nlp, we use word embeddings, which are vectors of floats that represent different words.
But in ULMFiT, we use a pretrained language model and fine-tune it for our task.
A language model not only has word embeddings, but has also been trained to get a
representation of full sentences and documents.

## Pre-processing
We clean up the data a little. Remove user-mentions, links and numbers from the tweet.
Also, I separated the hashes to better obtain their co-relation with the tweet
Here is the code I used:

```python
from nltk.tokenize import TweetTokenizer
import re
import wordsegment as ws
ws.load()

def preprocess(tweet):
  tknzr = TweetTokenizer(reduce_len=True, strip_handles=True)
  tokens = tknzr.tokenize(tweet)

  tweet = " ".join(tokens)  # we need to ensure that all the tokens are separated using the space

  tweet = tweet.lower()
  tweet = re.sub(r'http[s]?://(?:[a-z]|[0-9]|[$-_@.&amp;+]|[!*\(\),]|(?:%[0-9a-f][0-9a-f]))+', '', tweet)  # URLs
  tweet = re.sub(r'(?:@[\w_]+)', '', tweet)  # user-mentions
  tweet = re.sub(r'(?:\#+[\w_]+[\w\'_\-]*[\w_]+)', '', tweet)  # hashtags
  tweet = re.sub(r'(?:(?:\d+,?)+(?:\.?\d+)?)', '', tweet)  # numbers

  return tweet

def segmentHashes(tweet):
  tags = " ".join(re.findall(r"#(\w+)", tweet))
  return " ".join(ws.segment(tags)).lower()
  
```

## Preparing the data
Let's get the training, validation and test data into the necessary format.
We split the data 70-30 for validation

```python
from fastai.text import *
from sklearn.model_selection import train_test_split
import wordsegment as ws

path = ''
ws.load()

df = pd.read_csv(path + 'SemEval2018-Task3-master/datasets/train/SemEval2018-T3-train-taskB_emoji_ironyHashtags.txt', delimiter='\t')
df['hashes'] = df.apply(lambda row: segmentHashes(row['Tweet text']), axis=1)
df['Tweet text'] = df.apply(lambda row: preprocess(row['Tweet text']), axis=1)

train_df, valid_df = train_test_split(df, test_size=0.7)

test_df = pd.read_csv(path + 'SemEval2018-Task3-master/datasets/goldtest_TaskB/SemEval2018-T3_gold_test_taskB_emoji.txt', delimiter='\t')
test_df['hashes'] = test_df.apply(lambda row: segmentHashes(row['Tweet text']), axis=1)
test_df['Tweet text'] = test_df.apply(lambda row: preprocess(row['Tweet text']), axis=1)
```

![Data sample](/assets/images/sarcasm/data.png)

## Building our classifier

### Fine-tune the language model
We first get a pre-trained model to use as our base.
Since we are classifying English tweets, the WT103 model (from fastai) works fine for our case.
Fine-tuning it for tweets is as simple as:


```python
# Language model data
data_lm = TextLMDataBunch.from_df(
    path = 'salil',
    train_df = train_df,
    valid_df = valid_df,
    test_df = test_df,
    label_cols = ['Label'],
    text_cols = ['Tweet text', 'hashes']
)
learn = language_model_learner(data_lm, pretrained_model=URLs.WT103_1, drop_mult=0.7, callback_fns=ShowGraph)
learn.fit_one_cycle(1, 1e-2)
```
![Loss graph](/assets/images/sarcasm/loss1.png)

We unfreeze the model and fine-tune it:

```python
learn.unfreeze()
learn.fit_one_cycle(1, 1e-3)
```
![Loss graph](/assets/images/sarcasm/loss2.png)

We can test our language model by having it create some tweets for us:
![Example prediction](/assets/images/sarcasm/predict.png)

### Fine-tune for classification
Now, we fine-tune it for the purpose of classification.
```python
learn = text_classifier_learner(data_clas, drop_mult=0.5)
learn.load_encoder('tweet_enc')
learn.fit_one_cycle(1, 1e-2)
learn.freeze_to(-2)
learn.fit_one_cycle(1, slice(5e-3/2., 5e-3))
learn.unfreeze()
learn.fit_one_cycle(1, slice(2e-3/100, 2e-3))
```
The classifier is tuned and ready to classify. 

## Results
Without much work, we easily got an accuracy of around 85% on the validation set
![Accuracy of 85%](/assets/images/sarcasm/accuracy.png)