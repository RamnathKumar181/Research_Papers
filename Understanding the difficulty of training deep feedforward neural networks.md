# Understanding the difficulty of training deep feedforward neural networks

The paper's objective is to understand better why standard gradient descent from random initialization is doing so poorly with deep neural networks, to better understand these recent relative successes and help design better algorithms in the future. Recent work with deep architectures shows that even with very large training sets or online learning, initialization from unsupervised pre-training yields substantial improvement, which does not vanish as the number of training examples increases.

## Effect of Activation Functions and Saturation During Training

### Experiments with the Sigmoid

The authors noticed that all the sigmoid activation values of the last hidden layer are pushed to their lower saturation value of 0. Inversely, the others layers have a mean activation value that is above 0.5, and decreasing as we go from the output layer to the input layer. This kind of saturation can last very long in deeper networks with sigmoid activations. The big surprise is that for intermediate number of hidden layers, the saturation regime may be escaped. At the same time that the top hidden layer moves out of saturation, the first hidden layer begins to saturate and therefore to stabilize. Note that deep networks with sigmoids but initialized from unsupervised pre-training (e.g. from RBMs) do not suffer from this saturation behavior. The logistic
layer output softmax(b + W h) might initially rely more on its biases b (which are learned very quickly) than on the top hidden activations h derived from the input image (because h would vary in ways that are not predictive of y, maybe correlated mostly with other and possibly more dominant variations of x). Thus the error gradient would tend to push W h towards 0, which can be achieved by pushing h towards 0. In the case of symmetric activation functions
like the hyperbolic tangent and the softsign, sitting around 0 is good because it allows gradients to flow backwards. However, pushing the sigmoid outputs to 0 would bring them into a saturation regime which would prevent gradients to flow backward and prevent the lower layers from learning useful features. Eventually but slowly, the lower layers move toward more useful features and the top hidden layer then moves out of the saturation regime.

### Experiments with the Hyperbolic tangent

The hyperbolic tangent networks do not suffer from the kind of saturation behavior of the top hidden layer observed with sigmoid networks, because of its
symmetry around 0. However, we still observe the saturation phenomenon and the reason is yet to be understood.

### Experiments with the Softsign

The softsign x/(1+|x|) is similar to the hyperbolic tangent but might behave differently in terms of saturation because of its smoother asymptotes. The saturation is faster at the beginning and then slow, and all layers move together towards larger weights.

## Studying Gradients and their Propagation
### Effect of the Cost Function

We found that the plateaus in the training criterion (as a function of the parameters) are less present with the log-likelihood cost function. There are clearly more severe plateaus with the quadratic cost.

### Gradients at initialization

Previous studies found that back-propagated gradients were smaller as one moves from the output layer towards the input layer, just after initialization. He studied networks with linear activation at each layer, finding that the variance of the back-propagated gradients decreases as we go backwards in the network. We can see that the variance of the gradient on the weights is the same for all layers, but the variance of the backpropagated gradient might still vanish or explode as we consider deeper networks. The normalization factor may therefore be important when initializing deep networks because of the multiplicative effect through layers. What is really surprising is that even when the back-propagated gradients become smaller (standard ini-
tialization), the variance of the weights gradients is roughly constant across layers.

## Findings and Conclusions

The more classical neural networks with sigmoid or hyperbolic tangent units and standard initialization fare rather poorly, converging more slowly and apparently towards ultimately poorer local minima. The softsign networks seem to be more robust to the initialization procedure than the tanh networks, presumably because of their gentler non-linearity. For tanh networks, the proposed normalized initialization can be quite helpful, presumably because the
layer-to-layer transformations maintain magnitudes of activations (flowing upward) and gradients (flowing backward). Sigmoid activations (not symmetric around 0) should be avoided when initializing from small random weights, because they yield poor learning dynamics, with initial saturation of the top hidden layer.

## Paper link

http://proceedings.mlr.press/v9/glorot10a/glorot10a.pdf?source=post_page---------------------------
