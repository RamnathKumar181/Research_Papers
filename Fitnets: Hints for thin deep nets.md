# Fitnets: Hints for thin deep nets

While depth tends to improve network performances, it also makes gradient-based training more difficult since deeper networks tend to be more non-linear. The recently proposed knowledge distillation approach is aimed at obtaining small and
fast-to-execute models, and it has shown that a student network could imitate the soft output of a larger teacher network or ensemble of networks. The authors proposed a novel approach to train thin and deep networks, called Fitnets, to compress wide and shallower(still deep) networks.

## Knowledge Distillation

We train a student network from the softened output of an ensemble of wider networks, teacher network. The student network not only captures information provided by true labels, but also the finer structure learned by the teacher network. The loss function is the L = H(y_true, P_s) + lambda*H(P_t, P_s). Here, H refers to the cross-entropy and lambda is a tunable parameter. KD is designed such that student networks mimic teacher architectures of similar depth. However, as depth of student network increases, KD training still sudders from the difficulty of optimizing deep nets.

## Hint-based training

A hint is defined as the output of a teacher's hidden layer responsible for guiding the student's process. We choose a hidden layer of the fitnet, the guided layer to learn from teacher's hint layer. We want this guided layer to predict the output of the hint layer. Note that having hints is a form of regularization and thus, the pair hint/guided layer has to be chosen such that the student network is not over-regularized. The deeper we set the guided layer, the less flexibility we give to the network and, therefore, FitNets are more likely to suffer from over-regularization.

## Fitnet stage-wise training

We start from a trained teacher network and a randomly initialized fitnet. We add a regressor parametrized by W_r on top of the FitNet guided layer and train the Fitnet parameters W_Guided up to the guided layer to minimize. Finally, from the pre-trained parameters, we train the parameters of whole FitNet W_s to minimize the loss as stated earlier.

## Relation to curriculum learning

Hint based training with KD can be seen as a particular form of curriculum learning. CL accelerates training convergence as well as potentially improve the model generalization by properly choosing a sequence of training distributions seen by the learner: from simple to more complex ones. Here, they used user-defined heuristics to measure the "simplicity" of an example in a sequence. Furthermore, guidance hints require some prior knowledge of the end-task. Both of these CL learning strategies tend to be problem-specific. In order to promote the learning of more complex examples (examples with lower teacher confidence), we gradually anneal λ during the training with a linear decay. The curriculum can be seen as composed of two stages: first learn intermediate concepts via the hint/guided layer transfer, then train the whole student network jointly, annealing λ, which allows easier examples (on which the teacher is very confident) to initially have a stronger effect, but progressively decreasing their importance as λ decays.

## Paper link

https://arxiv.org/pdf/1412.6550.pdf
