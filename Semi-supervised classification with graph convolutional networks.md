# Semi-supervised classification with graph convolutional networks

The authors present a scalable approach for semi-supervised learning on graph structured data that is based on an efficient variant of CNN which operate directly on graphs. The authors consider a problem of classifying nodes in a graph, where labels are only available for a small subset of nodes.

## Fast approximate convolutions on graphs

H_(l+1) = activation_function(D^(-0.5) * A * D^(0.5) * H_(l) * W_(l))
A is the adjacency matrix + self loops. This is done so that each node includes its own features at its next representaion.
D is the degree matrix of A. Degree matrix is used to normalize nodes with high degrees.

Note that the term [D^(-0.5) * A * D^(0.5)] will always be of size n8n since A is of size n*n. We have the flexibility to decide the size of H_(l) and W_(l). H_(l) is of the shape n*y and W_(l) is of size y*y'.

In this paper, the ReLu function was used as the activation function.

### Spectral graph convolutions

The term [D^(-0.5) * A * D^(0.5)] is k-normalized, since it depends only on nodes that are at maximum K steps away from the central node. The exact mathematics uses the chebyshev approximation and is better explained in the paper.

### Layer-wise linear model

A neural network model based on graph convolutions can therefore be built by stacking multiple convolutional layers, each layer followed by a point-wise non-linearity.

### Computing loss on semi supervised classification

In semi-supervised learning, we assume that the locally connected nodes are likely to share the same label. At the end of the GCN, we obtain a layer with F features and use the softmax activation function. We then evaluate cross entropy error over all labeled examples.

## Simple working of a GCN

THe idea between any GCN layer is composed of 3 steps:
* Aggregate all neighbors
* Use a neural network to encode this into an embedding of size F
* Backpropagation using a loss function such as cross entropy loss and update weights

## Paper link

https://arxiv.org/pdf/1609.02907.pdf
