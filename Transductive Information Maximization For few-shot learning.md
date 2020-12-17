# Transductive Information Maximization For few-shot learning

The authors propose a novel approach that maximizes the mutual information between the query features and their label prediction for a given few-shot task.

## Few shot learning

Ina few-shot learning setting, a model is first trained on labeled data with base classes. Then, model generalization is evaluated on few-shot tasks, composed of unlabeled samples from novel classes unseen during training (query set), assuming only one or few labeled samples (the support set) are given per novel class.

## Transductive inference

In the transductive setting, the model classifies the unlabeled query examples of a single few-shot task at once, instead of one sample at a time as in inductive methods.

## Transductive Information Maximization

Let f denote the encoder or feature extractor function. The encoder is first trained on the base training set X_base using the standard cross entropy loss, without any meta training. Then, for each specific few shot task, we propose to minimize a mutual information defined over the query samples. Now for each single few-shot task, we introduced our empirical weighted mutual information between the query samples and their latent variables, which integrates two terms:
* Empirical (Monte Carlo) estimate of the conditional entropy of labels given the query raw features.
* Empirical label-marginal entropy.
We set the loss as lambda*CE - I, where CE is cross entropy loss.

### Conditional Entropy H(Y|X)

Aims at minimizing the uncertainty of the posteriors at unlabeled query samples, thereby encouraging the model to output confident predictions.

### Label-marginal entropy regularizer H(Y)

Encourages the marginal distribution of labels to be uniform, thereby avoiding degenerate solutions obtained when solely minimizing conditional entropy. Hence, it is highly important as it removes the need for implicit regularization, as mentioned in earlier.

## Optimization

The authors propose two methods for optimization such as:
* Gradient Descent
* Alternating Direction Method of Multipliers

For both methods:
* The pre-trained features is kept  fixed. Only the weights W are optimized for each task. Overall and interestingly, fine-tuning only classifier weights W, while fixing feature-extractor parameters yield the best performances for our mutual information loss.
* For each task, weights are initialized as the cross prototypes of the support set

### Gradient Descent (TIM-GD)

A straightforward way to minimize our loss is to perform gradient descent on W.

### Alternating direction method (TIM-ADM)

This training scheme yields substantial speedups in transductive learning, while maintaining the high levels of accuracy of TIM-GD.  

## Paper link

https://arxiv.org/pdf/2008.11297.pdf
