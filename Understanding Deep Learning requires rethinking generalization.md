# Understanding Deep Learning requires rethinking generalization

The paper's motivation is to understand what distinguishes neural networks that generalize well from those that don't.

## Fitting random labels and pixels
The conclusion they reached was that deep neural networks could easily fit random variables. This implies that the capacity of the neural networks is sufficient for memorizing the entire dataset. For example, In tasks such as Imagenet, our model can perfectly fit them even when we destroy the relations between images and the labels. We previously thought that the network was learning abstractions between classes, and if it had to memorize every single example, that would take much longer to converge. However, our assumption may be false. Memorization takes just as long as learning relationships.

## The role of Regularization

### Expicit Regularization

The conclusion reached was that augmenting data shows a more significant generalization performance than weight decay. Also, the model architecture seems to play a more critical role in generalization when compared to regularization. The above two conclusions imply that explicit regularization may improve generalization, but this is neither necessary nor by itself sufficient.

### Implicit Regularization

Early stopping could potentially improve generalization, but this is not always the case. Furthermore, the authors also pointed out that, though we do not apply batch normalization as a regularizer method, the operation does seem to improve generalization performance. The authors conclude that regularizers could help improve generalization performance. However, it is unlikely that regularizers are the fundamental reason for generalization! When training a model on a vast dataset, the researchers previously believed that regularizers limit the parameter values, thus helping generalization and reduce overfitting. However, this paper proves that the regularization only plays a small role in learning, and is inherent in the model itself. This suggests that learning is not dependant on the regularization techniques.

## Finite-Sample expressivity

The authors extend the Universal Approximation Theorem and suggest that a two-layer network can represent any function as long as few conditions hold. However, we also know that given infinite data, higher depth models usually perform better than the shallow counterparts.
The authors also prove that the stochastic gradient descent converges to the minimum L2 norm solution, which is an interesting analysis. This would suggest that the SGD is like an implicit regularization technique! However, the minimum norm does not imply anything about generalization performance.
The authors also mentioned that optimization continues to be easy even when generalization is poor. This was very surprising since researchers thought that there was an inherent connection between how easy we can find a solution and how good the solution is. They found that some models could converge very quickly on the training set but perform poorly, and others may converge very slowly but perform very well. They concluded by saying that traditional measures of model complexity struggle to explain the generalization of large neural networks.
With this, the paper concludes, raising various significant problems with neural networks and encouraging other researchers to participate in the discussed open problems!

## Paper link

https://arxiv.org/pdf/1611.03530.pdf
