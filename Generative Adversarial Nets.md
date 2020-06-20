# Generative Adversarial Nets

The GAN usually consists of two networks - a Generator(G) and a Discriminator(D). The idea is that the two networks play a minimax two-player game where, the goal of G is to create data capable of fooling D, and the goal of D is to not get fooled by G. If allowed to run for millions of iterations, the entire network reaches a very good understanding of the distribution of the data, and can replicate it.  

## Adversarial Nets

The idea is that we try to train D to maximize the probability of assigning the correct label to both training examples and generated examples. Furthermore, we train G to minimize log(1-D(G(z))). The two players play a minimax game with the value function V(G,D).

The authors also suggest that training the two networks in an iterative way leads to overfitting on small datasets. Instead, we train k steps of D and one step of optimizing G. Hence, D will remain around optimal as long as G changes slowly enough.

There are also a few proofs to support their claims. A simple summary is given below.

### For fixed G, the optimal D is D* = p_data(x)/(p_data(x) + p_g(x))

While training D, our goal is to maximize V(G,D). Just simplifying the "expected" terms to integral allows us to reach a very simple equation of alog(y) + blog(1-y). The value of y which maximizes this equation is a/(a+b) as long as a and b are both not equal to 0. Hence, we prove the above statement.

### The global minimum of the virtual training criterion C(G) is achieved if and only if p_g = p_data . At that point, C(G) achieves the value − log 4.

With a simple addition and subtraction of log(4), we can explain the same equation in terms of KL divergence. This can further be simplified to Jensen Shannon Divergence. The final equation we have is now -log(4) + 2.JSD(p_data||p_g). Since, JSD is a function in the range of 0-1. The minimum of this equation will occur when JSD gives a output of 0. This only happens when p_g = p_data. Hence, we have proved the above statement.

## Proving Convergence of the Algorithm

To the best of my knowledge, there is no proof which claims that neural networks converge at global optimum. However, its excellent performance in practice suggests that they are a reasonable model despite their lack of theoretical guarantees.

## Paper link

http://papers.nips.cc/paper/5423-generative-adversarial-nets.pdf
