# Deep Reinforcement Learning: An Overview

## Core Elements

### Value Function

#### DQN - baseline

*pseudo code:*

![pseudo-dqn](https://github.com/txzhao/Paper-Notes/blob/master/RL/fig/pseudo-dqn.PNG)

*contributions:*

- **experience replay** and **target network** -> stablize value function training
- end-to-end RL approach, minimal domain knowledge required
- same algorithm, network and hyper-parameters perform well on many different tasks -> good generalization

#### Double DQN

*changes from DQN:* 
evaluate greedy policy by **online network**, but estimate value by **target network**; mitigate the problem of over-optimistic value estimates.

|**DQN**|![dqn-greedy-policy-1](https://github.com/txzhao/Paper-Notes/blob/master/RL/fig/dqn-greedy-policy-1.PNG) <=> ![dqn-greedy-policy-2](https://github.com/txzhao/Paper-Notes/blob/master/RL/fig/dqn-greedy-policy-2.PNG)|
|:------:|:------:|
|**D-DQN**|![ddqn-greedy-policy](https://github.com/txzhao/Paper-Notes/blob/master/RL/fig/ddqn-greedy-policy.PNG)|

#### Prioitized Experience Replay

*changes from DQN:* 

- uniformly-sampled experience replay -> priotized experience replay; 
- importance of experience transitions is measured by TD errors; 
- use importance sampling to avoid bias in update distribution.

#### Dueling Architecture

*changes from DQN:* 
estimate **state value function** V(s) and **associated advantage function** A(s, a) separately, and then combine them to estimate **action value function** Q(s, a)

![duel-arch](https://github.com/txzhao/Paper-Notes/blob/master/RL/fig/duel-arch.PNG)

*combination relations:*

![duel-arch](https://github.com/txzhao/Paper-Notes/blob/master/RL/fig/combine-1.PNG)

for better stability:

![duel-arch](https://github.com/txzhao/Paper-Notes/blob/master/RL/fig/combine-2.PNG)
