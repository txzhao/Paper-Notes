# Deep Reinforcement Learning from Human Preferences

## Abstract

- explore RL systems with (non-expert) human preferences between pairs of trajectory segments;
- run experiments on some RL tasks, namely Atari and MuJoCo, and show effectiveness of this approach;
- advantages mentioned: 
	- no need to access to the reward function; 
	- less than 1% feedback needed -> reduce the cost of human oversight;
	- can learn complex novel behaviors.

## Introduction

**Challenges**

- goals complex, pooly-defined or hard to specify;
- reward function -> behaviors that optimize reward function without achieving goals;

> This difficulty underlines recent concerns about misalignment between reward values and the objectives of RL systems.