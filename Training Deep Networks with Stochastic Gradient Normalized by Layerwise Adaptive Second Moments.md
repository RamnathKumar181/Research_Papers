# Training Deep Networks with Stochastic Gradient Normalized by Layerwise Adaptive Second Moments

The paper's motivation is to propose a new optimization method, called NovoGrad. SGD with momentum and Adam are two of the most popular optimization methods. SGD with momentum is the preferred algorithm for computer vision, while Adam is perceived safer and more commonly used for NLP. Moreover, Adam can have its second moment vanish or explode, especially during the initial phase of training. However, the NovoGrad method equally performs well on image classification, speech recognition, machine translation, and language modeling and has strong regularization properties.

## Basics

NovoGrad is a type of stochastic normalized gradient descent:
'''
w_t+1 = w_t - l * g_t/||g_t||
'''
Ignoring the gradient magnitude makes SNGD robut to vanishing and exploding gradients, but will be still be sensitive to "noisy" gradients during the initial training phase. One can improve SNGD by gradient averaging such as Adagrad, Adam, RmsProp. Adam however, does not take the normalization of gradients.
'''
m_t = b1 * m_t-1 + (1-b1) * g_t
v_t = b2 * v_t-1 + (1-b2) * g_t^2
w_t+1 = w_t - l * m_t/ ((v_t)^1/2 + e)
'''


## Layer wise Gradient Normalization

We can try to combine SNGD with layer-wise gradient normalization. Here, we replace g_t with g_t(hat) = g_t^l/||g_t^l|| for layer l. We also define m_t^l and v_t^l.

## Improving Adam Generalization

Adaptive methods like Adam generalize worse than SGD with momentum. Some suggest using Adam only for initial stages, and then switch to SGD. To improve adam regularization, AdamW was proposed which decouples the weight decay d as follows:
'''
w_t+1 = w_t - l * [m_t/ ((v_t)^1/2 + e) + d * w_t]
'''

## Reduction of Adam Memory Footprint

Unfortunately, since, we might need to store the second moments for all layers, the memory required will be very large and almost impossible for very deep networks. Instead, they proposed an AdaFactor model which replaced the full second moment with moving averages of the row and column sums of squared gradients.

## NovoGrad Algorithm

NovoGrad combines three ideas: (1) use layer-wise second moments, (2) compute first moment with gradients normalized with layer-wise second moments,
(3) decouple weight decay. The exact math is a bit different, but all the properties are conserved. Note, that the final updation happens more like the SGD than the Adam algorithm. Also note that, NovoGrad uses a learning rate between SGD and Adam.

## Paper link

https://arxiv.org/pdf/1905.11286.pdf
