# Lecture 1 - Introduction to Reinforcement Learning

[[slides](http://www0.cs.ucl.ac.uk/staff/d.silver/web/Teaching_files/intro_RL.pdf)]
[[video](https://www.youtube.com/watch?v=2pWv7GOvuf0)]

## Characteristics
- No supervisor, only a reward signal
- Feedback is delayed, not instantaneous
- Time matters, we have sequential non-iid data
- Agents actions affect subsequent data it receives
## Rewards
- Reward <img alt="$R_t$" src="tex/svgs//7f8a20dacaccab775d1e690bcf0f49e1.png?invert_in_darkmode" align=middle width="17.447265000000005pt" height="22.46574pt"/> is a scalar feedback signal
- Agents job is to maximize it's cumulative reward
- Reward Hypothesis: All goals can be described as the maximization of cumulative rewards.
## Sequential Decision Making
- The goal is to select actions which maximize total future reward
## History
- <img alt="$H_t = A_1, O_1, R_1, ..., A_t, O_t, R_t$" src="tex/svgs//c15749c14abe93abe0e9b04b15a12150.png?invert_in_darkmode" align=middle width="212.26705499999997pt" height="22.46574pt"/>
- Defined as all observables up to time <img alt="$t$" src="tex/svgs//4f4f4e395762a3af4575de74c019ebb5.png?invert_in_darkmode" align=middle width="5.936155500000004pt" height="20.222069999999988pt"/>
- Entirely determines what can happen next
## State
- Defined as all information used to decide what happens next
- <img alt="$S_t = f(H_t)$" src="tex/svgs//2166b0ec2e84321839a449966e7a13f8.png?invert_in_darkmode" align=middle width="79.84020000000001pt" height="24.65759999999998pt"/>, any function of the history can be a state
- Environment state <img alt="$S_t^e$" src="tex/svgs//1d28b1d0b6c75d75d3c3b883a31b29bb.png?invert_in_darkmode" align=middle width="17.264445000000002pt" height="22.46574pt"/> is it’s private representation of the world (e.g. Atari memory).
  - Usually hidden from an agent, so it cannot depend on this
- Agent state <img alt="$S_t^a$" src="tex/svgs//8d4502ee67885ff60280a6a6212d399f.png?invert_in_darkmode" align=middle width="18.157755000000005pt" height="22.46574pt"/> is it’s internal representation of the world; this is what we must design.
## Information State (Markov State)
- Contains all useful information from the history
- A state <img alt="$S_t$" src="tex/svgs//9f8bba50b95de09625626ddafa0698eb.png?invert_in_darkmode" align=middle width="15.045855000000003pt" height="22.46574pt"/> is Markov iff <img alt="$P[S_{t+1}|S_t] = P[S_{t+1}|S_1,...,S_t]$" src="tex/svgs//3a69213aee0351c0284e738f2dd7a4c8.png?invert_in_darkmode" align=middle width="217.51240499999997pt" height="24.65759999999998pt"/>
- “The future is independent of the past given the present”
- “The state is a sufficient statistic of the future”
- <img alt="$S_t^e$" src="tex/svgs//1d28b1d0b6c75d75d3c3b883a31b29bb.png?invert_in_darkmode" align=middle width="17.264445000000002pt" height="22.46574pt"/> and <img alt="$H_t$" src="tex/svgs//7e079fda336460481fecbdc8d4a08446.png?invert_in_darkmode" align=middle width="18.630315000000007pt" height="22.46574pt"/> are both Markov states
## Fully Observable Environments
- An agent directly observes the environment state
- <img alt="$O_t = S_t^a = S_t^e$" src="tex/svgs//8ffdf3b3cb0598e63fe89f34a1242401.png?invert_in_darkmode" align=middle width="98.405835pt" height="22.46574pt"/>, a Markov Decision Process (MDP)
## Partially Observable Environments
- An agent indirectly observes the environment state
  - e.g. a robot’s camera vision, stock prices, public poker cards
- <img alt="$S_t^a \neq S_t^e$" src="tex/svgs//fda0b0f5932f5f0467dd1af85946bbbb.png?invert_in_darkmode" align=middle width="58.161675pt" height="22.831379999999992pt"/>, a Partially Observable MDP (POMDP)
- We must choose the agent’s state representation
## Components of an Agent

**Policy**

- An agent’s behaviour function
- <img alt="$a = \pi(s)$" src="tex/svgs//2afd7aaff2306a902c027fe99967b373.png?invert_in_darkmode" align=middle width="61.05792pt" height="24.65759999999998pt"/> for deterministic policies
- <img alt="$\pi(a|s)$" src="tex/svgs//a5f75f5c24cae21447686b47e4f99d38.png?invert_in_darkmode" align=middle width="43.70652pt" height="24.65759999999998pt"/> for probabilistic policies

**Value Function**

- An agent’s evaluation of how good each state and/or action is
- <img alt="$v_{\pi}(s) = E_{\pi}[R_t + \gamma R_{t+1} + ... | S_t=s]$" src="tex/svgs//50999077dd63fd2d6a951317cd62a81d.png?invert_in_darkmode" align=middle width="256.03165499999994pt" height="24.65759999999998pt"/>, where <img alt="$\gamma$" src="tex/svgs//11c596de17c342edeed29f489aa4b274.png?invert_in_darkmode" align=middle width="9.423975000000004pt" height="14.155350000000013pt"/> is a discounting factor
  - The value of state <img alt="$s$" src="tex/svgs//6f9bad7347b91ceebebd3ad7e6f6f2d1.png?invert_in_darkmode" align=middle width="7.705549500000004pt" height="14.155350000000013pt"/> under policy <img alt="$\pi$" src="tex/svgs//f30fdded685c83b0e7b446aa9c9aa120.png?invert_in_darkmode" align=middle width="9.960225000000003pt" height="14.155350000000013pt"/> is equal to the discounted cumulative reward when selecting actions under this policy

**Model**

- An agent’s representation of it’s environment
- <img alt="$P_{ss'}^a = P[S'=s'|S=s, A=a]$" src="tex/svgs//5426100ce0d98879177ec6b36cde16bf.png?invert_in_darkmode" align=middle width="217.449705pt" height="24.716340000000006pt"/>
  - A transition function which predicts the next state given an action and the current state.
- <img alt="$R_s^a = E[R|S=s, A=a]$" src="tex/svgs//13e6cd3ee75f4400655a46bf293e7a57.png?invert_in_darkmode" align=middle width="172.75945499999997pt" height="24.65759999999998pt"/>
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

