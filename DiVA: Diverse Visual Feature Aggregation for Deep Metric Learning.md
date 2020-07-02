# DiVA: Diverse Visual Feature Aggregation for Deep Metric Learning

The motivation of this paper is to study the combination of various losses in the DML setting.

## Fitting random labels and pixels
The conclusion they reached was that deep neural networks could easily fit random variables. This implies that the capacity of the neural networks is sufficient for memorizing the entire dataset. For example, In tasks such as Imagenet, our model can perfectly fit them even when we destroy the relations between images and the labels. We previously thought that the network was learning abstractions between classes, and if it had to memorize every single example, that would take much longer to converge. However, our assumption may be false. Memorization takes just as long as learning relationships.

## Model

In this paper, the authors used the simple triplet loss to create embeddings of images. However, as we are interested in generalizing to unknown test distributions, we should rather aim at maximizing the amount of features captured from the training set, thereby increasing the potential of embedding space to transfer to unseen images.

### Class-discriminative features

These features are learned by standard class-discriminative optimization of φ and focus on data characteristics which allow to accurately separate one class from all others. We do this using average of triplet losses.

### Class-shared features

This feature is common between different classes. For instance, birds and cars share a similar variety in colors, which are of little help when separating between them. However, to learn about this characteristic is actually beneficial, when describing other colorful object classes like flowers or fish. We do this using triplet loss again. The only difference being, that the positive label is now a sample which has similar features as the anchor, regardless of which class it falls in.

### Intra-class features

Intra-class features describe variations within a given class. While these variations may also apply to other classes (thus exhibiting a certain overlap with class-shared features), more class-specific details are targeted. Here, y_a = y_p = y_n.

### Sample-specific features

They also applied Contarstive loss, to capture sample specific features.

## Improved generalization by multi feature learning

The authors propose to combine all these different features to train the model. The loss is defined in terms of L = l1 + w2l2+ ... - term. This term is to minimize mutual information. The exact math describing the exact loss function is available in the paper.

## Paper link

https://arxiv.org/pdf/1611.03530.pdf
