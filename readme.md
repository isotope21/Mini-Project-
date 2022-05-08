# Virtual Self Driving Car

## Description

We are creating a virtial self driving car which will choose path to get the destination. Here we are using **Reinforcement Learning** in order to make the agent capable to learn by its own.

## Team
- Akash Gupta
- Shreyas
- Rashmi
- Aishwarya

## Topics

1. Technology Stack
2. Libraries
3. Algorithms
4. Code Overview
5. Conclusion

## Technology Stack
- Python<br>
Python is the high-level and beginner friendly language. It has dynamic garbage collection mechanism which improve the performance of our project. There is lot of libraries available related to machine learning which will save our time and give more flexibility to work on our logic.

## Libraries
1. Pillow<br>
Python Imaging Library is a free and open-source additional library for the Python programming language that adds support for opening, manipulating, and saving many different image file formats.

2. OpenCV<br>
OpenCV is a Python open-source library, which is used for computer vision in Artificial intelligence, Machine Learning, face recognition, etc. We are using OpenCV to make our image alive.

3. Numpy<br>
NumPy is a library for the Python programming language, adding support for large, multi-dimensional arrays and matrices, along with a large collection of high-level mathematical functions to operate on these arrays. We will make our matrices which help to learn our agent using Numpy.

These three are most basic and important libraries which will boost the development time to the next level and complete it faster.

Let's have a look on the algorithm which is used in this project.

## Algorithms

**Q-learning Algorithm**

Q-learning is a model-free **reinforcement learning algorithm** to learn the value of an action in a particular state. It does not require a model of the environment (hence "model-free"), and it can handle problems with stochastic transitions and rewards without requiring adaptations.

**Reinforcement Learning**

Reinforcement learning involves an agent, a set of states {\displaystyle S}S, and a set {\displaystyle A}A of actions per state. By performing an action {\displaystyle a\in A}a\in A, the agent transitions from state to state. Executing an action in a specific state provides the agent with a reward (a numerical score).

The goal of the agent is to maximize its total reward. It does this by adding the maximum reward attainable from future states to the reward for achieving its current state, effectively influencing the current action by the potential future reward. This potential reward is a weighted sum of expected values of the rewards of all future steps starting from the current state.

After giving the short discussion of the Q-learning and Reinforcement learning We will look at the formula to get the Q-values of the particular state.

<div style="background:white">

![Q-learning Formula](https://wikimedia.org/api/rest_v1/media/math/render/svg/678cb558a9d59c33ef4810c9618baf34a9577686)

</div>

After looking at the theory we will look at the some parts of the code where you will see the practical implementation of the theory.

## Code Overview

### Initialization of the Q-table

Q-table is the mapping of the observation with the action in which agent will look at to get the best optimal next step. We are initilizing the Q-table with all zeros

```python
q_table = {}
for x1 in range(-SIZE + 1, SIZE):
    for y1 in range(-SIZE + 1, SIZE):
        for x2 in range(-SIZE + 1, SIZE):
            for y2 in range(-SIZE + 1, SIZE):
                q_table[((x1, y1), (x2, y2))] = [0, 0, 0, 0]
```

After the Q-table it's become very interesting to know how our agent will use this q-table to see the action.

So let's find out the mistry.

```python
if np.random.random() > epsilon:
    action = np.argmax(q_table[obs])
else:
    action = np.random.randint(0, 4)
```
You can see we are using max-greedy algorithms to get the action which has maximum reward point. Here we have used epsilon. But why we are using epsilon..??

Epsilon decides whether agent have to explore the new trajectory or exploit the trajector which he has explored already.

Now we will see how our reward and penaly system works.

```python
if (agent.x, agent.y) in BLOCKED_N:
    reward = -WALL_PENALTY
elif agent.x == DESTINATION[0] and agent.y == DESTINATION[1]:
    reward = DESTINATION_REWARD
else:
    reward = -MOVE_PENALTY
```

Our agent will get penalty if it hits the wall of the environment or roaming around. It will get reward also if it gets to the destination.

Now we will look the formula into the code.

```python
if reward == DESTINATION_REWARD:
    new_q = DESTINATION_REWARD
else:
    new_q = current_q + LEARNING_RATE * (reward + DISCOUNT * (max_future_q - current_q))
```

If out agent get to the destination then it will get the destination reward else it will calculate the max reward and update the state in the q-table.

Finally It's done..

## Conclusion

We have made our project with some monimal functionality to demonstrate the theory into code. In the next chapter of this project we can introduct some **Animated Environment** to get some more interest in this project.
