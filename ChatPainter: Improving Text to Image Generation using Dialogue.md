# ChatPainter: Improving Text to Image Generation using Dialogue

Generating images from captions alone has been a prior work. However, captions might not be informative enough to capture the entire image and insufficient for the model to be able to understand which objects in the images correspond to which captions. Add a dialogue that further describes a scene leads to a significant improvement in the performance. This task is fairly simpler for an image with only one object. However, it is way harder for datasets such as MS COCO where there are multiple objects and these objects need not be centred.

## Model

The model is built upon the StackGAN model. StackGAN generates an image in two stages where Stage-I generates a coarse 64*64 image and Stage-II generates a refined 256*256 image. Before training either, we need to create dialogue embeddings. This can be done in 2 ways:
* Non-recurrent encoder: The entire dialogue is collapsed into a single string and encoded with a pre-trained Skip-Thought encoder.
* Recurrent encoder: They generate Skip-Thought vectors for each turn of the fialogue and then encode them with a bidirectional LSTM-RNN.
The caption and dialogue embeddings are then concatenated using the Conditional Augmentation (CA) module.

### Stage-I

The Stage-I generator upsamples the input representation to a W_o*H_o image. The Stage-I image expected to be a blurry and rough version of the final one. The discriminator downsamples this image.

### Stage-II

In case of recurrent dialogue encoder, the RNN weights are copied from Stage-I and kept fixed. The model details is kept the same as that of original StackGAN.

### Training details

Similar to StackGAN, the authors use a matching-aware discriminator, that is trained using "real" pairs consisting of a real image together with matching caption and dialogue, and "fake" pairs that consist either of a real image together with another image's caption and dialogue or a generated image with the corresponding caption and dialogue.

## Paper link

https://arxiv.org/pdf/1802.08216.pdf
