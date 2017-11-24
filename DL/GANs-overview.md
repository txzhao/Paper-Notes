# Generative Adversarial Networks: An Overview

## Abstract

- GAN - derive backprop signals through a **competitive process** invovling a pair of networks;
- Aim: provide an overview of GANs for signal processing community, drawing on familiar analogies and concepts; point to remaining challenges in theory and applications.

## Introduction

- How to achieve: implicitly modelling high-dimensional distributions of data
- generator receives **no direct access to real images** but error signal from discriminator
- discriminator receives both the synthetic samples and samples drawn from the real images
- G: G(z) -> R^|x|, where z \in R^|z| is a sample from latent space, x \in R^|x| is an image
- D: D(x) -> (0, 1). may not be trained in practice until the generator is optimal

![gan-baseline](https://github.com/txzhao/Paper-Notes/blob/master/DL/fig/gan-baseline.PNG)

## Preliminaries

- objective functions J_G(theta_G;theta_D) and J_D(theta_D;theta_G) are **co-dependent** as they are iteratively updated
- difficulty: hard to construct likelihood functions for high-dimensional, real-world image data

