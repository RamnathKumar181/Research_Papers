# Learning Representations by back-propagating errors

The paper's proposes a novel approach for learning in networks. The procedure repeatedly adjusts the weights of the connections in the network so as to minimize a measure in the difference between the actual output vector of the net and the desired output vector. As a result of the weight adjustments, internal hidden units which are not part of the input or output come to represent important features of the task domain, and the regularities in the task are captured by the interactions of these units.

## Network

The total input, xj, to unit j is a linear function of the outputs yj, of the units that are connected to j and of weights wji on these connections. Units can be given biases by introducing an extra input to each unit which always has a 1. The weight on this extra input is called bias and is equivalent to a threshold of the opposite sign. Let us use a simple error function such as mean square error. To minimize E by gradient descent, it is necessary to compute the partial derivative of E wrt each weight in the network. For a given case, the partial derivatives of the error wrt each weight are computed in two passes. The forward pass is used to compute the output. The backward pass is more complicated. We first compute gradient with respect to y (output variable). Then, by chain rule, we compute derivative of E wrt x as follows:
'''
dE/dx = dE/dy * dy/dx
'''
If y is a sigmoid function,then dy/dx = y(1-y). This means that we know how a change in the total input x to an output unit will affect the error. But, this total input is just a linear function of the states of the lower level units and it is also a linear function of the weights on the connections, so it is easy to compute how the error will be effected by changing these states and weights.

'''
dE/dw_ji = dE/dx_j * dx_j/dw_ji = dE/dx_j * y_i
'''
To compute dE/dy, we need to solve the following:
'''
dE/dy_i = dE/dx_j * dx_j/dy_i = dE/dx_j * w_ji
'''
Hence, dE/dy_i is just summation of all dE/dx_j * w_ji.
This basic formula is the basis of the backpropagation algorithm used in neural networks.

## Paper link

https://www.iro.umontreal.ca/~vincentp/ift3395/lectures/backprop_old.pdf
