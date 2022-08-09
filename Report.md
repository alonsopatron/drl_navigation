# Navigation Project Report

This document describes the implementation used in this repository to train an agent to solve Udacity's Navigation project. This is part of the Value-based methods in the Deep Reinforcement Learning course.

## Environment and problem description.

The project uses the **Banana Unity Environment**. This environment consist of a large square space where yellow and blue bananas are placed randomly.

The state space of the environment is 37-dimensional and contains information such as the agent's velocity and ray-based perception of bananas along the agent's forward direction. The agent can perform one of four actions to navigate the space:

  0. Move forward
  1. Move backward
  2. Turn left
  3. Turn right

The task to solve is episodic and consists of training an agent that, given the state of the environment, can choose the right set of actions that allow it to collect the greatest amount of yellow bananas while avoiding blue bananas before the episode ends. The agent is rewarded +1 every time it collects a yellow banana and penalized -1 when it collects a blue banana. The task is considered solved if the agent obtains an average score of at least +13 over 100 consecutive episodes.

## Model

A simple Deep Q-Network was implemented in order to solve this problem. It uses a replay memory that keeps  the last 100K experiences and uniformly samples batches of 64 experiences for learning. A separate fixed Q-Target Network is also kept to improve stability in the optimization.

Each layer in the Q-Network consists of fully connected (FC) linear nodes each followed by ReLU activations (with the exception of the output layer). The input to the network is the 37-dimensional state vector. The first hidden layer has 128 units and the second hidden layer has 64. The output layer has 4 units (one for each possible action).

During training we optimized the MSE loss using the Adam optimizer.

Input (37) -> Linear(128) -> ReLU(128) -> Linear(64) -> ReLU(64) -> Linear(4)

## Training parameters

The following table summarizes the values used for all the hyperparameters during training.

| Hyperparameter | Value | Description |
|---|---|---|
|replay memory size | 100000 | Size of the experience replay buffer |
|minibatch size | 64 | Size of the experience batch sampled from the buffer for optimization |
|target network update frequency | 4 | Frequency (in number of experiences) when a learning step occurs |
|learning rate | 0.0005 | Learning rate used by the Adam optimizer|
|gamma | 0.99 | Reward discount factor |
|tau | 0.001 | Factor used for soft-updates of the target network |
|epsilon start | 1.0 | Starting value for Epison-Greedy action selection |
|epsilon end | 0.01 | Ending value for Epison-Greedy action selection|
|epsilon decay factor | 0.995 | Decay value for Epison-Greedy action selection |
|training episodes | 1000 | Number of episodes used for training |


## Results

After training for 1000 episodes the agent was able to consistently surpass the goal of a +13 score. The agent achieved a score above +13 after **583** episodes. The training progress is illustrated in the figure below.

<img src="/images/training_results.png" alt="drawing" width="400"/>

## Future improvements

In Version 2.0 of this repository will include:

1. Prioritized experience replay to improve learning efficiency.
2. Double Q-Learning to improve potential overestimation of action values.
3. Network architecture exploration.
