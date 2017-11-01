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