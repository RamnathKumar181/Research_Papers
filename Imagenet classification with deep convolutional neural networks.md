# Imagenet classification with deep convolutional neural networks

The paper proposes a novel approach using deep CNN on the imagenet task. They also use the ReLU activation instead of tanh or softmax since, ReLU is a non-saturating linearity unlike tanh and softmax. Furthermore, ReLU is also faster to train in comparison.

## Local Response Normalization

ReLUs have the desirable property that they do not require input normalization to prevent them from saturating. If at least some training examples produce a positive input to a ReLU, learning will happen in that neuron. However, the authors found out that the local normalization scheme aids generalization.

## Overlapping Pooling

Pooling layers in CNNs summarize the outputs of neighboring groups of neurons in the same kernel map. Traditionally, the neighborhoods summarized by adjacent pooling units do not overlap. A pooling layer can be thought of as consisting of a grid of pooling units spaced s pixels apart, each summarizing a neighborhood of size z × z centered at the location of the pooling unit. If we set s = z, we obtain traditional local pooling as commonly employed in CNNs.

## Reducing Overfitting

Due to the sheer number of parameters, there is a very high probability of overfitting. To combat this, the authors used various methods in parallel, including data augmentation and dropout.

## Paper link

http://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks.pdf
