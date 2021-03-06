# Meta-graph: Few shot link prediction via meta learning

The authors propose a novel approach to predict missing edges across multiple graphs using only a small sample of known edges. The general problem assumes that we have to perform link-completion on a single large graph and that this rgaph is relatively complete (atleast 50% of edges are already known). Here, we face a problem with multiple graphs with only a few true edges known. Specifically, they consider a distribution over graphs as the distribution over tasks from which a global set of parameters are learnt, and we deploy this strategy to train graph neural networks that are capable few-shot link prediction. To further improve fast adaptiation to new graphs, they also introduced a graph signature function, which learns how to map the structure of an input graph to an effective initialization point for a GNN link prediction model.

## Introduction

### Graphs

G = (V,E), where V is set of nodes and E is set of edges. Denote an edge going from node u to v where u,v belong to nodes, and (u,v) belongs to edges.
A simple graph is a graph which has at most one edge between each pair of nodes.
In multi-relational graphs, there is different types of edges. We would need to define an adjacency matrix per edge type. Defined in the format (u,t,v), where u and v are nodes and t is edge type. e.g. heterogeneous graphs.

### Tasks

Machine learning tasks on graphs include:
* Node classification: Classify nodes as labels
* Link prediction: Extrapolate new edges
* Clustering and community detection: In previous two tasks, we assume, that there is some missing information (prior assumption). However, in this task, we assume all the information is already available. The only goal is here to form clusters in this graph.
* Graph classification, regression, and clustering: We have multiple graphs in this task.

## Relationship to standard link prediction

* Rather than learning from a single graph, this learns from multiple graphs sampled from a common distribution or domain.
* Access to a very sparse sample of true edges.
* Distinguish between global parameters (used to encode knowledge about underlying distribution) and local parameters (optimized to perform link prediction on a specific graph G). This allows us to consider leveraging information from multiple graphs, while still allowing for individually-tuned link prediction models on eaach specific graph.

## Relationship to traditional meta learning

Traditional meta learning assumes a distribution over classification tasks, with the goal of learninng global parameters that can facilitate fast adaptation with few examples. Here, we consider a distribution p(G) over graphs with the goal of performing link prediction on a newly sampled graph.

## Local link prediction model

Variational graph autoencoders was used as the base link prediction framework. Formally, given a graph, the VGAE learns an inference model q, that defines a distribution over node embeddings. These node embedding can be used to score the likelihood of an edge existing between pairs of nodes. The GNN allows us to learn the parameters of the normal distribution (specifically, the mean and the variance of the distribution). The generative component VGAE allows us to create a new graph where the likelihood of an edge existing between two nodes is proportional to the dot product of their node embeddings. The inference GNNs can be trained to minimize the variational lower bound on the training data.

## Graph signature

We pass the data through the GCN. We obtain a matrix of dimentions (n*E), where n is number of nodes and E is size of embedding. We then apply an aggregate over the rows to get an vector of size E. We send the same data to 4 different fully connected layers. The outputs gamma_1, beta_1, gamma_2, beta_2. The gamma_1 and beta_1 are sent to the first GCN, whereas the others are sent to the second GCN. We use the formula [Wh * gamma + beta].

## VGAE

In the second GCN layer, we get two outputs. One to obtain mean, and other to compute variance. The same signature values are used for both. We use reparametrization to obtain an embedding. The inner product between two inner nodes are used to determine whether an edge exists between them or not.

## Overview of meta-graph

* Global initialization, theta that is used to initialize all the parameters of the GNNs in the inference model. They are optimized via second-order gradient descent to provide an effective initialization point for any graph sampled from the distribution p(G).
* A graph signature s_G is used to modulate the parameters of inference model based on the history of training graphs. In particular, we assume that the inference model for each graph G_i can be conditioned on the graph signature.

## Paper link

https://arxiv.org/pdf/1912.09867.pdf
