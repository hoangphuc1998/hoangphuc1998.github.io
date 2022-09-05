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

{{< figure src="/imgs/machine-learning/variational_inference/dag_example.png" align="center" numbered="true" >}}

Normally, the joint distribution of these 3 variables can be written as:
$$P(a,b,c)=P(c|a,b)P(a,b)=P(c|a,b)P(b|a)P(a)$$

But as you can see in the figure above, we can say that variables $a$ and $b$ are independent because there is no "direct" edge from $b$ to $a$ and vice versa. We can simplified the joint distribution $P(a,b,c)$ as:
$$P(a,b,c)=P(c|a,b)P(b)P(a)$$

**In a more general case**, let's consider the joint distribution of $N$ variables $x_1,x_2,...,x_N$:
$$P(x_1,x_2,...,x_N)=P(x_1)P(x_2|x_1)...P(x_N|x_{N-1}...x_1)$$

Given a graphical model $G=(V,E)$ represents this joint distribution, with $V$ is the set of vertices (or nodes) of $N$ random variables $x_1, x_2, ..., x_N$ and $E$ is the set of edges (or links) between these vertices. Without loss of generality, we assume that a node can only have links from lower number nodes. 

Then we can simplify each conditional probability in the right hand side by $P(x_i|x_{Pa_i})$, with $Pa_i$ is the set of direct parents of node $i$ (if exists a link *from* node $j$ *to* node $i$ then $j\in A_i$), and remove everything else in the condition.
### Observed and latent variables
A variable in graphical model can be either observed or unobserved (latent variable) while we're doing inference. Observed varibles are like the evidence that we accounted for and latent variables are query nodes that we need to infer. In graphical model language, observed variables are denoted by gray color nodes:

{{< figure src="/imgs/machine-learning/variational_inference/observed_variable.png" caption="Annotations for observed variable $x$ and latent variable $z$" align="center">}}
### Example
Now, take a look at the simple and familiar spam email classification example for clarification of what we have gone through about graphical models:
- Suppose we have a dataset of $N$ emails, which have labels $y_i$ ($i=1..N$), each will denote whether that email is spam or not.
- Each email is a bag-of-word over $M$ words in the vocabulary. The words per email are represented by $x_{ij}$ ($i=1..N, j=1..M$).
- We define the model parameters $z=(z_1, z_2,...,z_M)$. To simplify the problem, we restrict the $z$s that those can only take 3 values $-1, 0$ and $+1$.

{{< figure src="/imgs/machine-learning/variational_inference/spam_email.png" caption="Graphical model for simple spam email classification example" align="center" numbered="true" >}}
The square box is called plate notation. Every varibles in the box are replicated and all these variable are independent of each other.

This graphical model will represent the joint distribution of spam email classification problem:
$$
\begin{aligned}
P(x, y, z) &= \prod^N_{i=1}\prod^M_{j=1}P(y_i|x_{ij}, z_i)P(x_{ij}|z_i)P(z_i) \\\\\\
&= \prod^N_{i=1}\prod^M_{j=1}P(y_i|x_{ij}, z_i)P(x_{ij})P(z_i)
\end{aligned}
$$
In this problem, we observe the dataset $\mathcal{D}$ which include all variables $x_{ij}$ and $y_i$. The objective is to "learn" the latent variables $z$ from this dataset. In other words, we need to calculate the posterior $P(z|\mathcal{D})$. This leads to the need to do inference in graphical models.

### Inference in Graphical Models
Given a graphical model, **inference is the task to find the posterior distribution $P(z|x)$**, with $z$ is a set of latent variables and $x$ is a set of observed variables. Based on Bayes' theorem, this posterior distribution can be expressed as:
$$P(z|x)=\frac{P(x|z)P(z)}{P(x)}$$

### Why inference is hard?
- Multidimensionality
- Example
- Sampling techniques
- Advantages and disadvantages of sampling techniques
## Inference as an optimization problem

## Optimizing Evidence Lower Bound objective
## Example: Topic modeling with Linear Discriminant Analysis (LDA)

## Reference
- CS228: Probabilistic Graphical Models of Stanford University [https://ermongroup.github.io/cs228-notes](https://ermongroup.github.io/cs228-notes)