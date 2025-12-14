---
layout: post
title:  "Baird's Counterexample Meets Optimization"
math: true
tags: [rl]
---

Baird's counterexample is a canonical concrete system that demonstrates the instability of semi-gradient Q-learning in the presence of the so-called "deadly triad" of reinforcement learning: functional approximation, off-policy learning, and bootstrapping. This post sheds light on Baird's counterexample and the deadly triad from the perspective of traditional optimization theory, demonstrating that the underlying principles are nothing more exotic than well-established gradient descent convergence guarantees.

# Setup

Baird's counterexample is a simple Markov decision process with 7 states: one "upper" state and six "lower states". An agent at any lower state transitions deterministically to the upper state, while an agent at the upper state will transition at random to one of the six lower states. There are no rewards in this system, so the true value function $$V^{\star}$$ is identically 0 for all states.

We parameterize the value function with a linear model $$V_{\theta}(s) = \phi(s)^T \theta$$, where $$\phi(s)$$ is a feature vector corresponding to state $$s$$ and $$\theta$$ are the learned feature weights, which we wish to optimize with temporal difference (TD(0)) learning.

The TD(0) update rule at step $$t+1$$ takes the form $$\theta_{t+1} = \theta_t + \eta \delta_t \nabla_{\theta} V_{\theta}$$, where $$\delta_t = r_t + \gamma V_{\theta}(s_{t+1}) - V_{\theta}(s_t)$$ represents the current approximation error between $$V_{\theta}$$ and $$V^{\star}$$ ($$\eta$$ is the learning rate, $$\gamma$$ is the discount factor for future rewards, and $$r_t$$ is the reward at state $$s_t$$). Our linear model for $$V_{\theta}$$ gives $$\nabla_{\theta} V_{\theta} = \phi(s_t)$$, so the expected update can be written as

\\[ \Delta \theta = \mathbb{E}_{d_b} [ \eta (r_t + \gamma \phi_{t+1}^T  \theta_t - \phi_t^T \theta_t ) \phi_t ] \\]
where $$d_b$$ is the distribution over states drawn from the behavior policy $$b$$.



