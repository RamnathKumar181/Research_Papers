# Small-GAN: Speeding up GAN training using core-sets

It has previously been studied that training with larger batches yield better results when compared to smaller batches. However, the training on harder batches require very high computational power. Since, such a model is impractical, the authors tried to achieve the same using smaller batches. This experiment was performed on the GAN, and hence, the name. The idea is to extract a smaller batch which mimics the coverage of the larger batch.

## Some Important Terms

### Inception score and Frechet Inception Distance

The FID is used to measure the effectiveness of an image synthesis model. This score is derived from using a pre-trained Imagenet classifier. Hence, the name.

### Core set Selection

A core set Q, of a set P is a subset Q belongs to P, that approximates the 'shape' of P.

## Sampling Distributions

Sampling from the prior is relatively simple. We can assume the prior distribution to be an uniform distribution. We do have the freedom to do so as well, so no issues here.

Sampling from the target distribution is more tricky. Taking pairwise distance might not work due to high concentration of images. Furthermore, simple metrics such as eucledian distance do not work as they lack any semantic significance. To avoid these issues, they created Inception embeddings of their data. They projected these embeddings on lower dimensions and applied eucledian pairwise distance to this set. The previous step further reduces the time taken computationally. We can then apply core-set sampling to these representations to select images. Once, we obtain the core-set, we need to apply the inverse embedding function to obtain the original image as well.

The process is task agnostic and could be applied to any variant of GAN (or any similar neural network in my opinion).

## Paper link

https://arxiv.org/pdf/1910.13540
