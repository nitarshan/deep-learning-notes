# Lecture 1 - Introduction to Reinforcement Learning

[[slides](http://www0.cs.ucl.ac.uk/staff/d.silver/web/Teaching_files/intro_RL.pdf)]
[[video](https://www.youtube.com/watch?v=2pWv7GOvuf0)]

## Characteristics
- No supervisor, only a reward signal
- Feedback is delayed, not instantaneous
- Time matters, we have sequential non-iid data
- Agents actions affect subsequent data it receives
## Rewards
- Reward $R_t$ is a scalar feedback signal
- Agents job is to maximize it's cumulative reward
- Reward Hypothesis: All goals can be described as the maximization of cumulative rewards.
## Sequential Decision Making
- The goal is to select actions which maximize total future reward
## History
- $H_t = A_1, O_1, R_1, ..., A_t, O_t, R_t$
- Defined as all observables up to time $t$
- Entirely determines what can happen next
## State
- Defined as all information used to decide what happens next
- $S_t = f(H_t)$, any function of the history can be a state
- Environment state $S_t^e$ is it’s private representation of the world (e.g. Atari memory).
  - Usually hidden from an agent, so it cannot depend on this
- Agent state $S_t^a$ is it’s internal representation of the world; this is what we must design.
## Information State (Markov State)
- Contains all useful information from the history
- A state $S_t$ is Markov iff $P[S_{t+1}|S_t] = P[S_{t+1}|S_1,...,S_t]$
- “The future is independent of the past given the present”
- “The state is a sufficient statistic of the future”
- $S_t^e$ and $H_t$ are both Markov states
## Fully Observable Environments
- An agent directly observes the environment state
- $O_t = S_t^a = S_t^e$, a Markov Decision Process (MDP)
## Partially Observable Environments
- An agent indirectly observes the environment state
  - e.g. a robot’s camera vision, stock prices, public poker cards
- $S_t^a \neq S_t^e$, a Partially Observable MDP (POMDP)
- We must choose the agent’s state representation
## Components of an Agent

**Policy**

- An agent’s behaviour function
- $a = \pi(s)$ for deterministic policies
- $\pi(a|s)$ for probabilistic policies

**Value Function**

- An agent’s evaluation of how good each state and/or action is
- $v_{\pi}(s) = E_{\pi}[R_t + \gamma R_{t+1} + ... | S_t=s]$, where $\gamma$ is a discounting factor
  - The value of state $s$ under policy $\pi$ is equal to the discounted cumulative reward when selecting actions under this policy

**Model**

- An agent’s representation of it’s environment
- $P_{ss'}^a = P[S'=s'|S=s, A=a]$
  - A transition function which predicts the next state given an action and the current state.
- $R_s^a = E[R|S=s, A=a]$
  - A reward function which gives the expected (immediate) reward given an action and the current state.

*Note*: Not all of these three are required when constructing an agent.

## Categorizing Agents

**Policy vs Value**

- Value-based (implicit policy function, greedy selection on values)
- Policy-based (no value function, explicit policy)
- Actor-critic (uses both functions)

**Model vs Model Free**

- Model Free (no model, just policy and/or value functions)
- Model Based (use a model in planning)
## Learning and Planning

These are the two fundamental problems of sequential decision making

**Learning**

- The environment is initially unknown
- The agent interacts with the environment to improve its policy

**Planning**

- A model of the environment is known
- The agent simulates interactions with the environment to improve its policy
## Exploration and Exploitation
- Reinforcement learning is like trial and error learning
- An agent should discover a good policy without giving up too much reward along the way
- Contention between discovering more about the environment vs exploiting known information to maximize rewards
## Prediction and Control

**Prediction**

- Evaluating the future given a policy

**Control**

- Optimizing the future by finding the best policy

