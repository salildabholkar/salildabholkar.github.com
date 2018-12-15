---
layout: summary
category: summaries
tagline: "Just say it"
description: Edit images just by writing what you want
math: true
keywords: nlp, deep learning, paper summary, image manipulation, GAN, TAGAN,
---

Photos and images are ubiquitous now. Everyone can click and post photos, but modifying them still takes an expert. What if you could just write down the changes you want and voila! There they are. This is the idea explored in the paper, [Text-Adaptive Generative Adversarial Networks: Manipulating Images with Natural Language](https://papers.nips.cc/paper/7290-text-adaptive-generative-adversarial-networks-manipulating-images-with-natural-language.pdf)

### Table of Contents
{:.no_toc}

* Toc
{:toc}


## Pre-paper era

### Common Techniques

* Style transfer techniques can modify a photo to look similar in style to a given photo <sup>[[F. Luan, 2017](https://arxiv.org/pdf/1703.07511.pdf)]</sup>

*  Image modification within specific constraints (edit classes) is possible <sup>[[J.-Y. Zhu, 2016](https://arxiv.org/pdf/1609.03552.pdf)]</sup>

* Automatic construction of similar images (different age, gender, eyes, etc), given an input image is easily possible through adversarial training in pixel space <sup>[[X. Yan, 2016](https://eng.ucmerced.edu/people/jyang44/papers/eccv16_attr2img.pdf)]</sup> or in the latent space <sup>[[G. Lample, 2017](https://arxiv.org/pdf/1706.00409.pdf)]</sup>

* Image generation based on conditional variables has been successfully attempted by many: [Attribute2Image](https://arxiv.org/abs/1512.00570) (using cVAE), [InfoGAN](https://papers.nips.cc/paper/6399-infogan-interpretable-representation-learning-by-information-maximizing-generative-adversarial-nets.pdf) (latent variables), [cGAN](https://arxiv.org/pdf/1411.1784.pdf) (for MNIST)

* There has been some experimentation in the text-to-image synthesis too: 

    * Using a DCGAN to generate natural image from sentence vector <sup>[[S. Reed, 2016](http://proceedings.mlr.press/v48/reed16.pdf)]</sup>

    * [StackGAN](https://arxiv.org/pdf/1612.03242.pdf), for high-res images by stacking up GANs

    * [AttnGAN](http://openaccess.thecvf.com/content_cvpr_2018/papers/Xu_AttnGAN_Fine-Grained_Text_CVPR_2018_paper.pdf), which added attention mechanism to StackGAN

### Limitations

* Although techniques to alter images through natural language exist, they also end up modifying things that weren’t specified in the text (like backgrounds)

* Due to coarse training feedback, GANs tend to generate a new image from the old image and the sentence vector, instead of only modifying the parts specified in the sentence.

## The paper

### Concept in brief

* Proposes a Text-Adaptive Generative Adversarial Network (TAGAN)

* Given an image (x), its description (t), and description of what it should be ($$\hat{t}$$), it learns to generate a modified image $$\hat{y}$$ such that: $$\hat{y} = G(x, \hat{t})$$

#### The Generator

* An encoder-decoder network:

    * Encodes the image into a feature representation

    * Transforms it into a manipulated representation according to the text

    * This manipulated representation is then converted back to an image

* To enforce the generator to only modify the relevant contents, reconstruction loss is used

#### The Discriminator

* Provides feedback for disentangling visual attributes

* Uses word-level local discriminators

* For each word (wi) in the sentence, 

    * Determine whether an attribute related to wi exists using a 1D sigmoid local discriminator fwi by applying weights and bias on a 1D image vector computed by applying global average pooling to the feature map of the image encoder
    $$f_{w_i}(v) = σ(W(w_i) · v + b(w_i))$$

* Softmax is added as a word-level attention to filter out less important words: $$α_i = {exp(u^T w_i) \over \sum_{i}exp(u^T w_i)}$$

* A multiplicative aggregation of scores is done, using multi-scale features: $$D(x, t) = \prod_{i=1}^T[β_{ij}f_{w_{i,j}}(v_j)]^{α_i}$$

### Experiments and Results

* A human evaluation was done on [CUB dataset](http://www.vision.caltech.edu/visipedia/CUB-200-2011.html) and [Oxford-102 dataset](http://www.robots.ox.ac.uk/~vgg/data/flowers/102/)

* Two criteria were used for evaluation (averaged over 50 trials):

    * Parts of the image relevant to the text were modified and irrelevant parts were preserved

    * Naturalness of the modified image 

    * Additionally, L2 reconstruction error by forwarding images with positive texts was also calculated

* Quantitatively and qualitatively, TAGAN performed better over other baseline models such as AttnGAN and [SISGAN](https://arxiv.org/pdf/1707.06873.pdf)

* TAGAN was preferred for its accuracy and naturalness, and obtained a $$p-value < 10^{-30}$$

<figure markdown="1">
![Quantitative results](/assets/images/TAGAN/quantity.png "Quantitative results")
<figcaption>
Quantitative results obtained by TAGAN
</figcaption>
</figure>

* The images produced by TAGAN successfully retained any details that were not mentioned in the text unlike other models:

<figure markdown="1">
![Qualitative results](/assets/images/TAGAN/quality.png "Qualitative results")
<figcaption>
Qualitative results obtained by TAGAN
</figcaption>
</figure>

* In image-text matching tasks, it outperforms the auxiliary matching network in AttnGAN, and is competitive with the state-of-the-art matching methods<sup>[[S. Li, T. Xiao](http://openaccess.thecvf.com/content_ICCV_2017/papers/Li_Identity-Aware_Textual-Visual_Matching_ICCV_2017_paper.pdf)]</sup>.

## Advantages

* Can be trained by the crossentropy loss without the ranking loss due to multiplicative aggregation

* Does not need any hand-tuned hyperparameters

* The text-adaptive discriminator is trained as the core GAN framework

* TAGAN considers the importance of each word at every level of the image vector

* Individual attributes are identified in the sentence and then mapped to the relevant attribute in the image

* Thus, unmentioned changes are perfectly retained from the original image