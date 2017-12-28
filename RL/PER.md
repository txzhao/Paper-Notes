# Prioritized Experience Replay

## Abstract

- prior work: uniformly sample a replay memory to get experience transitions
- this paper: develop a framework to replay important transitions more frequently -> learn efficienty
- evaluate: DQN + PER outperform DQN on 41 out of 49 Atari games

## Introduction

**issues with online RL:** (solution: experience replay) 

1. strongly correlated updates that break the i.i.d. assumption
2. rapid forgetting of rare experiences that could be useful later

**key idea:** 

more frequently replay transitions with high expected learning progress, as measured by the magnitude of their temporal-difference (TD) error

**issues with prioritization:**

1. loss of diversity -> alleviate with stochastic prioritization
2. introduce bias -> correct with importance sampling

## Prioritized Replay

**criterion:**

- the amount the RL agent can learn from a transition in its current state (expected learning progress) -> not directly accessible
- proxy: the magnitude of a transition’s TD error ~= how far the value is from its next-step bootstrap estimate

**stochastic sampling:**

![](https://github.com/txzhao/Paper-Notes/blob/master/RL/fig/PER-eq1.PNG)

*p_i* > 0: priority of transition *i*; 0 <= *alpha* <= 1 determines how much prioritization is used.

*two variants:*

1. proportional prioritization: *p_i* = abs(TD\_error\_i) + epsilon (small positive constant to avoid zero prob)
2. rank-based prioritization: *p_i* = 1/rank(*i*); **more robust as it is insensitive to outliers**

![](https://github.com/txzhao/Paper-Notes/blob/master/RL/fig/DDQN_PER.PNG)

