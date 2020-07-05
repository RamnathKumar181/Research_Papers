# On the variance of the adaptive learning rate and beyond

The paper's motivation is to depict a problem faced by the Adam optimizer and try to address it. Adam usually experiences problematically large variance in the early stage of training. They introduce a new novel optimizer called the Rectified Adam (RAdam), which caters to this issue. It has been observed that these optimization methods may converge to bad/suspicious local optima, and have to resort to a warmup heuristic – using a small learning rate in the first few epochs of training to mitigate such problem.

## Variance of the adaptive learning rate

Due to the lack of samples in the early stage, the adaptive learning rate has an undesirably large variance, which leads to suspicious/bad local optima. Getting large enough samples prevents the gradient distribution from being distorted. The exact proof is given in the paper.

## Rectified Adaptive Learning Rate

We use a rectification term in the weight updation process. Specifically, when the length of the approximated SMA is less or equal than 4, the variance of the adaptive learning rate is intractable and the adaptive learning rate is inactivated. Otherwise, we calculate the variance rectification term and update parameters with the adaptive learning rate. The exact proof is better explained in the paper.

## Paper link

https://arxiv.org/pdf/1908.03265.pdf
