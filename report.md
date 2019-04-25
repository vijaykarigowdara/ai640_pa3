# Programming Assignment 3

CS 640 

Name: Vijay Nagaraj Karigowdara

Team Member: Diptanshu Singh

Date: 25/04/2019

## Problem Definition

Implement minimax or alpha-beta pruning for a tic-tac-toe game AI to break the 4x4x4 game.

To win the game, which position will you mark first as player going first? Are you always going to win as player going first? If not, why?
What are the “node” in our tic-tac-toe game? What are the children of “node” then?
What is the “terminal node” in our tic-tac-toe game?

There are at least two issues related to the decision of heuristic value for each node:
How to make sure your AI always prevent the opponent from winning in the next move if your AI still have a chance to do so by correct values for nodes?
If there is a move for your AI to win in the next move, is your AI able to find out the move also by correct values for nodes?

## Scope

The implementation of minimax search and alpha-beta pruning contribute towards making the game more intelligent. The goal is to create an intelligent game by looking at the future of the board and use a good heuristic. Best possible move for a certain situation is calculated by learning what board states are most beneficial and hence working towards those states. Thus, avoiding using brute-force method makes the game an interesting prospect.

## AI Algorithms
### Minmax 

Minimax is a decision rule used in decision theory, game theory, statistics and philosophy for minimizing the possible loss while maximizing the potential gain. Alternatively, it can also be thought of as maximizing the minimum loss. If the game is over in the given position, then there is nothing to compute; minimax will simply return the score of the board. Otherwise, minimax will go through each possible child, and (by recursively calling itself) evaluate each possible move. Then, the best possible move will be chosen, where best move leads to the most positive score for player ‘A’, and the board with the most negative score for player ‘B’.

psedo-code:
function minimax(player,board)
  if(game over in current board position)
      return winner
    children = all allowed moves for player from this board
  if(max's turn)
    return max score of calling minimax on all the children
  else (min's turn)
    return min score of calling minimax on all the children

        
### Alpha-Beta Pruning

Alpha-Beta pruning is an optimization algorithm of Minmax where we can save a lot of searching and allows us to increase our maximal search depth. Here we will keep track of two numbers, alpha and beta for each node we're analyzing. Alpha will be the value of the best possible move the current player can make. Beta will be the value of the best possible move the opponent can make, that you have computed so far. If at any time, alpha >= beta, then opponent's best move can force a worse position than our best move so far, and so there is no need to further evaluate this move. The same pruning condition applies if you are the min player, except instead of finding the move that yields alpha, we would find the move that yields beta. Initially alpha is negative infinity(the best you can do is lose) and beta is positive infinity(the worst your opponent can do is to let you win). As the recursion progresses the window becomes smaller. When beta becomes less than alpha, it means that the current position cannot be the result of best play by both players and hence need not be explored further and these values are updated as we examine more nodes.

pseudo-code:
function alpha-beta(player, board, alpha, beta)
  if(game over in current board position)
      return winner
  children = all legal moves for player from this board
  if(max's turn)
    for each child
      score = alpha-beta(other player, child, alpha, beta)
      if score > alpha then alpha = score (we have found a better best move)
        if alpha >= beta then return alpha (cut off)
          return alpha (this is our best move)
   else (min's turn)
      for each child
	      score = alpha-beta(other player, child, alpha, beta)
          if score < beta then beta = score (opponent has found a better worse move)
            if alpha >= beta then return beta (cut off)
              return beta (this is the opponent's best move)
              
It is to our advantage to generate the best moves first for max and the worst moves first for min, this will cause the algorithm to cut off more quickly. On average, using a good successor generator will allow alpha-beta to search to a level twice as deep as minimax in the same amount of time. Though this algorithm returns the same score as minimax. But it returns the same result in faster time. 
In this algorithm, the subtrees are temporarily dominated by either a first player advantage (when many first player moves are good, and at each search depth the first move checked by the first player is adequate, but all second player responses are required to try and find a refutation), or vice versa. This advantage can switch sides many times during the search if the move ordering is incorrect, each time leading to inefficiency. As the number of positions searched decreases exponentially each move nearer the current position, it is worth spending considerable effort on sorting early moves. An improved sort at any depth will exponentially reduce the total number of positions searched, but sorting all positions at depths near the root node is relatively cheap as there are so few of them. In practice, the move ordering is often determined by the results of earlier, smaller searches, such as through iterative deepening.

       

## Method and Implementation

The implementation has been written in the function myAIAlgorithm() of the Java file aiTicTacToe.java. 


## Limitations

This neural network will introduce some non-linearity in the analysis but it will not be scalable. The network will also not be able to We will be hard coding the forward and backward propagation steps in the neural network.

This neural network will only be able to understand the very simple non-linear functions. As we are using only 1 hidden layer, the network can introuce only 1 layer of non-linearity in the network. To calculate more complex function, we can select a network with more number of nodes in hidden layer, but a better way to go about it to introduce more layers in the network.
Define your evaluation metrics, e.g., detection rates, accuracy, running time.

## Exploration

Hyperparameters for the network :

1. Number of nodes in the hidden layer
2. Learning Rate
3. Number of Epochs
We will also understand the effect of these hyperparameters on our network by analysing the test error and train error in our network.




