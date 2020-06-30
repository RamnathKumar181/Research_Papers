# AMC-AutoML for Model Compression and Acceleration of Mobile Devices

This paper proposes a novel compression algorithm which allows us to efficiently deploy neural network models on mobile devices, etc. Previously, models were compressed using hand-crafted heuristics and rule-based policies that require domain expert knowledge. Their algorithm is automated and less time consuming than others of the same kind. They create a reinforcement learning model called DDPG which penalizes accuracy loss while encouraging model shrinking and speedup. This agent works in a layerwise manner.

## AMC

The AMC algorithm can be broadly broken down into 3 different parts as follows.

### Compression strategy

Two types of pruning strategy are experimented with in this work. The fine-grained pruning strategy prunes unimportant values in the weights or the weights with least magnitude. Coarse-grained pruning refers to dropping entire channels,rows or columns.

### Policy gradient RL

For this section, the deep deterministic policy gradient(DDPG) is employed. The state space s_t is defined by 11 different features for layer t, where t is layer index. Before being passed to the agent, they are scaled with [0,1].The agent receives an embedding state s t of layer L t from the environment and then outputs a sparsity ratio as action a_t . The underlying layer is compressed with a_t using a specified compression algorithm. Then the agent moves to the next layer L t+1 , and receives state s t+1 . After finishing the final layer L T , the reward accuracy is evaluated on the validation set and
returned to the agent.

### Reward function

Based on the constraint, the reward function is given as follows:
'''
R_metric = -Error * log(metric)
'''
In resource constrained optimization, we do not use a constraint. i.e. R_error = -Error. For instance, in fine-grained pruning, a is allowed to take any value for the first few layers, and later limits a, allowing an agent to achieve a target compression ratio.
In accuracy constrained optimization, we use FLOPs, #params and latency in the reward function as defined earlier.This also shows that any type of metric: proxy(FLOPs, #params) and real-time(latency) can be plugged in.
The paper goes on to provide clear experimental results on CIFAR-10 and a subset of ImageNet which clearly explain the performance boost over all previous research works.

## Paper link

https://arxiv.org/pdf/1802.03494.pdf
