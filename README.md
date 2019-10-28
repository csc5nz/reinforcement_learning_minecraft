# Reinforcement Learning on Minecraft
Reinforcement learning for environment navigation on Minecraft    


[Reinforcement learning on Mincraft example on Youtube](https://www.youtube.com/watch?v=n2FjAefLCB0)      
[![Malmo](https://img.youtube.com/vi/n2FjAefLCB0/0.jpg)](https://www.youtube.com/watch?v=n2FjAefLCB0)   

[![Malmo](https://img.youtube.com/vi/n2FjAefLCB0/1.jpg)](https://www.youtube.com/watch?v=n2FjAefLCB0) [![Malmo](https://img.youtube.com/vi/n2FjAefLCB0/2.jpg)](https://www.youtube.com/watch?v=n2FjAefLCB0) [![Malmo](https://img.youtube.com/vi/n2FjAefLCB0/3.jpg)](https://www.youtube.com/watch?v=n2FjAefLCB0)  


Malmo and Mincecraft are used to create the enviroment that the AI agent will navigate. The AI agent doesn't know anything about the world and must learn how to navigate the map to reach the goal without dying. The agent can walk one block in any direction and jump two blocks in any direction. Walking and jumping have a small negative reward. Falling into the water has large negative reward, while reaching the goal has a large positive reward.


### How to Run
- Install Malmo    
- Copy finalproject.py and finalproject.xml into the Python_Example folder in Malmo.    
- Execute: python finalproject.py
   
     
### Objective

The goal is  to create an AI agent in Minecraft which can learn to avoid obstacles. 
The knowledge and experience from this project can be applied to real world problems such as robotics. There might be some scenarios where robots might have to avoid obstacle such as in rescue missions. For instance, trying to rescue a person after an earthquake where the robot will have to jump over obstacles and  gaps on the floor or dodge flying debris. The robot also needs to learn to save energy by using the most efficient strategy to get to its goal.
	
### Background  
In this project I use ideas and techniques from the AI course such as reinforcement learning, rewards/cost, and exploration vs exploitation. I apply algorithmic solutions to robotics problems. 

My agent will learn to avoid holes in the ground by jumping when appropriate to reach the goal location. In addition, my agent will learn to take the most efficient strategy and route by jumping only when necessary and walking the rest of the time. 
	
### Implementation  
 For this problem I'm using Malmo with Minecraft to generate the environment. The environment is a 5x15 blocks sized arena surrounded by walls. There are randomly placed holes in the ground filled with water. If the agent falls in the water it dies. In addition the probability of having holes on the floor increases every even block in the y direction. I added this constrain to make sure that in some occasions the only way to advance towards the goal is to jump over the water.

I am using python to write my code which will control the agent in Malmo. The learning technique used is Qlearning.  My AI agent  uses information about the state of the word, its location, location of the obstacle, location of walls, and reward values. The agent will be able to move in four directions: forward, backward, left, and right. The agent will also be able to jump in the four directions.  The agent should move in such a way to survive and make it to the goal.

The strategy revolves around avoiding holes on the ground and reaching the goal position. If the agent falls on one of the holes it dies. If the agent reaches the goal it wins. The agent can walk in all four directions and jump in all four directions. Walking moves the agent one position while jumping  moves the agent two positions. I used Qlearning which computes the qvalue using a reward system where the rewards are: walking  -1, jumping -2, falling into a hole -100, and reaching the goal 100. 

The algorithm works using 3 main steps: updating the qtable, deciding on the next action to take, and taking the action. In addition there are two main strategies: exploration and exploitation. 

Updating the table consists of figuring out the next  action with the max reward, the current reward, the current state, and the previous action which are used together with    the formula presented in class to update the qtable. The current reward must be computed based on the reward where the agent is currently. The next reward is computed based on where the agent will be next based on the chosen action.

Deciding the next action consists of   finding the action with the maximum reward from the 8 available actions (move in four different directions and jump in four different directions). If any of the actions have the same reward then one of those is chosen at random to avoid getting stuck. If the goal is to exploit then this strategy would be enough.  However, we want to explore first to learn the best strategy. To do so, the algorithm needs to try some random moves. I used a epsilon of .05 to explore which every so often chooses a random move from the 8 different ones which allows the agent to learn. In addition, this epsilon gets smaller as the number of trials increases. This is done to focus more on exploitation after the agent behaves more efficiently and correctly.

Finally, the last step is taking the action. To do so, I use a series of if statements to choose the correct movement command for Malmo matching the chosen action.  Actions are discrete because Mlamo has multiple problems when dealing with continuous movements. Walking in the four different directions moves the agent one block. Jumping in one of the four direction moves the agent two blocks and jumps over obstacles avoiding them. 

### Results
  I ran the program for 150 trials. It is able to find the goal position for the first time after on average around  30 tries. And is able to consistently find the goal position after about 50 tries. As it approaches 100, it becomes more efficient at finding the the goal. In other words, it is able to find a more direct and less costly path. In addition, its exploration reduces to almost non existent. It walks when there is grass available to walk and jumps when there is water in its way. If the shortest distance requires jumping then it will jump.

