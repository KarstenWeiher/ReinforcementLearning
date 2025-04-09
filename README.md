### Learning Project for Reinforcement learning. 

In this small Project I use different RL approaches to solve simple games and learn about the underlying mechanisms of RL. 
For a starter the game that gets solved is Tic Tac Toe and I use 2 approaches: 
- Value Iteration (model based)
- Policy Gradient (model free)

The Repo contains 3 notebooks: 
- ValueIteration. Solves the Tic Tac Toe game with model based Value Iteration. The weights of the model are stored in TTT_model.
- PolicyGradient. Uses Policy Gradient Methods to train a small neural network
- PlayInterface. Implements a tkinter surface to play against the computer model. Currently we can only play against the Value Iteration model

The dependencies are numpy, matplotlib, tkinter on python 3.12.9 

Sources: 
- Value iteration was mostly inspired by the lecture series of Steve Brunton https://www.youtube.com/watch?v=sJIFUTITfBc
- The Policy Gradient Method is based on the blog post from Andrej Kapathy https://karpathy.github.io/2016/05/31/rl/
- Some general information was derived from https://arxiv.org/abs/2204.04198

Plans for further development are: 
- host a small webpage, were one can play against the models
- Implement more interesting games
- Implement Q Learning methods

