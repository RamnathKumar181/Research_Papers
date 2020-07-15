# Grad-CAM: Visual Explanations from Deep Networks via Gradient-based Localization

The paper's proposes a novel approach for producing ‘visual explanations’ for decisions from a large class of Convolutional Neural Network (CNN)-based models, making them more transparent and explainable. Gradient-weighted Class Activation Mapping (Grad-CAM), uses the gradients of any target concept flowing into the final convolutional layer to produce a coarse localization map highlighting the important regions in the image for predicting the concept.

## What makes a good visual explanation?

Pixel-space gradient visualizations such as Guided Backpropagation and Deconvolution are high-resolution and highlight fine-grained details in the image, but are not class-discriminative. In contrast, localization approaches like CAM or our proposed method Gradient-weighted Class Activation Mapping (Grad-CAM), are highly class-discriminative (the ‘cat’ explanation exclusively highlights the ‘cat’ regions but not ‘dog’ regions). In order to combine the best of both worlds, we show that it is possible to fuse existing pixel-space gradient visualizations with Grad-CAM to create Guided Grad-CAM visualizations
that are both high-resolution and class-discriminative.

## Grad-CAM

CAM produces a localization map for an image classification CNN with a specific kind of architecture where global average pooled convolutional feature maps are fed directly into softmax. While Grad-CAM is class-discriminative and localizes relevant image regions, it lacks the ability to highlight fine-
grained details like pixel-space gradient visualization methods. In order to combine the best aspects of both, we fuse Guided Backpropagation and Grad-CAM visualizations via element-wise multiplication. in order to obtain the class-discriminative localization map Grad-CAM L_Grad-CAM ∈ R_u×v of width u
and height v for any class c, we first compute the gradient of the score for class c, y_c (before the softmax), with respect to feature map activations A_k of a convolutional layer. The exact computation amounts to successive matrix products of the weight matrices and the gradient with respect to activation functions till the final convolution layer that the gradients are being propagated to. Hence, this weight α_ck represents a partial linearization of the deep network downstream from A, and captures the ‘importance’ of feature map k for a target class c.
The exact math behind this approach is better explained in the paper.

## Paper link

https://arxiv.org/pdf/1610.02391.pdf
