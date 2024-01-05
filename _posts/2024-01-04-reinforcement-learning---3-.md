---
title: Reinforcement Learning - 3 
layout: post
math: true
toc: false
---

# How to solve the MDP?
In the last post we discussed about Value,policy and Q functions and find their optimal forms. But we never discussed how to find them for a MDP. We will go over some of the methods now.

## Dynamic Programming
These are the classical algorithms used to calculate the value and policy functions. These are rarely used in real life problems are they require a perfect model of the MDP, which happens rarely. But these are important theoretically and beome basis for many of the practical algorithms.

### Policy Evaluation (Prediction)
First we need to find a method to compute state-value functions for a arbitary policy $\pi$. This is called policy evaluation i.e calculating value functions from a policy.

$$v_{\pi}(s) = \sum\limits_{a} {\pi(a|s)} \sum\limits_{s',r}{p(s',r|s,a)[r + \gamma v_{\pi}(s')]}$$

If we have complete knowledge about the dynamics of the MDP. We can easily solve the equations and calculate the state-value function for each state. The process is solving a system of $\|S\|$ simaltenous linear equations. The time complexity of solving this is very high $O(n^3)$ hence we need some iterative methods to solve the same.

As a starting point lets assume an arbitary (only thing to keep in mind is to keep terminal state values 0) value function $v_0$. We use the bellman equation for state-value function as an update rule.

$$v_{k+1}(s) = \sum\limits_{a} {\pi(a|s)} \sum\limits_{s',r}{p(s',r|s,a)[r + \gamma v_{k}(s')]}$$

<center>As $k \rightarrow \infty$, $v \rightarrow v_{\pi}$</center>

This algorithm is called iterative policy evaluation.

As discussed before state-value function is a metric to measure how good a policy in comparison to another, policy evalution does that exactly.
Now the obvious step would be to find a better policy from state-value function.Thats what we are gonna talk about.

#### Pseudocode for Policy Evaluation
![pseudocode](/assets/images/pseudo.png)

### Policy Improvement

Once we have the value function we can calculate q-values (state-action value). We can use this to improve our policy.
_Policy Improvement Theorem_ - Let $\pi$ and $\pi '$ be any pair of deterministic policies such that, for all $s \in S$.

$$q_{\pi}(s,\pi '(s)) > v_{\pi}(s)$$

Then the policy $\pi'$ must be as good as, or better than $\pi$. That is must obtain greater or equal expected return from all states $s \in S$.

$$\pi'(s) = \arg \max \limits_{a} q_{\pi}(s,a) $$


$$\pi'(s) = \arg \max \limits_{a} \sum\limits_{s',r}{p(s',r|s,a)[r + \gamma v_{\pi}(s')]}$$

This is called Policy Improvement. After repeated process of this we will converge to the optimal policy.

### Policy Iteration
The process of iteratively policy evaluation and policy improvement is called policy iteration.

$$\pi _0 \rightarrow v_{\pi_{0}} \rightarrow \pi _{1} \rightarrow \rightarrow v_{\pi_{1}} \cdots \rightarrow \pi _{*} \rightarrow v_{*}$$

#### Pseudocode for policy iteration
![policy iteration](/assets/images/policyit.png)

### Value Iteration
If we look at policy iteration, policy evaluation step of it is computationaly expensive as it does multiples sweeps of each state. One way to reduce this is do only one update of each state. This doesnt affect the convergence of the the process.

$$v_{k+1}(s) = \max\limits_{a}{\sum\limits_{s',r}{p(s',r|s,a)[r+\gamma v_{k}(s')]}}$$

![value iteration](/assets/images/valueit.png)

In the next post we will discuss methods to solve MDP when we dont have complete information about the models, i.e we dont have the dynamics functions available to us.