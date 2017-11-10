# Enhanced Experience Replay Generation for Efficient Reinforcement Learning

## Abstract

- *issue:* RL on real systems -> sparse and slow data sampling;
- *solution:* pre-train the agent with the EGAN;
- *performance:* ~20% improvement of training time in the beginning of learning compared to no pre-training; ~5% improvement and smaller variations compared to GAN pre-training.

## Introduction

5G telecom systems -> fufill ultra-low latency, high robustness, quick response to changed capacity needs, and dynamic allocation of functionality.

*Problems:*

1. exploration has an impact on the service quality in real-time service systems;
2. sparse and slow data sampling -> extended training duration.

## Enhanced GAN

**Fomulas**

the training data for RL tasks:

![Equation 1](https://github.com/txzhao/Paper-Notes/blob/master/RL/fig/egan-eq1.PNG)

the generated data:

![Equation 2](https://github.com/txzhao/Paper-Notes/blob/master/RL/fig/egan-eq2.PNG)

the value function for GAN:

![Equation 4](https://github.com/txzhao/Paper-Notes/blob/master/RL/fig/egan-eq4.PNG)

where the regularization term *D\_KL* has the following form:

![Equation 3](https://github.com/txzhao/Paper-Notes/blob/master/RL/fig/egan-eq3.PNG)

**EGAN structure**

![egan](https://github.com/txzhao/Paper-Notes/blob/master/RL/fig/egan-struct.PNG)

**Algorithm**

![egan-algo](https://github.com/txzhao/Paper-Notes/blob/master/RL/fig/egan-pseudocode.PNG)

The enhancer is fed with training data *D\_r(s\_t, a)* and *D\_r(s\_{t+1}, r)*, and trained by supervised learning. After GAN generates synthetic data *D\_t(s\_t, a, s\_{t+1}, r)*, the enhancer could enhance the dependency between *D\_t(s\_t, a)* and *D\_t(s\_{t+1}, r)* and update the weights of GAN.

## Results

two lines of experiments on CartPole environment involved with PG agents: 

1. one for comparing the learning curves of agents with no pre-training, GAN pre-training and EGAN pre-training. => Result: EGAN > GAN > no pre-training

2. one for comparing the learning curves of agents with EGAN pre-training for various episodes (500, 2000, 5000). => Result: 5000 > 2000 ~= 500

