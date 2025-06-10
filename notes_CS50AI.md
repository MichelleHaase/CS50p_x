# CS50AI Lecture 0 Search
* agent - entity that perceives environment and acts upon it
* state - configuration of agent, initial state - state where agent begins problem solving
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

## search Algorithms
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
```python
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
* is more effective the closer initial and goal state lay together
* always returns optimal, might explore every state to get there
  
```python
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
* works similar to greedy best-first but also takes the cost to reach each node(steps) into consideration
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

# CS50AI Lecture 1 Knowledge
## knowledge based agents
agents that reason on internal representations of knowledge   
* sentence - assertion in a knowledge representation language   
* knowledge base - set of sentences that the ai knows are true   
* inference - process of deriving new sentences based on old ones
## Propositional logic
* uses propositional symbols that represent sentences or facts like P Q R
* logical Connectives ¬ not; ∧ and; ∨ or; → implication; ↔ bi-conditional  
* or includes the possibility of both being right just one would be XOR (⊕)
<br>
### Truth tables   
NOT (¬)   

| P | ¬P |   
|---|----|   
| False | True |   
| True | False |   

AND (∧)

| P | Q | P∧Q |
|---|---|-----|
| False | False | False |
| False | True | False |
| True | False | False |
| True | True | True |

OR (∨)

| P | Q | P∨Q |
|---|---|-----|
| False | False | False |
| False | True | True |
| True | False | True |
| True | True | True |

Implication (→)

| P | Q | P→Q |
|---|---|-----|
| False | False | True |
| False | True | True |
| True | False | False |
| True | True | True | 

if P is true Q must be true for P to imply Q, if P is false the implication cant be falsified so its true.   
Consider a promise:

  Promise: “If I pass the exam (P), then I will celebrate with a party (Q).”

Here are the scenarios:

  If you do pass (P is true) and there is a party (Q is true), the promise is fulfilled.

  If you pass and no party is thrown, the promise is broken (true antecedent, false consequent → implication false).

  If you do not pass (P is false), then whether or not there is a party doesn’t affect the promise because the promise was only about the case of passing. In logic, we call this situation “vacuously true” because the condition that would need to be tested (passing) never actually occurred.

* entailment (⊨)   
α ⊨ β

 alpha entails beta, in every model in which α is true, β is also true

### model checking
knowledge Base : (P ∧ ¬Q) → R
check: KB(knowledge Base) ⊨ α
query (α) - is R True

| P | Q | R | KB |
|---|---|---|---|
| False | False | False | False |
| False | False | True | False |
| False | True | False | False |
| False | True | True | False |
| True | False | False | False |
| True | False | True | True |
| True | True | False | False |
| True | True | True | False |

KB ⊨ α is only true for one instance in this case
### inference rules
#### Modus Ponens 

|  |  |
|--|--|
| α → β  | if alpha entails beta |    
| α      | if alpha is true |
| β      | beta is true can be inferred 

#### And Elimination

|  |  |
|--|--|
| α ∧ β  | if alpha and beta is true |
| α | then just alpha is true | 

#### Double Negation Elimination

|  |  |
|--|--|
| ¬(¬α)  | not alpha is not true |
| α | then alpha is true | 

#### Implication Elimination

|  |  |   |
|--|--| --|
| α → β | if alpha implies beta | if its raining he is inside
| ¬α v β| if not alpha beta is true | either it's not raining or he is inside

#### Bi-conditional Elimination

|  |  |   |
|--|--| --|
| α ↔ β | if alpha Bi-conditionally implies beta | only if it is raining hes is inside
| (α → β) ∧ (β → α) | alpha implies beta and beta implies alpha | if it's raining he's inside; If he's inside it's raining

#### De Morgan's Laws

|  |  |   |
|--|--| --|
| ¬(α ∧ β) | if not alpha and beta | it is not true that a and b passed the test
| ¬α v ¬β | either not alpha or not beta  | a did not pass the test OR b did not pass the test


