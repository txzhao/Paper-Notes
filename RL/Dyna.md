# Dyna, an Integrated Architecture for Learning, Planning, and Reacting

## Introduction to Dyna

#### Diagram
![dyna diagram](https://github.com/txzhao/Paper-Notes/blob/master/RL/fig/dyna-diagram.png)

#### Generic algorithm

- step 1-3: standard reinforcement learning agent
- step 4: learning of domain knowledge - action model
- step 5: RL from hypothetical, model-generated experiences - planning

![dyna pseudo code](https://github.com/txzhao/Paper-Notes/blob/master/RL/fig/dyna-algorithm.png)

#### Main idea

planning is 'trying things in your head' using an internal model of the world

#### Action model

input: state, action; output: immediate resulting state and reward

search control: how to select hypothetical state and action

## Potential problems

1. reliance on supervised learning
2. hierarchical planning
3. ambiguous and hidden state
4. ensuring variety in action
5. taskability
6. incorporation of prior knowledge
