---
layout: summary
category: summaries
tagline: "Sharing is caring"
description: ULMFiT allows us to significantly improve performance of deep learning on nlp tasks by leveraging transfer learning
keywords: nlp, deep learning, paper summary, transfer learning
---

In early 2018, [Jeremy Howard](https://www.fast.ai/about/#jeremy) and [Sebastian Ruder](http://ruder.io/) came up with one of the first methods to significantly improve performance of deep learning on nlp tasks by leveraging transfer learning
Their findings were reported in their paper – [Universal Language Model Fine-tuning for Text Classification](https://arxiv.org/abs/1801.06146) (ULMFiT)


### Table of Contents
{:.no_toc}

* Toc
{:toc}


The idea behind transfer learning is simple: <sup>[[Peter Martigny, 2018](https://blog.feedly.com/transfer-learning-in-nlp/)]</sup>

* The hidden layers of models are able to learn general knowledge, which can then be used as one big featurizer

* We can download a pre-trained model and remove the last layer of the network (the fully-connected layer, which projects the features)

* We can then replace it with a classifier of our choice, tailored to our task (say, a binary classifier to classify a sentence as positive or negative)

* Thus, we need to train our classification layer only

* The data we use may be different than the data which was used for pre-training

* So we do a fine-tuning step, where we train all layers for a [much] short amount of time.


## Pre-paper era

### Common Technologies

* Traditional approaches such as one-hot encoding and bag-of-words do not capture information about a word’s meaning or context.

* Word vectors were used as the defacto representation technique in NLP

* [Word2vec](http://papers.nips.cc/paper/5021-distributed-representations-of-words-andphrases) became popular as an approximation to language modeling, followed by others such as [GloVe](https://nlp.stanford.edu/projects/glove/).

* Transfer learning had meanwhile become a common place in other domains such as computer vision <sup>[[ImageNet](http://www.image-net.org/)]</sup>

### Limitations

* Word vectors used previously learned knowledge only in the first layer of the model --- the rest of the network still needed to be trained from scratch.

* As languages can be quite ambiguous, huge amount of labelled data and the capacity to process it was required

* Not the idea of LM fine-tuning but our lack of knowledge of how to train them effectively has been hindering wider adoption.

* LMs overfit to small datasets and suffered catastrophic forgetting when fine-tuned with a classifier.

## The paper

### Concept in brief
The paper proposes using an AWD-LSTM model for transfer learning from a LM [source] task to the classification [target] task in the following manner:

* **pre-train on a general language modeling (LM) task:**

    * Wikitext-103 was used for this purpose <sup>[[Merity et al., 2017b](https://arxiv.org/pdf/1609.07843.pdf)]</sup>

    * Consists of 28,595 preprocessed English Wikipedia articles and 103 million words.

    * Performed only once and improves performance and convergence of downstream models.

* **fine tune the LM on target task:**

    * Allows to train a robust LM even for small datasets.

    * Different learning rates are used for different layers <sup>[discriminatively fine-tuned]</sup>

    * Learning rates are first increased linearly, and then decreased gradually after a cut <sup>[slanted triangular learning rates]</sup>

* **fine tune for text classification:**

    * LM model is gradually unfreezed starting from the last layer

    * variable length backpropagation sequences are used <sup>[[Merity et al., 2017a](https://arxiv.org/abs/1708.02182)]</sup>

    * Classifier is fine-tuned for forward and backward language models and the average is used as final output

### Experiments and Results

* ULMFiT with 100 examples = Training from scratch with upto 20k examples <sup>[IMDb sentiment analysis]</sup>

* Accuracy of ULMFiT with 1000 examples = Accuracy of FastText model from scratch on full dataset <sup>[[Kaggle project](https://www.kaggle.com/bittlingmayer/amazonreviews/home)]</sup>

* combining the predictions of a forward and backwards LM-classifier results in a boost of around 0.5–0.7

* Even regular LM reaches good performance on larger datasets

* ‘Discr’ and ‘Stlr’ improve performance across all three datasets and are necessary on TREC-6

* ULMFiT is the only method that shows excellent performance universally

* performance remains similar or improves until late epochs

ULFiT obtained reductions in error rates over state-of-the-art as follows:

<table>
  <tr>
    <td>IMDb</td>
    <td>DBpedia</td>
    <td>Yelp-bi</td>
    <td>Yelp-full</td>
  </tr>
  <tr>
    <td>22%</td>
    <td>4.8%</td>
    <td>18.2%</td>
    <td>2.0%</td>
  </tr>
</table>

<small>
**Note:** 10% of the training set was used and error rates with unidirectional LMs were reported. The classifier was fine-tuned for 50 epochs
</small>

## After the paper

With the emergence of better language models, we will be able to further improve our model’s performance

The success achieved by ULMFiT has spurred an interest in applying transfer learning to NLP. In just the next few months after the paper, there were several frameworks proposed (especially fine-tuned language models). A few of the popular ones are:

* **Generative Pre-training:** <sup>[[Radford et al., 2018](https://s3-us-west-2.amazonaws.com/openai-assets/research-covers/language-unsupervised/language_understanding_paper.pdf)]</sup>

    * Input is transformed differently while pre-training depending on the task to be performed

    * Uses a Transformer network instead of the LSTM used here

* **Deep contextualized word representations:** <sup>[[Peters et al., 2018](https://arxiv.org/pdf/1802.05365.pdf)]</sup>

    * word embeddings should incorporate word-level characteristics and contextual semantics

    * Instead of just using the final layer, vectors of all internal states are weighted and combined to form the final embeddings
