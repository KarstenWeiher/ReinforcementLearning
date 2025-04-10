## Learning Project for Reinforcement learning 

In this small Project I use different RL approaches to solve simple games and learn about the underlying mechanisms of RL. 
The first game to solve is Tic Tac Toe and I use 2 approaches: 
- Value Iteration (model based)
- Policy Gradient (model free)

### The Repo contains 3 notebooks 
- ValueIteration. Solves the Tic Tac Toe game with model based Value Iteration. The weights of the model are stored in TTT_model.
- PolicyGradient. Uses Policy Gradient Methods to train a small neural network
- PlayInterface. Implements a tkinter surface to play against the computer model. Currently we can only play against the Value Iteration model

The dependencies are numpy, matplotlib, tkinter on python 3.12.9 

### Sources: 
1. Value iteration was mostly inspired by the lecture series of Steve Brunton https://www.youtube.com/watch?v=sJIFUTITfBc
2. The Policy Gradient Method is based on the blog post from Andrej Kapathy https://karpathy.github.io/2016/05/31/rl/
3. Some general information was derived from https://arxiv.org/abs/2204.04198

### Plans for further development are
- host a small webpage, where one can play against the models
- Implement more interesting games
- Implement Q-Learning methods

### Results and Discussion: 
<p align="center">
  <img src="images\tictactoe.png" alt="Diagramm" width="20%" />
</p>
Tic Tac Toe is a simple game, which makes it a good starting point to learn reinforcement learning. 
To evaluate the models I use a metric based on playing against an opponent that makes random moves. 
In the evaluation the model will always start the game.  

<p align="center">
  <img src="images\score.png" alt="Diagramm" width="25%" />
</p> 

This metric can be between -1 and 1. 
If the model makes random moves the score will be around 0.3.  
The board state is encoded as a length 9 array with 0 for empty fields, 1 for the first player with token x and 2 for the second player with token o.

### Value Iteration
I will not go into detail about the mathematical background of Value Iteration (VI), please view the sources for more information. 
The VI model uses a big look up table to store the value of being in a particular state based on the estimated future rewards. 
At the start of the training the value table is initialized with a guess (I choose all zeros).
The model is improved iteratly by playing the game and updating the value function (i.e. value table) at each board state.  
After iterating a sufficient time, the optimal actions can be extracted from the value function, by choosing the action that leads to the next state with the highest value. 
The training contains 100 epochs with 100 games each. 
Each epoch the model score is evaluated.  
<p align="center">
  <img src="images\val.png" alt="Diagramm" width="50%" />
</p> 
The training curve shows that the model reaches a score of close to 1 around episode 40, suggesting that the model has reached optimality. 
Playing against the model with the tkinter application indeed shows, that the model will never lose and exploid every mistake to win.

### Policy Gradient
Here things became more interesting. The policy model is a neural network that takes the current board position as the input and output the a probabilty distribution for taken a certain a field. 
I first started with a linear model, with only one layer, but that model could only go to a score of 0.5 beeing only slightly better than a random model. 
Then I implemented a nonlinear NN with one hidden layer and a relu activation. 
Innitally the two layer model had no biases, as this was the case in the blog post I took as reference [2]. 
Without a bias the nonlinear model was also performing quit weak around 0.5. 
Adding a bias bosted the performance to 0.8.
I assume this is because of the way the board state is encoded.
Increasing the neurons of the hidden layer from 9 to 100 slightly increased the performance from about 0.75 to 0.8. 
<p align="center">
  <img src="images\pg.png" alt="Diagramm" width="50%" />
</p> 
Note that the NN trains longer than the VI model with 2000 games per epoche. 
Interestingly the NN develops a very different behavior than the VI model. 
The VI model doesn't have a preferance on which field it starts, whereas the NN always starts on one field (the middle in most runs)
The strategie of the NN is to then take the edge fields and try to build a diagonal. 
It does not seem to defend against possible winning combinations of the opponent, instead always follows its own strategie. 
The VI model on the other hand will do the optimal strategie, which is to build quandries if possible and to block the opponents combinations. 
I assume, that the NN never learns to block the opponents combinations, because the opponent is randomly moving and rather unlikely to successfully complete a combination. 

Things to try out next: 
- let the NN train against the VI model
- increase exploration during training
- use one hot encoding for the board state. 

