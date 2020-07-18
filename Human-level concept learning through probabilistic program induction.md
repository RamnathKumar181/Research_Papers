# Human-level concept learning through probabilistic program induction

Despite recent advances in artificial intelligence and machine learning, two aspects of human conceptual learning have always eluded machine systems. For one, people can learn new concepts from just one or a handful of examples. Secondly, people learn richer representations than machines do, even for simple concepts unlike machines. The paper raises a few important concerns: How do people learn new concepts from just one or a few examples? And how do
people learn such abstract, rich, and flexible representations? An even greater challenge arises when putting them together. This paper also introduces the Bayesian program learning (BPL) framework, capable of learning a large class of visual concepts from just a single example and generalizing in ways that are mostly indistinguishable from people.

## Bayesian Program Learning

The BPL approach learns simple stochastic programs to represent concepts, building them compositionally from parts, subparts, and spatial relations. The joint distribution on types y, a set of M tokens of that type q(1) , . . ., q(M), and the corresponding binary images I(1) , . . ., I(M) factors as:
'''
P(y,q(1),...q(M),I(1),...,I(M)) = p(y) ∏ p(I(m)|q(m))p(q(m)|y) (for all m)
'''
This is a simple bayes application which can be easily proved. This concept was particulary applied on handwritten characters. Note that these tokens are generated using another code and not readily availble in our data.


## Inference

Although successful on these tasks, BPL still sees less structure in visual concepts than people do. It lacks explicit knowledge of the general environment. Furthermore, capturing how people learn all these concepts at the level the authors reached with handwritten characters is a long-term goal.

## Paper link

http://clm.utexas.edu/compjclub/wp-content/uploads/2016/02/lake2015.pdf
