---
title: Reinforcement Learning - 2
layout: post
math: true
---

## How to solve MDP?
Once we have converted our problem to MDP, we will now develop tools to solve the MDP.This includes Policy and Value Function which tell us about a state and action.

### Policy Function
A policy $\pi$ is a mapping function from each state and action to the probability $\pi(s,a)$ of taking action a in state s.

### Value Function
For each policy $\pi$ we have a particular value function $V^{\pi}(s)$. The value function denotes what return can the agent expect from going on a particular state. It seems like the obvious tool we would require to solve any problem. As in real life, we need a metric to compare two states according to the return they give.

$$ V^{\pi}(s) = E_{\pi}\{R_t|s_t=s\} = E\{\sum\limits_{k=0}^\infty{\gamma^k R_{t+k+1} | S_t=s}\}$$

Value function of a termianl state is always 0.

### Q-Function
Q function can be defined as expected return from taking action **a** on state **s**.

$$Q^{\pi}(s,a) = E_{\pi}[G_t | S_t = s, A_t = a] = E[\sum\limits_{k=0}^{\infty}{\gamma^k R_{t+k+1} | S_t=s , A_t=a}]$$

Later on we will discuss on how to estimate these values to solve the given MDP.

We can write the value function formula which connects $V(s)$ to $V(s+1)$.

$$V(s) = \sum\limits_a \pi(a|s) \sum\limits_{s',r}p(s',r|s,a)[r + \gamma V_{\pi}(s')]$$


This is called Bellman's equation for value function.It epresses the relation between the value of a state and the values of its successor states.

### Optimal Functions

We can image $(V_{\pi},\pi)$ as a set of Value function and Q-function which are connected to each other. There are infinite number of these pairs to choose from to use for our MDP. One of all these pairs there is only optimal policy and value function, which maximizes our returns.

We can denote them as follows - 

Value functions defines a partial ordering over policies. A policy $\pi$ is defined to be better than or equal to a policy $\pi '$ if its expected return is greater than or equal to that of $\pi '$ for all states.


$$v_*(s) = \max\limits_{\pi} v_{\pi}(s) \text{   for all } s \in S$$ 

same goes for Q - functions

$$q_*(s,a) = \max\limits_{\pi} q_{\pi}(s,a) \text{   for all } s \in S \text{ and a} \in A(s)$$


Now we have the tools to solve MDP, now we need to figure out how to calculate these functions in real-life problems. As real-life problems are very complex with possibly infinite states, we need approximate solution methods to find the value,policy and Q functions.