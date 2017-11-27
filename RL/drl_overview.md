# Deep Reinforcement Learning: An Overview

## Core Elements

### Value Function

#### DQN

*pseudo code:*

![pseudo-dqn](https://github.com/txzhao/Paper-Notes/blob/master/RL/fig/pseudo-dqn.PNG)

*contributions:*

- experience replay and target network -> stablize value function training
- end-to-end RL approach, minimal domain knowledge required
- same algorithm, network and hyper-parameters perform well on many different tasks -> good generalization

#### double DQN

*changes from DQN:* evaluate greedy policy by online network, but estimate value by target network

|**DQN**|![dqn-greedy-policy-1](https://github.com/txzhao/Paper-Notes/blob/master/RL/fig/dqn-greedy-policy-1.PNG) <=> ![dqn-greedy-policy-2](https://github.com/txzhao/Paper-Notes/blob/master/RL/fig/dqn-greedy-policy-2.PNG)|
|:------:|:------:|
|**D-DQN**|![ddqn-greedy-policy](https://github.com/txzhao/Paper-Notes/blob/master/RL/fig/ddqn-greedy-policy.PNG)|





