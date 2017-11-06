# Deep Reinforcement Learning from Human Preferences

## Abstract

- explore RL systems with (non-expert) human preferences between pairs of trajectory segments;
- run experiments on some RL tasks, namely **Atari** and **MuJoCo**, and show effectiveness of this approach;
- advantages mentioned: 
	- no need to access to the reward function; 
	- less than 1% feedback needed -> reduce the cost of human oversight;
	- can learn complex novel behaviors.

## Introduction

**Challenges**

- goals complex, pooly-defined or hard to specify;
- reward function -> behaviors that optimize reward function without achieving goals;

> This difficulty underlines recent concerns about misalignment between reward values and the objectives of RL systems.

**Alternatives**

- inverse RL: extract a reward function from demonstrations of desired tasks;
- imitation learning: clone the demonstrated behavior;

*con: not applicable to behaviors that are hard to demonstrate for humans*

- use human feedback as a reward function;

*con: require thousands of hours of experience, prohibitively expensive*

**Basic idea**

![approach illustration](https://github.com/txzhao/Paper-Notes/blob/master/RL/fig/approach_scheme.PNG)


**Contributions**

1. solve tasks for which we can only recognize but not demonstrate the desired behaviors;
2. allow non-expert agent training;
3. scale to larger problems;
4. economical with user feedback.

**Related work**

two lines of work: (1) RL from human ratings or rankings; (2) general problemn of RL from preferences rather than absolute reward values.

*close-related paper:*

(1) [Active preference learning-based
reinforcement learning](https://arxiv.org/abs/1208.0984); (2) [Programming by
feedback](http://proceedings.mlr.press/v32/schoenauer14.pdf); (3) [A Bayesian approach for policy learning from
trajectory preference queries](https://papers.nips.cc/paper/4805-a-bayesian-approach-for-policy-learning-from-trajectory-preference-queries).

*diffs with (1)-(2)*: 

a) elicit preferences over whole trajectories rather than short clips; b) change training procedure to cope with nonlinear reward models and modern deep RL.

*diffs with (3)*: 

a) fit reward function by Bayesian inference; b) produce trajectories using MAP estimate of the target policy instead of RL -> involve 'synthetic' human feedback drawn from Bayesian model.

## Preliminaries and Method

**Agent goal**

to produce trajectories which are preferred by the human, while making as few queries as possible to the human.

**Work flow**

at each point maintains two deep NNs - policy *pi*: O -> A; reward estimate *r\_hat*: O x A -> R. 

*Update procedure (asyn):*

1. policy *pi* => env => trajectories *tau* = {*tau^1*,..., *tau^i*}. Then update *pi* by a traditional RL algorithm to maximize the sum of predicted rewards *r\_t* = *r\_hat*(*o\_t*, *a\_t*);
2. select segment pairs *sigma* = (*sigma^1*, *sigma^2*) from *tau*. *sigma* => human comparison => labeled data;
3. update *r\_hat* with labeled data by supervised learning.

> step 1 => trajectory *tau* => step 2 => human comparison => step 3 => parameters for *r\_hat* => step 1 => ....

**Policy optimization (step 1)**

*subtlety:* non-stationary reward function *r\_hat* -> methods robust to changes in reward function.

A2C => Atari, TRPO => MuJoCo.

use parameter settings that work well for traditional RL tasks; only adjust the entropy bonus for TRPO (improve inadequate exploration); normalize rewards to zero mean and constand std. 

**Preference eliciation (step 2)**

clips of trajectory segments for 1 to 2 seconds long.

*data struct:* triples (*sigma^1*, *sigma^2*, *mu*), *mu* - distribution over {1, 2}.

one preferable over the others -> *mu* puts all mass on that choice; equally preferable -> *mu* uniform; incomparable -> skip saving triples.

**Fitting the reward function (step 3)**

*assumption:* human’s probability of preferring a segment *sigma^i* depends exponentially on the value of the latent reward summed over the length of the clip.

![Equation 1](https://github.com/txzhao/Paper-Notes/blob/master/RL/fig/eq1.PNG)

(no discount of reward <- human being indifferent about when things happen in the trajectory segment; could consider discounting.)

![Equation 2](https://github.com/txzhao/Paper-Notes/blob/master/RL/fig/eq2.PNG)

*modifications:*

1. ensemble of predictors -> independently normalize base predictors and then average results;
2. validation set ratio 1/e; employ *l\_2* regularization, and tune regularization coefficient -> validation loss = 1.1~1.5 training loss; dropout in some domains;
3. assume 10% chance that human responds uniformly at random;

**Selecting queries**

*pipeline:* sample trajectory segments of length k -> predict preference by base reward predictor in our ensemble -> select trajectories with the highest variance across ensemble members

*future work:* query based on the expected value of information of query.

*Related articles:* 

1. [APRIL: Active Preference-learning based Reinforcement Learning](https://arxiv.org/abs/1208.0984)
2. [Active reinforcement learning: Observing rewards at a cost](http://www.filmnips.com/wp-content/uploads/2016/11/FILM-NIPS2016_paper_30.pdf)

> At each time-step, the agent chooses both an action and whether to observe the
reward in the next time-step. If the agent chooses to observe the reward, then it
pays the “query cost” c > 0. The agent’s objective is to maximize total reward
minus total query cost.


