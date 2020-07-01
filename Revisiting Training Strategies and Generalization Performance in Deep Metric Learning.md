# Revisiting Training Strategies and Generalization Performance in Deep Metric Learning

The authors review various deep metric learning methods and propose a simple, yet effective training regularization to boost the performance of ranking basaed DML methods.

## Training a deep metric learning model

The key components of a DML model can be broken down into 3 different parts:

### Objective Function

The usual objective functions used to train the network model are as follows. The most popular are the ranking based loss functions operating on pairs or triplets. The second is to use cross-entropy optimization which comes under the category of classification based. The last is to use proxy based, where the entire class can be represented as a proxy distribution, and are compared with to compute the loss. Additionally, proxy based approaches help to alleviate the issue of tuple mining which is encountered in ranking-based loss functions.

### Data Sampling

There are two broadly types of samplers, label samplers and embedded samplers. In label samplers, we choose a heuristic based on n Samples per class (SPC-n). In SPC-R, we select b-1 samples, and the last sample is made sure to have the same label as another existing sample. This ensures, that atleast one triplet exists in the batch. In embedded samplers, we try to create batches of diverse data statistics. The criteria used for this include:
* Greedy Coreset Distillation (GC): This criterion finds a batch by iteratively adding samples which maximize the distance from the samples that have been already selected.
* Matching of distance distributions (DDM): DDM aims to preserve the distance distribution of B∗. We randomly select m candidate mini-batches and choose the batch B with smallest Wasserstein distance between normalized distance histograms of B and B∗.
* FRD-Score Matching (FRD): Very similar to the previous approach. The only difference being, that we use frechet distance instead of Wasserstein distance.

### Training parameters, regularization and architecture

* Architecture: In recent literature, mainly 3 architectures are used- GoogLeNet, Inception-BN and ResNet50.
* Weight Decay: Commonly, network optimization is regularized using weight decay/L2 Optimization.
* Embedding dimensionality: This is harder to compare and not justified in many works.
* Data Preprocessing: This definitely changes the entire model weights. Unfortunately, there is no proper comparison between different preprocessing steps.
* Batchsize: Batchsize determines the nature of the gradient updates to the networkHowever, it is commonly not taken into account as a influential factor of variation.
* Advanced DML methodologies: There are many extensions to objective functions, architectures, etc.However, although extensions are highly individual, they still rely on these components.

## Analyzing DML training strategies

### Studying DML parameters and architectures

In order to warrant unbiased comparability, equal and transparent training protocols and model architectures are essential, as even small deviations can result in large deviations in performance.

### Batch sampling impacts DML training

Their study indicates that DML benefits from data diversity in mini-batches, independent of the chosen training objective. This coincides with the general benefit of larger batch sizes. While complex mining strategies may perform better, simple heuristics like SPC-2 are sufficient.

### Comparing DML models

Under the same setup, performance saturates across different methods, contrasting results reported in recent literature. Carefully trained baseline models are able to outperform state-of-the-art approaches which use considerable stronger architectures. Thus, to evaluate the true benefit of proposed contributions, baseline models need to be competitive and implemented under comparable settings.

## Generalization in Deep Metric Learning

The experiments performed by the authors indicate that representation learning under considerable shifts between training and testing distribution is hurt by excessive feature compression, but may benefit from a more densely populated embedding space.

## Rho-regularization for improved generalization

This is their proposed addition to the DML training. Implicitly regularizing the number of directions of significant variance can improve generalization.

## Paper link

https://arxiv.org/pdf/1611.03530.pdf
