# Reducing the dimensionality of data with neural networks

High-dimensional data can be converted to low-dimensional codes by training a multilayer neural network with a small central layer to reconstruct high-dimensional input vectors. Gradient descent can be used for fine-tuning the weights in such ‘‘autoencoder’’ networks, but this works well only if the initial weights are close to a good solution. The paper's proposes an effective way of initializing the weights that allows deep autoencoder networks to learn low-dimensional codes that work much better than principal components analysis as a tool to reduce the dimensionality of data.
It is difficult to optimize the weights in nonlinear autoencoders that have multiple hidden layers. Furthermore, with large initial weights, autoencoders typically find poor local minima; with small initial weights, the gradients in the early layers are tiny, making it infeasible to train autoencoders with many hidden layers.

## Restricted Boltzmann Machine

A restricted Boltzmann machine (RBM) is a generative stochastic artificial neural network that can learn a probability distribution over its set of inputs. As their name implies, RBMs are a variant of Boltzmann machines, with the restriction that their neurons must form a bipartite graph: a pair of nodes from each of the two groups of units (commonly referred to as the "visible" and "hidden" units respectively) may have a symmetric connection between them; and there are no connections between nodes within a group.
In short, the rbm is going to define a distribution over x, and that distribution is actually going to involve some latent variables which correspond to your binary hidden units h.
The canonical RBM is an energy-based model with binary visible and hidden units. Its energy function is: E(v, h) = −bT*v − cT*h −vT*W*h, where b,c and W are unconstrained, real valued, learnable parameters. Once we obtain the energy function, we can define the p(x,h) as exp(E(v, h))/Z, where z is partition function and is intractable (to normalize probability between 0 and 1). Note that, h is conditionally independent given x. Hence, p(h|x) = p(h1|x)* ... * p(h_n|x). Furthermore, p(h_j = 1|x) = sigmoid(b_j + W_j*x) and p(x_k = 1|h) = sigmoid(c_k + hT*W_k). The exact proof is better explained in Hugo Larochelle's lecture : [Link](https://www.youtube.com/watch?v=lekCh_i32iE)

## Pre-training

Pretraining consists of learning a stack of restricted Boltzmann machines (RBMs), each having only one layer of feature detectors. The learned feature activations of one RBM are used as the data for training the next RBM in the stack. After the pretraining, the RBMs are decoded to create a deep autoencoder, which is then fine-tuned using backpropagation of error derivatives. This has proven to start off at a good initialization and would decrease the probability of the network falling in bad local minima.

## Paper link

http://www.cs.toronto.edu/~hinton/science.pdf
