# Report for Reacher

## State and action space, rewards in environment

In the environment, a double-jointed arm can move to target locations. A reward of **+0.1** is provided for each step that the agent's hand is in the goal location. Thus, the goal of your agent is to maintain its position at the target location for as many time steps as possible.

The observation space consists of **33** variables corresponding to position, rotation, velocity, and angular velocities of the arm. Each action is a vector with four numbers, corresponding to torque applicable to two joints. Every entry in the action vector should be a number between **-1 and 1**.

For this project **Version 2** of the environment was used: 20 agents are used in training at once. Agents must get an average score of +30 (over 100 consecutive episodes, and over all agents). In particular:

* After each episode, we add up the rewards that each agent received (without discounting), to get a score for each agent. This yields 20 (potentially different) scores. We then take the average of these 20 scores.
* This yields an average score for each episode (where the average is over all 20 agents).

## Learning algorithm

The agents training is conducted using `ddpg` function in the `TrainArm.ipynb` notebook. Agents are trained episodically until `n_episodes` is reached or until the environment is solved. Each episode continues until `max_t` time-steps is reached or until the environment is done.

Agent class is contained in `ddpg_agent.py` file and neural networks for actor and critic defined in `model.py` file.

Additionaly Agent used following mechanisms:
* Replay buffer of experiences
* Soft targets with specified "softness"
* Discounted rewards
* Noise generation with Ornstein-Uhlenbeck process
* Critic's weights decay

DDPG Agent Hyper Parameters:
- BUFFER_SIZE (int): replay buffer size
- BATCH_SIZE (int): mini batch size
- GAMMA (float): discount factor
- TAU (float): for soft update of target parameters
- LR_ACTOR (float): learning rate for Actor
- LR_CRITIC (float): learning rate for Critic
- WEIGHT_DECAY (float): weight decay for Critic's optimizer

Additionally, `theta=0.15` and `sigma=0.2` are set fixed for Ornstein-Uhlenbeck process.

`BUFFER_SIZE = int(1e5)`, `BATCH_SIZE = 128`, `GAMMA = 0.999`, `TAU = 0.001`, `LR_ACTOR = 0.0001`, `LR_CRITIC = 0.0001` and `WEIGHT_DECAY = 10e-7`  

Used hyperparameters values were found by trial and error until satisfactory results were reached. High `WEIGHT_DECAY` values were detrimental to algorithm performance, on the other hand no weight decay also produced poor results.

### DDPG Hyper Parameters  

- n_episodes (int): maximum number of training episodes
- max_t (int): maximum number of timesteps per episode

Where
`n_episodes=1000` and `max_t=1000`

Used hyperparameters values were found by trial and error until satisfactory results were reached.  For `max_t` < 1000 algorithm was performing poorly and in few cases didn't converge at all and was stopped during execution.

### Neural Networks
In the DDPG algorithm two deep neural networks are used and are characterised by following architectures:
- Actor    
    - Hidden 1: (33, 300)   - ReLU
    - Hidden 2: (300, 200)  - ReLU
    - Output: (200, 4)      - TanH

- Critic
    - Hidden 1: (33, 300)   - ReLU
    - Hidden 2: (304, 200)  - ReLU
    - Output: (200, 1)      - Linear


Used architecture is the same as in [`ddpg-pendulum/DDPG.ipynb`](https://github.com/udacity/deep-reinforcement-learning/blob/master/ddpg-pendulum/DDPG.ipynb) except for number of neurons in both hidden layers of critic and actor.

## Plot of average score

![Score](./img/Scores.png)

```
Episode 99	Average Score: 30.07	Score: 37.12
Environment solved in 99 episodes!	Average Score: 30.07
```

## Ideas for improvement

Further improvements may include more hyperparameter tuning or implementing other algorithms suitable for continous action space e.g. [PPO](https://arxiv.org/pdf/1707.06347.pdf) or [D4PG](https://openreview.net/pdf?id=SyZipzbCb)


