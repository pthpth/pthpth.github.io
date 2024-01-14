---
title: Reinforcement Learning - 4
layout: post
math: True
---

# Monte Carlo 
Wikipedia describes Monte Carlo as 
> 'Monte Carlo methods, or Monte Carlo experiments, are a broad class of computational algorithms that rely on repeated random sampling to obtain numerical results. The underlying concept is to use randomness to solve problems that might be deterministic in principle. They are often used in physical and mathematical problems and are most useful when it is difficult or impossible to use other approaches. Monte Carlo methods are mainly used in three problem classes:optimization, numerical integration, and generating draws from a probability distribution.'

Basically we repeat the process in hand and keep noting down all the values we obtain and then we average it out (or some other method of aggregation). The process can be sampling from a distribution, adding values from a function to integrate and in our case traverse the MDP to calculate value functions.


## Value Function
So how we calculate value function of MDP using Monte Carlo? As we discussed we note down the numerical value and then average it out, The value here is the returns from a state.

Supouse we have some episode in the MDP we obtained from following the policy, We want to evaluate the value of the policy at state S. We have have visited S multiple times in that episode.
- The first-visit MC method estimates $v_{\pi}(S)$ as the average of the returns following the first visit to s, whereas
- every-visit MC method averages the returns following all visits to s.

## Pseudocode for first-visit MC
![MC](/assets/images/mc.png)
As the number of episodes increases $v_{\pi}(s)$ converges to the true value.


Now the next step would be to calculate action values using Monte Carlo method. To calculate that we need to first to do policy evaluation.
Now we will calculate $q_{\pi}(s,a)$ using Monte Carlo method.

Suppouse our policy is deterministic i.e for every state we will only take 1 fixed action. But for calculating q values for each pair we need to perform each possible action at a state. To solve this we will have to **explaore**.

## Exploration vs Exploitation
In the first post we discussed this topic briefly. This is one of the key features of RL. 
_What is exploiation?_ Suppouse we have a policy $\pi$, which is deterministic. We always know which option is best.We will keep on taking the _optimal_ step **according to this policy** , this is called Exploitation.
_What is exploration?_  Exploration is going off the current policy to find a better path possibly. This is required to find better policies for the problem. 

For successfully training an agent for any MDP, we need to balance these two things. If we only exploit, we will stick to the first better option we get and never explore to find any new actions.If we explore a lot, we will be stuck in the initial stages of the.mdenvironment and wont move on towards the terminal step.

So to solve for the action values in a deterministic policy, we, assign each state-action pair a non-zero starting probability. So basically the episode can start at any given state and any given action, as the number of episodes increase, we will obtain action values for each state-action pair.
This is very simillar to random jumps we use in [Page Rank](https://en.wikipedia.org/wiki/PageRank) to work with Cyclic MDPs.

# Monte Carlo Control
Remember [here]({% post_url 2024-01-04-reinforcement-learning---3- %}) we talked about Policy Improvement as a step by step process of Policy Evaluation and Policy Iteration