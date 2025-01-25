# CS50AI Lecture 0 Search
* agent - entity that perceives environment and acts upon it
* state - konfiguration of agent, initial state - state where agent begins problem solving
* actions - set possible operations that can be executed per state
* transition model - result function, Result(a,s) returns the state resulting from performing action (a) in state (s), 
  the model is the way to determine what ne state will exits after an action is taken
* state space - the set of all states reachable from initial state by ANY sequence of actions
* graphically the state space is often represented as a graph with node for the spaces and edges for the actions
* goal test - tests if a given state is a goal state
* path cost - numeric cost associated with a given path, so the shortest (cheapest) route is found, might have different 
  cost for different route in the same state space
* optimal solution - solution with the lowest path cost   
<br />
* search problems have initial state, actions , transition model, goal tests and path cost functions   
<br />
* node - Datastructure that keeps track of a 
  * state, 
  * parent( node that generated the current node),
  * an action, that was applied to the parent,
  * a path cost, from the initial state to the current node   
<br />

## search Alogrithms
* frontier is a mechanism that manges the nodes, it starts with just the initial state and an empty set for explored Nodes then it repeats   
  1. stop if frontier is empty --> no Solution
  2. remove a Node from the frontier
  3. if the removed node is the goal state return result
  4. expand the Node and add all possible Nodes to the frontier and the current Node to the explored Set
   
* to expand a node means to consider all possible actions
### depth-first search DFS
* uses a Stack as Data structure for the frontier, last in first out
* this approach goes completely through (as deep as possible) one branch of the graph before it considers another because the last Node added will always be next to be explored
* at beat (lucky) this algorithm can be really fast at worst it will exhaust every possibilty before it finds its Mark
* it might not return the optimal path
```
    # Define the function that removes a node from the frontier and returns it.
    def remove(self):
    	  # Terminate the search if the frontier is empty, because this means that there is no solution.
        if self.empty():
            raise Exception("empty frontier")
        else:
        	  # Save the last item in the list (which is the newest node added)
            node = self.frontier[-1]
            # Save all the items on the list besides the last node (i.e. removing the last node)
            self.frontier = self.frontier[:-1]
            return node
```
### breadth first search BFS
* uses a Queue as Data structure for frontier, first in first out
* goes completely through every level bevor it goes deeper into the initial state
* is more efective the closer inital and goal state lay together
* always returns optimal, might explore every state to get there
  
```
    # Define the function that removes a node from the frontier and returns it.
    def remove(self):
    	  # Terminate the search if the frontier is empty, because this means that there is no solution.
        if self.empty():
            raise Exception("empty frontier")
        else:
            # Save the oldest item on the list (which was the first one to be added)
            node = self.frontier[0]
            # Save all the items on the list besides the first one (i.e. removing the first node)
            self.frontier = self.frontier[1:]
            return node
```
### greedy best-first search
* expands the Node next, that is closes to the goal determined by heuristic function
* heuristic function - h(n) gives an estimate to what a good solution might be
  * the Manhatten Distance estimates distance by assuming grid lines so it gives an estimate of e g how many steps away a goal is. It is just a guess not an answer
* it makes choices based on the estimate of the heuristic, it always chooses the node with smallest h(n)
* might not return optimal
  
### A* Search
* workrs similar to greedy best-first but also takes the cosdt to reach each node(steps) into consideration
* expands the next node that has the lowest g(n) + h(n)\
* g(n) cost to reach current node
* returns optimal if h(n) is admissible (never overestimates) and consistent 
  
### uninformed vs informed search
* uniformed: the search algorithm has no knowledge of the specific problem its solving
  * examples would be DFS or BFS
* informed search uses problem specific knowledge like a general direction to go in
  * e.g greedy best-first search

### adversarial Search
* e g Tic Tac Toe, the objective is not just to win but also not for the opponent to win

#### Minimax Algorithm
* for example in Tic tac toe win states get assigned values, e g O winning as -1, a Tie as 0 and X winning as 1
* in this case X would be the Max player - trying to maximize the Score   
  and O would be the min player - trying to minimize the Score   
  this ensure that a Tie is a preferred option to the opponent winning
* recursive function that goes through the possible decisions and takes the option that has the lowest Value in the end assuming optimal from the opponent 
* there are two functions MIN-Value and MAX- Value that call each other recursively until a terminal state occurs assuming the other function always picks the most optimal option, this gets reevaluated each turn

1. S0 - the board
2. function player(s), returns which players turn it is
3. function actions(s), returns legal moves for State
4. result(s, a) returns the board after the move
5. function Terminal(s), state that terminates game ie winner or tie
6. function utility(s), assigns value to terminal states

#### Alpha-Beta pruning
* optimization for e g MiniMax 
* when looking for lowest Value outcome, if the cost to get to a space is higher than a Space checked before it is pruned and all following options are discarded since it won't be relevant anyway
* alpha beta - based on two values/players/options

#### Depth-limited Minimax
* only goes a certain amount of levels deep into the tree
* evaluation function - estimates the utility at the predetermined depth