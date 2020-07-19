# Large-Scale Study of Curiosity-Driven Learning

Reinforcement learning is a great approach to train an agent to perform a specific task in a given environment. However, annotating each environment with
hand-designed, dense rewards is not scalable, motivating the need for developing reward functions that are intrinsic to the agent. This paper experiments with these intrinsic reward functions and proves that they still are able to achieve good performances. The central idea is to represent intrinsic reward as the error in predicting the consequence of the agent’s action given its current state, i.e., the prediction error of learned forward-dynamics of the agent.

## Dynamics-based Curiosity-driven Learning

Consider an agent that sees an observation x_t , takes an action a_t and transitions to the next state with observation x_t+1 . We want to incentivize this agent with a reward r_t relating to how informative the transition was. An agent trained to maximize this reward will favor transitions with high prediction error, which will be higher in areas where the agent has spent less time, or in areas with complex dynamics. To provide this reward, we use an exploration bonus involving the following elements:
(a) a network to embed observations into representations φ(x),
(b) a forward dynamics network to predict the representation of the next state conditioned on the previous observation and action p(φ(x_t+1 )|x_t,a_t). Given a transition tuple {x_t,x_t+1,a_t}, the exploration reward is then defined as r_t = − log p(φ(x_t+1)|x_t,a_t ), also called the surprisal.

### Feature spaces for forward dynamics

The feature space φ in the curiosity formulation above is extremely important. The feature space should have the following features:
* Compact: The features should be easy to model by being low(er)-dimensional and filtering out irrelevant parts of the observation space.
* Sufficient: The features should contain all the important information.
* Stable: Non-stationary rewards make it difficult for reinforcement agents to learn.

With the characteristics being laid down, we have a few options for the feature space:
* Pixels: φ(x) = x. It is stable, and sufficient but not compact.
* Random Features(RF): The next simplest case is where we take our embedding network, a convolutional network, and fix it after random initialization. It would be stable but might not be compact and sufficient.
* Variational Autoencoders(VAE): This is a feedforward network that takes an observation as input and outputs a mean and variance vector describing a Gaussian distribution with diagonal covariance. These would be compact and sufficient but not stable.
* Inverse Dynamics Features(IDF):Given a transition (s_t,s_t+1,a_t) the inverse dynamics task is to predict the action a_t given the previous and next states s_t and s_t+1. A potential downside could be that the features learned may not be sufficient, that is they do not represent important aspects of the environment that the agent cannot immediately affect.

### ‘Death is not the end’: discounted curiosity with infinite horizon

One important point is that the use of an end of episode signal, sometimes called a ‘done’, can often leak information about the true reward function. If we don’t remove the ‘done’ signal, many of the Atari games become too simple. For example, a simple strategy of giving +1 artificial reward at every time-step when the agent is alive and 0 on death is sufficient to obtain a high score in some games. In the case of negative rewards, the agent will try to end the episode as quickly as possible. Therefore, we removed ‘done’ to separate the gains of an agent’s exploration from merely that of the death signal. In practice, we do find that the agent avoids dying in the games since that brings it back to the beginning of the game, an area it has already seen many times and where it can predict the dynamics well.

### Limitation of prediction error based curiosity
A more serious potential limitation is the handling of stochastic dynamics. If the transitions in the environment are random, then even with a perfect dynamics model, the expected reward will be the entropy of the transition, and the agent will seek out transitions with the highest entropy. Even if the environment is not truly random, unpredictability caused by a poor learning algorithm, an impoverished model class or partial observability can lead to exactly the same problem.

## Paper link

https://arxiv.org/pdf/1808.04355.pdf
