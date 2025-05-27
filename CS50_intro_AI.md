# Lecture 0 Playing
minimax as other ai course
* alpha beta pruning - ignore states in the calculation if there is already a better state 
## Monte Carlo Tree Search
simulate randomly a lot of games.  
compare the results of the simulated games (how often does X win) for two or more different starting changes to determine the 'best' next step  

exploring - with just a few iterations its sensible to explore 'bad' looking options because its likely that the good options are just not found yet   
exploiting - making a choice based on the given data after more iterations, exploiting the knowledge   

in mote carlo tree search during the iterations the combinations are not completely random, there is balance between exploring 'bad' looking options and exploiting the ones that already look promising.  

## reinforcement Learning
learning through remward and punishment  

q learning  
is a n algorith where the agent learns through adding up reward over time. for example in Snake running into a barrier could be -100, getting food +10, moving without incident 0, the agent keeps track of the state the action and the reward and learns though trying to maximise its reward.  

# Lecture 1 Predicting