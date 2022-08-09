# Navigation example using a Deep Q-Network (Version 1.0)

This repository contains a solution to the Navigation project
from the Deep Reinforcement Learning Udacity course.

## Project description

The project involves the implementation and training of an agent to "solve" a Unity ML environment.
The environment consists of a square world with yellow and blue bananas (see image below). The agent must learn to collect as many yellow bananas as possible.
The agent gets a reward of +1 for each yellow banana collected and -1 for a blue one.

The environment is considered solved if the agent gets an average score of +13 or more over 100 consecutive episodes.

![Unity Environment](/images/environment.png "Banana Unity Environment")

## Running the code

In this section we describe how to run the code to train and test an agent. Before attempting to run any script/notebook please make sure all dependencies are installed.

Before installing dependencies first download the repo:

```
git clone https://github.com/alonsopatron/drl_navigation.git
```

### Installing dependencies

The first thing to set up is a working Python environment. Here we assumed Anaconda3 is already installed in your system. If not this can be installed with **apt** in linux or with **brew** in Mac.

1. Set up your Python Environment

  ```
  conda create --name dqnav python=3.7
  conda activate dqnav    # use [conda deactivate] to get out of the environment
  ```

2. Unzip the Unity environment included in the environment/ folder

3. With the conda environment active, install the Python dependencies. The dependencies folder in this repo was taken from the original course example repository and a few modifications were made to update/remove some dependencies.

  ```
  cd drl_navigation/dependencies/
  pip install .
```

4. Add the conda environment to the Jupyter kernel list so that we can use it when opening a notebook.

  ```
  python -m ipykernel install --user --name dqnav --display-name "dqnav"
  ```

You are all setup for running the code! Just remember to select the **dqnav** kernel when running the Jupyter notebooks as shown below.

![Jupyter Kernel](/images/jupyter.png "Jupyter Kernel")

### Training the agent

Training of a new agent is done by running the **NavigationTrain** Jupyter notebook. By default this will save the trained model to a checkpoint.pth file. Please feel free to modify any parameters in the training function (e.g. the number of episodes to use).

### Testing the agent

Testing of a trained agent is done by running the **NavigationTest** Jupyter notebook. By default this will load a pre-trained model that is included in this repo (pre_trained_model.pth). Please modify the filename if you would like to test one of your trained agents.
