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

$$ V^{\pi}(s) = E_{\pi}\{R_t|s_t=s\} = E\{\sum\limits_{k=0}^\infty{\gamma^k r_{t+k+1} | s_t=s}\}$$

Value function of a termianl state is always 0.

## Q-Function
Q function can be defined as expected return from taking action **a** on state **s**.

$$Q^{\pi}(s,a) = E_{\pi}$$

