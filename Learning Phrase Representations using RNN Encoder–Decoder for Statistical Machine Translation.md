# Learning Phrase Representations using RNN Encoder–Decoder for Statistical Machine Translation

The paper successfully proposes a novel neural network model called the RNN Encoder-Decoder for phase based statistical machine translation system.

## RNN

An RNN has a hidden unit h and an output y. It operates on a variable sized input x. At each step, the hidden unit is updated based on its previous value and current input. It learns to predict the next symbol in a sequence. In this case, we need a conditional probability of word t occuring given the previous t-1 words.

## RNN Encoder-Decoder

The encoder is an RNN that reads each symbol of an input sequence x sequentially. This updates the hidden state at each step. At the end, the hidden state acts as a summary of the entire sequence. The decoder is also an RNN which predicts the next symbol given the hidden state. The only difference being that the the predicted symbol and the hidden state also depend on the previous symbol. The entire net is trained to maximize log likelihood of the translation given a sequence input.  The given network can be used in two ways:
* Generate a target sequence given an input sequence
* Score a given pair of input and output sequence, where score is simply p(y|x)

## Hidden Unit that Adaptively Remembers and Forgets

They also proposed a new type of hidden unit. This hidden unit is motivated by the LSTM but is much simpler to compute. The idea is that, the reset gate and the update gate are learned over the iterations. When the reset gate is close to 0, the hidden state is forced to ignore the previous hidden state and reset with current input only. On the other hand, the update gate controls how much information from the previous hidden state will carry over. The intuition here is similar to LSTM. As each hiddent unit has seperate reset and update gates, each unit will learn to capture dependencies of different time scales.

## Paper link

https://arxiv.org/pdf/1406.1078.pdf
