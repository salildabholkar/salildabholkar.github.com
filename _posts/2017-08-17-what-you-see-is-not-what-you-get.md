---
layout: post
title: "What You See Is Not What You Get: Experiments in fooling neural nets"
tagline: "What do you see?"
math: true
description: Tricking neural nets into wrongly classify images in stupidly easy
keywords: neural nets, computer vision, inception
---

Image Recognition has penetrated our everyday lives,
from small conveniences such as searching by images and tagging photos
to self driving cars.
But even with all these advances, the neural nets used for these tasks
still remain "naive" and can be easily fooled

What do you see when you see the images below?

<!--more-->

![Panda-like image](/assets/images/FoolNet/panda-shuttle.png "Panda-like image"){: .d-inline-block}
![Panda-like image](/assets/images/FoolNet/panda-soccer.png "Panda-like image"){: .d-inline-block}

A Panda? Congratulations! You are smart!

But neural networks are not as smart as you.
It turns out that even with all that terabytes of training,
we can easily fool them into thinking what we want them to think.
[Inception V3](https://arxiv.org/pdf/1512.00567v3.pdf), one of the most
sophisticated image classifiers (42 layers deep),
**[classified the first image as a space shuttle and the second one as a soccer ball](#results)**

First, let's take a quick look at how neural networks work to understand how we can trick them

### Table of Contents
{:.no_toc}

* Toc
{:toc}

## Neural networks

### Brief overview
<figure markdown="1">
![A basic neural net](/assets/images/FoolNet/neural%20net.png)
<figcaption markdown="1">
A basic neural net [[source]](https://towardsdatascience.com/applied-deep-learning-part-1-artificial-neural-networks-d7834f67a4f6)
</figcaption>
</figure>

A neural network, as the name suggests, is a network of neurons (nodes).
Every node has a weight attached to it. 

The working of a neural net can be summarized as follows:

* Weights of every node are randomly initialized
* Every node takes a weighted sum of its inputs
and passes it (as output) to the next layer after applying an [activation function](https://towardsdatascience.com/activation-functions-and-its-types-which-is-better-a9a5310cc8f)
* The output of the last layer forms our final output
* This output is compared with our expected value in terms of a loss function
* We then tweak the weights of each node in a way that would make our generated output as similar as possible to our actual output
* We continue this process until our error is sufficiently small

### In image classification
For image classification, Neural networks in very simple terms are functions &mdash; functions that take in an image
and output a list of probabilities for each of the classes available.
But since there would be 1000 values given 1000 classes, neural networks combine these values
into one value: the **loss function** as stated above.

The loss function for each image depends on the actual correct output for the image.
So in our case of a panda, the actual probabilities should be y [where y is a list containing probability of each class]
with $$y_{panda} = 1$$ and 0 for all the remaining classes.
Initially, with random weights, suppose the neural network has output probabilities p, then the loss function can be defined as:


$$L = - \sum_i{y_i \log{p_i}}$$


As every other term in y is 0 except $$y_{panda}$$, the value returned by the loss function is
$$−\log{p_{panda}}$$ 

This error is propagated to every node and **its weight is changed** in a way that minimizes this error.
This algorithm is called as the [backpropagation algortihm](http://cs231n.github.io/optimization-2/)
Eventually, after repeating the process with several images, the net begins to learn the weights for accurately classifying images.

## Fooling the net
Now what happens if we:
* Fed our original (panda) image as input
* Took a completely different image (say, a soccer ball) as our target

The neural net would learn weights to recognize a panda as a soccer ball.
But as the net was already probably trained on  thousands of panda images,
the probability of it recognizing a panda as a ball increases only slightly

But what if, we calculated the loss, and instead of modifying the weights we modify 
our original image in a way that minimizes this loss? 
This is the intuition behind fooling a neural net.
As it turns out, doing the above is fairly simple and can be done in a few lines of code:

```python
# how likely is the image of the target class (soccer ball)
# get ids from https://gist.github.com/yrevar/942d3a0ac09ec9e5eb3a
probability_fn = output_layer[0, 805]

# The gradient for the same
gradient_fn = keras.gradients(probability_fn, input_layer)[0]

get_probability_and_gradient = keras.function([input_layer, keras.learning_phase()], [probability_fn, gradient_fn])
probability = 0.0

# until at least 90% confidence:
while probability < 0.90:
    # probablity and gradients
    probability, gradients = get_probability_and_gradient([image, 0]) # 0 for learning mode

    # Move the image towards fooling the model
    image += gradients * 0.3 # learning_rate

```

Eventually the image (panda) would be modified into an image which the selected neural net would believe
to be a soccer ball.
By placing appropriate constraints while modifying the image, the changes can be made completely
invisible to humans.

## Results
![The net thinks it's a space shuttle](/assets/images/FoolNet/panda-shuttle-inception.png "The net thinks it's a space shuttle")
![The net thinks it's a soccer ball](/assets/images/FoolNet/panda-soccer-inception.png "The net thinks it's a soccer ball")

## Implications
* As we are manipulating pixels of the image, it is possible to fool systems even when the image
is printed out on a paper. Thus fooling cameras and other sensors is easily possible.
* If two or more neural nets were trained using the same data, all of these would be fooled by the generated image.

### Security implications
* Bypassing security systems using face detection (door lock, phone lock systems).
* Tricking cheque scanner machines.
* Can be used in black hat seo techniques.
* Tricking self-driving cars into seeing red light as green light.

## Tips to overcome fooling attempts
* Generate adversarial images and add them to your training data, to make your system more resistant.
* Use input transformations. These techniques are an effective defence against both Gray-Box and Black-Box attacks. <sup>[[C. Guo, 2017]](https://arxiv.org/abs/1711.00117)</sup>
* Use distillation as a defence mechanism. <sup>[[N. Papernot, 2017]](https://arxiv.org/abs/1511.04508)</sup>