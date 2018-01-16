---
layout: post
title: Anonymous Question -- pretrained model zoos for transfer learning
---

For posts titled "Anonymous Question", I'll be answering questions I receive through the group and posting my responses as writeups on the site in case other people might find them useful.  They'll always be anonymized, unless someone requests to be recognized.  Hope you all find this useful!

### Question
_Hey Jason - I went to one of your previous meetups for AI where you talked about a site that is a repository of pretrained models available for download. What site was that?_

### Answer

Like many great features of the Internet, there is no single, centralized repository of pretrained models (yet).  Most of what I'll say is regarding convolutional networks for images.  The same principles of transfer learning apply to other models too, but pretrained image models seem to be hosted online far more often than other kinds of models.

Most of the major frameworks have their own pretrained model zoos bundled in.  The best of these are for PyTorch and TensorFlow, although the one from Keras isn't bad either if you prefer that.  You can find these in the official Github repos/documentation sites for most of the frameworks, and Google will help you find those.  One caveat though, those zoos are not frequently updated with state-of-the-art models, so their performance is somewhat stale (usually on the order of a year or two of lag time).

However, many researchers post their own models they've trained to Github, and some of these are much closer to state-of-the-art performance.  If you find a paper that shows good performance, you can sometimes find the author's Github repo with the code for their experiments.  Even if the author hasn't published their code, chances are somebody has tried to reproduce it and put that code on Github.  Often, there are a few different implementations in each framework, although this varies widely with the popularity of the model.

For PyTorch, the official model zoo packaged in the [torchvision](https://github.com/pytorch/vision) is pretty great.  An unofficial but similarly strong repo for pretrained models is [pytorch-classification](https://github.com/bearpaw/pytorch-classification).  This repo has quite a few models pretrained on Imagenet and CIFAR, and a few of them are pretty strong.  For an example of a more state of the art model that's been pretrained, look [here](https://github.com/hujie-frank/SENet) -- this model won ILSVRC 2017.  It's implemented by the authors in Caffe, although there are third party implementations around (including this one in [PyTorch](https://github.com/moskomule/senet.pytorch)).  In general, these third party implementations do not always match the original performance, so make sure you note their results when they're available.

Generally speaking, which repo/pretrained model you choose will first be constrained by whatever framework you plan on using in your code.  However, there is some flexibility here with tools like [ONNX](https://github.com/onnx/onnx) for those frameworks that participate.  There are other open source tools that are similar, although their efficacy varies widely.  A quick Google search of "converting model from X framework to model in Y framework" should let you know if it's possible.

A final warning: pretrained models can be susceptible to backdoors implemented by hackers.  This attack has been called "BadNets" and was revealed in a [paper](https://arxiv.org/abs/1708.06733) published this past December at NIPS 2017 and presented at the ML for Computer Security workshop.  With this attack, a model can be trained to have state-of-the-art performance on regular images, but also trained to recognize slightly "poisoned" examples (e.g. with a single pixel brightened in the bottom right corner of the image, or a similarly distinct pattern).  This poisoning can be used to influence the model's classification behavior on poisoned images, potentially resulting in dangerous outcomes.  The only way to tell if a pretrained model has been trained cleanly is if whoever's hosting the model provides MD5 or SHA1 checksum keys with the files.  This isn't foolproof, as whoever is hosting will have to update these checksum keys everytime they update the model (which could result in false alarms).  And even if the checksums are up to date, you still have to trust whoever trained and hosted the model to begin with.

If you're model isn't being deployed in a high stakes application, this may not be a huge deal.  That's up to your stakeholders' discretion though, and it's definitely good to know about for all of us trying to apply these methods in practice.

If you have questions more specific to your use case, please do let me know, and I'll help however I can.  Good luck!

Jason
