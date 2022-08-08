---
title: "Variational Inference"
# weight: 1
# aliases: ["/first"]
tags: ["statistics", "generative-models"]
date: "2022-06-26"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: true
draft: false
hidemeta: false
comments: false
description: ""
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
# math: true
categories: ["machine-learning"]
# url: /machine-learning/variational_inference
editPost:
    URL: "https://github.com/hoangphuc1998/hoangphuc1998.github.io/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---
While I was reading about generative models, I did not know a thing about 
## What is Bayesian inference?
### Bayesian networks
(In this post, I will only talk about inference in Bayesian network, but the idea remains the same when applying to general Probabilistic Graphical Models)

First of all, it is good to know what is a Bayesian network. A Bayesian network is a **directed acyclic graph** (DAG) that represents the joint probability of a set of random variables. The vertices of the graph represent random variables while the edges express the dependencies between them. To understand what this means, take a look at this easy Bayesian network with 3 random variables $a, b$ and $c$: 
![Simple DAG of joint probability](/imgs/machine-learning/variational_inference/dag_example.png#center)
Normally, the joint distribution of these 3 variables can be written as:
$$P(a,b,c)=P(c|a,b)P(a,b)=P(c|a,b)P(b|a)P(a)$$

But as you can see in the figure above, we can say that variables $a$ and $b$ are independent because there is no "direct" edge from $b$ to $a$ and vice versa. We can simplified the joint distribution $P(a,b,c)$ as:
$$P(a,b,c)=P(c|a,b)P(b)P(a)$$

**In a more general case**, let's consider the joint distribution of $N$ variables $x_1,x_2,...,x_N$:
$$P(x_1,x_2,...,x_N)=P(x_1)P(x_2|x_1)...P(x_N|x_{N-1}...x_1)$$

Given a graphical model $G=(V,E)$ represents this joint distribution, with $V$ is the set of vertices (or nodes) of $N$ random variables $x_1, x_2, ..., x_N$ and $E$ is the set of edges (or links) between these vertices. Without loss of generality, we assume that a node can only have links from lower number nodes. 

Then we can simplify each conditional probability in the right hand side by $P(x_i|x_{A_i})$, with $A_i$ is the set of direct parent of node $i$ (if exists a link *from* node $j$ *to* node $i$ then $j\in A_i$), and remove everything else in the condition.
### Observed and latent variables
- Two questions:
    - Marginal inference
    - Maximum a posteriori
- Example:
### Why inference is hard?
- Multidimensionality
- Example
- Sampling techniques
- Advantages and disadvantages of sampling techniques
## Inference as Optimization problem

## Reference
- CS228: Probabilistic Graphical Models of Stanford University [https://ermongroup.github.io/cs228-notes](https://ermongroup.github.io/cs228-notes)