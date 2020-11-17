# Visualizing data using t-SNE

The authors propose a new technique called "t-SNE" that visualizes high dimensional data by giving each datapoint a new location in a 2D or 3D map. The technique is a variation of the Stochastic Neibhbor Embedding which is much easier to optime and produces significantly better visualizations by reducing the tendency to crowd points together in the center of the map. Principal component analysis (PCA) and classical multidimensional scaling (MDS) are linear techniques that focus on keeping the low-dimensional representations of dissimilar datapoints far apart. They do not focus on keeping similar datapoints close together.

## Stochastic Neighbor Embedding (SNE)

SNE starts by converting high dimensional eucledian distances between datapoints into conditional probabilities that represent similarities. We define conditional probability as p_i|j as proportional to the gaussian distribution N(x_i;x_j,sigma_i). Suppose we compute the same for low dimensional points, call q_i|j. If the model computes correctly, p_i|j = q_i|j if i and j points are similar. Motivated by this observation, SNE aims to find a low-dimensional data representation that minimizes the mismatch between p_i|j and q_i|j. We use the Kullback-Leiber (P|Q) such that the total cost C = p_i|jlog(p_i|j/q_i|j) for all i. Since the KL divergence is not symmetric, different types or error in the pairwise distances in low dimensional map are weighted equally. Now, we need to select an appropriate sigma for every datapoint. In denser regions, a smaller value of sigma. SNE performs a binary search for the value of sigma that produces a P_i with a fixed perplexity that is specified by the user. Perp(P) = 2^(H(P_i)). H(p_i) is the Shannon entropy measured in bits. Perplexity can be interpreted as a smooth measure of the effective number of neighbors. The gradient of the cost function is equal to 2*(p_j|i - q_j|i + p_i|j - q_i|j)(y_i-y_j).
Physically, the gradient may be interpreted as the resultant force created by a set of springs between map point y_i and all other map points y_j. In addition, in the early stages of the optimization, Gaussian noise is added to the map points after each iteration. Gradually reducing the variance of this noise performs a type of simulated annealing that helps the optimization to escape from poor local minima in the cost function.

## t-Distributed Stochastic Neighbor Embedding

Although SNE constructs reasonably good visualizations, it is hampered by a cost function that is difficult to optimize and by a problem we refer to as the “crowding problem”. The cost function used by t-SNE differs from the one used by SNE in two ways:
* It uses a symmetrized version of SNE cost function
* It uses a student-t distribution rather than gaussian distribution to compute similarity between two points in the low dimensional space. This helps alleviate both problems.

### Symmetric SNE

instead of applying KL divergence between the conditional probabilities p_i|j and q_i|j, it is also possible to minimize a single KL divergence between joint probability distribution. C = KL(P||Q) = p_ijlog(p_ij|q_ij). The definition of p_ij is exactly the same as SNE used before. However, for defining on high-dimensional space, the model has an drwback in case of outlier. THe outlier would make fairly minimal effect on the cost function and the outlier could literally be placed anywhere on the lower-dimensional space. Hence, we instead define p_ij = (p_i|j+p_j|i)/2n. The main advantage of symmetric SNE is the simpler form of its gradient, which is faster to compute. Symmetric SNE seems to produce maps that are just as good as asymmetric SNE, and sometimes even a little better.

### The Crowding Problem

The area of the two-dimensional map that is available to accommodate moderately distant datapoints will not be nearly large enough compared with the area available to accommodate nearby datapoints. Hence, if we want to model the small distances accurately in the map, most of the point that are at a moderate distance from datapoint i will have to be placed much too far away in the two-dimensional map. This was a major problem faced by SNE and was overcome by t-SNE.

### Mismatched Tails can Compensate for Mismatched Dimensionalities

Since symmetric SNE is actually matching joint probabilities of pairs of datapoints rather than distances, we have a natural way of alleviating the crowding problem as follows. In high dimensional space, we convert distances into probabilities using a Gaussian distribution. In low dimensional map, we can use a probability distribution that has much heavier tails than a Gaussian to convert distances into probabilities. This allows a moderate distance in high distance space to be faithfully modeled by a much laarger distance in the map and, as a result, it eliminates the unwanted attractive forces between map points that represent moderately dissimilar datapoints. In t-SNE, we employ a Student t-distribution with one degree of freedom (which is the same as a Cauchy distribution) as the heavy-tailed distribution in the low-dimensional map. . A theoretical justification for the selection of the Student t-distribution is that it is closely related to the Gaussian distribution, as the Student t-distribution is an infinite mixture of Gaussians. A computationally convenient property is that it is much faster to evaluate the density of a point under a Student t-distribution than under a Gaussian because it does not involve an exponential, even though the Student t-distribution is equivalent to an infinite mixture of Gaussians with different variances.

## Paper link

https://www.jmlr.org/papers/volume9/vandermaaten08a/vandermaaten08a.pdf