|  |  |   |
|--|--| --|
| ¬(α v β) | if not alpha or beta | it is not true that a or b passed the test
| ¬α ∧ ¬β | neither alpha nor beta  | a did not pass the test and b did not pass the test

#### Distributive Property

|  |  |
|--|--|
| (α ∧ (β v γ)) | alpha and, beta or gamma are true | 
| (α ∧ β) v (α ∧ γ) | alpha and beta,  or alpha and gamma are true  |

|  |  |
|--|--|
| (α v (β ∧ γ)) | alpha or beta and gamma are true | 
| (α v β) ∧ (α v γ) | alpha or beta and alpha or gamma are true  |

### Theorem Proving 
initial state = knowledge base
actions = inference rules
transition model = updated KB after inference
goal test = checking alpha fro KB ⊨ α query
path cost = number of steps in the proof

clause - a disjunction od literals, propositional symbols connected with or - P v R  
conjunctive normal form (CNF) - logical sentence that is a conjunction (connected by and) of clauses(connected by or)- (P v R) ∧ (D v ¬E) ∧...   
<br>
achieve CNF  
1. Eliminate (change form with inference) bi-conditionals
2. Eliminate implications
3. move ¬ inwards with De Morgan's Laws
4. use distributive Law to distribute v where ever possible

example  
( P v Q) -> R  
¬(P v Q) v R - eliminate implication  
(¬P ∧ ¬Q) v R - De Morgan's Law  
(¬P v R) ∧ (¬Q v R) - distribution --> CNF  

### Inference by resolution (requires CNF)

|  |  |
|--|--|
| P v Q | 
| ¬P v R |
| (Q v R) | resolution|

|  |  |
|--|--|
| P v Q v S | 
| ¬P v R v S|
| (Q v R v S) | resolution|
keeping S double doesn't change the logic of the sentence so it's cancelled 
an empty clause in resolution is always false as in resolving ¬P and P to ()

* to determine KB ⊨ α check KB ∧ ¬α (check by contradiction) if ¬α is contradicted α isd True otherwise there is no entailment(⊨)

KB ∧ ¬α to CNF   
looping over data and simplifying with resolution  
if an empty clause is the result the contradiction is proofed and alpha is true  
example   
KB: (A v B) ∧ (¬B v C) ∧ (¬C)
Query KB ⊨ A (does the knowledge entail A)   
first check the negative so ¬A   
(A v B) ∧ (¬B v C) ∧ (¬C) ∧ (¬A)   
(¬B v C) ∧ (¬C) = (¬B) = (A v B) ∧ (¬B v C) ∧ (¬C) ∧ (¬A) ∧ (¬B)   
(¬B) (A v B) = (A) = (A v B) ∧ (¬B v C) ∧ (¬C) ∧ (¬A) ∧ (¬B) ∧ (A)   
(A) (¬A) = ()

## First-Order Logic
constants - represent objects like person places  
Variables - stand for arbitrary objects like x y z    
Predicate - properties or relationships like loves(x,y), Returns a bool     
quantifiers * Universal(∀) - for all ∀x isHuman(x), every x is human  
            * Existential (∃) - there exists - ∃x Loves(x, John) someone love John     
functions - Map object to another like MotherOf(x), Returns an object   
logical connectives - as in propositional (¬, ∧, ∨, →, ↔)  

#CS50AI Lecture 2 Uncertainty
probability - range 0-1 on a 6 sided die roll 0 would be a 7 so impossible and one die with only three's a three would be certain so a probability of 1 represented mathematcally P(ω) is the probabiolity of a worldview.   
ω represents the world we're looking at and Ω represents all the possible worlds. if all ω in Ω are added up the result is 1 since all the possiblilitys are accounted for so one of them must be true. this    
![probability](probability.png)
means the probability of the sum from all worlds in all possible worlds equals 1.   
