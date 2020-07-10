# How transferable are features in deep neural networks?

In this paper the authors experimentally quantify the generality versus specificity of neurons in each layer of a deep convolutional neural network and report a few surprising results. Transferability is negatively affected by two distinct issues: (1) the specialization of higher layer neurons to their original task at the expense of performance on the target task, which was expected, and (2) optimization difficulties related to splitting networks between co-adapted neurons, which was not expected. Modern deep neural networks exhibit a curious phenomenon: when trained on images, they all tend to learn first-layer features that resemble either Gabor filters or color blobs. When the target dataset is significantly smaller than the base dataset, transfer learning can be a powerful tool to enable training a large target network without overfitting. If the target dataset is small and the number of parameters is large, fine-tuning may result in overfitting, so the features are often left frozen. On the other hand, if the target dataset is large or the number of parameters is small, so that overfitting is not a problem, then the base features can be fine-tuned to the new task to improve performance. Of course, if the target dataset is very large, there would be little need to transfer because the lower level filters could just be learned from scratch on the target dataset.

## Generality vs. Specificity Measured as Transfer Performance

In this study, we define the degree of generality of a set of features learned on task A as the extent to which the features can be used for another task B. Because finding these standard features on the first layer seems to occur regardless of the exact cost function and natural image dataset, we call these first-layer features general. On the other hand, we know that the features computed by the last layer of a trained network must depend greatly on the chosen dataset and task. We thus call the last-layer features specific.

## Similar Datasets: Random A/B splits

The experiments shows that lower-layer features also learn on the target dataset, performance is similar to the base case. On AnB task, the top layers show the best transferability compared to the bottom. In AnB+, transferring features and then fine-tuning them results in networks that generalize better than those trained directly on the target dataset in some cases.

## Dissimilar Datasets: Splitting Man-made and Natural Classes Into Separate Datasets

The effectiveness of feature transfer is expected to decline as the base and target tasks become less similar.

## Random Weights

Another paper had claimed that the combination of random convolutional filters, rectification, pooling, and local normalization can work almost as well as learned features on shallow neural networks. The authors further proved that the transferability gap when using frozen features grows more quickly as n increases for dissimilar tasks (hexagons) than similar tasks. One possible reason this latter result may differ from the previous paper mentioned, is the fact that their model did not overfit on the dataset.

## Paper link

http://papers.nips.cc/paper/5347-how-transferable-are-features-in-deep-neural-networks.pdf
