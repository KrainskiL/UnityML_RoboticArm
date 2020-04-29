# Udacity Deep Reinforcement Learning Nanodegree
## Project 2 - Reacher :robot:

It's the second project for the Udacity Deep Reinforcement Learning Nanodegree. The goal is to teach robotic arm to touch revolving spheres. To achieve that [DDPG](https://arxiv.org/abs/1509.02971): Deep Deterministic Policy Gradient is used

![Trained DDPG agents](./img/Arms.gif)

## Environment description

In the environment, a double-jointed arm can move to target locations. A reward of **+0.1** is provided for each step that the agent's hand is in the goal location. Thus, the goal of your agent is to maintain its position at the target location for as many time steps as possible.

The observation space consists of **33** variables corresponding to position, rotation, velocity, and angular velocities of the arm. Each action is a vector with four numbers, corresponding to torque applicable to two joints. Every entry in the action vector should be a number between **-1 and 1**.

For this project **Version 2** of the environment was used: 20 agents are used in training at once. Agents must get an average score of +30 (over 100 consecutive episodes, and over all agents). In particular:

* After each episode, we add up the rewards that each agent received (without discounting), to get a score for each agent. This yields 20 (potentially different) scores. We then take the average of these 20 scores.
* This yields an average score for each episode (where the average is over all 20 agents).

## Installation and usage guide

1. Prepare new Conda environment following guidelines on [Udacity DRL repo](https://github.com/udacity/deep-reinforcement-learning#dependencies) 

:warning: You may encounter PyTorch installation issues on Windows 10. Looks like required version of PyTorch must be installed using conda: `conda install pytorch=0.4.0 -c pytorch` before running `pip install` in Point 3.


2. Download custom Reacher environment (Unity ML-Agents env) prepared by Udacity

Linux: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher_Linux.zip)
Mac OSX: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher.app.zip)
Windows (32-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher_Windows_x86.zip)
Windows (64-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher_Windows_x86_64.zip)

The file needs to placed in the root directory of this repository and unzipped.

Path to the executable has to be provided to `UnityEnvironment` function in `TrainArm.ipynb` 

For example on 64-bit Windows:
```python
env = UnityEnvironment(file_name="./Reacher_Windows_x86_64/Reacher.exe")
```

3. Run the `TrainArm.ipynb` notebook using the `drlnd` kernel to train the DDPG agent.

Once trained, the model's critic and actor weights will be saved in the same directory in the file `actor.pth` and `critic.pth`.

4. You can see how trained agent move in environment by running `Watch_Agent.ipynb` notebook.
