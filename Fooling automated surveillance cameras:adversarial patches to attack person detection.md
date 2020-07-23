# Fooling automated surveillance cameras:adversarial patches to attack person detection

In this paper, the authors present an approach to generate adversarial patches to targets with lots of intra-class variety, namely persons. The goal is to generate a patch that is able to successfully hide a person from a person detector.

## Generating adversarial patches against person detectors

The authors suggest an optimisation process (on the image pixels) where they try to find a patch that, on a large dataset, effectively lowers the accuracy of person detection. The loss can be broken down into:
* Non-printability score:- This factor represents how well the colours in our patch can be represented by a common printer.
'''
L_nps = min |p_patch − c_print| (for all patches and colours)
'''
* Total variation score:- This loss makes sure that our optimiser favours an image with smooth colour transitions and prevents noisy images. The score is low if neighbouring pixels are similar, and high if neighbouring pixel are different.
'''
L_tv = sqrt[((p_i,j − p_i+1,j)^2 + (p_i,j − p_i,j+1)^2]
'''
* Objectness score:- This loss is to minimize the object or class score outputted by the detector.

We then use a simple weighted sum to calculate the total loss. These weights are trained using Adam Optimizer.

## Methodology

We need to first run the target person detector over our dataset of images. This yields bounding boxes that show where people occur in the image according to the detector. On a fixed position relative to these bounding boxes, we then apply the current version of our patch to the image under different transformations (which are explained in Section 3.3). The resulting image is then fed (in a batch together with other images) into the detector. We measure the score of the persons that are still detected, which we use to calculate a loss function. Using back propagation over the entire network, the optimiser then changes the pixels in the patch further in order to fool the detector even more.

## Paper link

https://arxiv.org/pdf/1904.08653.pdf
