---
title: My notes from "Risks from Learned Optimization"
date: 2023-11-01
---

# Why I read the paper

I am currently going through the AI Safety Fundamentals course. I'm currently on section 5, and one of the optional readings that appeared several times listed was "Risks from Learned Optimization". Before taking this course, I had already watched Evan Hubinger's lectures on AI safety available on the YouTube channel "AI Safety Talks". The first of his lectures focuses on this paper, and that already left me wanting to read it. So when I saw it again listed in the AI Safety Fundamentals course I decided to take my time and read the manuscript in its entirety. What follows is a mixture of notes, summaries and questions I have about the manuscript. I enjoyed reading the manuscript and feel that it was worth my time and effort.

## My current limitations

I am not an AI Safety professional, but I do aspire to work in this field in the future. At the time of writing, I feel very overwhelmed and have the perception that the entry barriers are incredibly high. I am deeply humbled by the experts in this field. I took me around 10 hours to go through the whole paper and probably another 10 hours to put these notes together.

# What is Mesa-optimization?

One of the main contributions of the paper is the concept of "mesa-optimization". This phenomenon happens when the learned algorithm during training is *itself* an optimizer. If such optimizer is created, there are several safety implications that need to be considered as the safety properties of the *base-optimizer* (the optimizer that trained the neural network) are not guaranteed to be transferred to the *mesa-optimizer*.

## Why *mesa*?

The authors explain that the term *mesa-optimization* was chosen to show that the *mesa-optimizer* is one level below the *base-optimizer*. The word mesa (below) is the opposite of meta (above).

# Questions the paper tries to answer

The paper focuses on exploring two different questions:

1. The circumstances that may lead to mesa-optimization, i.e. when will the learned algorithm be an optimizer?
2. What will be the objective of the mesa-optimizer and can you align it?

# Base optimizers and mesa-optimizers

The *base optimizer* is typically based on a gradient-descent-based process with the goal of training a model to achieve a task. The base optimizer has a base objective that is used to search and select among possible models. If the model found by the base optimizer is itself an optimizer, then this is the *mesa-optimizer*.

IMPORTANT: The optimization carried by the mesa-optimizer is instrumentally useful for achieving its objective.

The *mesa-objective* is the criterion used by the mesa-optimizer to select the model output. Because the mesa-objective is not specified by the programmers, it can open a gap between the base and mesa-objectives. This gap can have significant safety implications in cases where the mesa-objective performs well in training but may have behaviors that are not intended in deployment.

When training is completed and the mesa-optimizer has selected a learned algorithm, its outputs do not depend on the base objective.

INSERT FIGURE 1 FROM THE PAPER HERE

# The inner and outer alignment problems

The *inner alignment problem* can be though of as eliminating the gap between the base objective and the mesa-objective. On the other hand, the *outer alignment problem* is the elimination of the gap between the base objective and the intended goal of the programmers.

An easy way to understand this is to think that the outer alignment problem is the alignment gap between the "system and the humans outside of it", and the inner alignment is the alignment gap between the mesa-objective and the loss function.

IMPORTANT: If mesa-optimizers can be prevented, then solving the inner alignment problem may prove to not be necessary in order to have safe and capable advanced AI systems. BUT, if this is not the case, a solution to both alignment problems is necessary.

## Robust alignment vs. pseudo-alignment

A mesa-optimizer is said to be *robustly aligned* when the mesa-objective agrees with the base objective across distributions. A *pseudo-aligned* mesa-optimizer agrees with the mesa-objective only in the training distribution, i.e. it appears to be aligned in training, but given a distributional shift in future data outside of training the model will not agree with the base-objective anymore.

The main issue with pseudo-alignment is that it open the possibility for advanced AI systems to competently perform other actions to achieve goals that are not the ones originally intended by the programmers.

## Mesa optimization as a safety problem

Given a pseudo-aligned agent, two safety problems are explored:

1. Unintended optimization: To start with, it is scary to think that ML systems can implement powerful optimization algorithms when they are not intended by the programmers. In the real world this can be dangerous if the objective functions and optimization procedures generalize well.

2. Inner alignment: Even in cases where you accept that your system to finds an optimization algorithm, i.e. it's okay to have a mesa-optimizer, you need to make sure it is robustly alignment with the base objective. Otherwise, it may optimize for something entirely different.

# Conditions for mesa-optimization

The conditions for mesa-optimization are currently theoretical and may occur in AI systems that are more advanced than the ones we currently have. There are two components in an ML system that can influence whether mesa-optimization will occur.

1. The task: this includes the training distribution and the function of the base objective.
2. The base optimizer: this includes both the model architecture and the base optimizer.

## The task

The following conditions are presented:

### Better generalization through search

If, in order to achieve good performance in an environment, some degree of optimizer is required to find a good policy, then you might get a mesa-optimizer.

If you think about a total optimization budget, there are two potential ways of how optimization can be performed: (a) the base optimizer expends it to select the learned algorithm or (b) the learned algorithm expends optimization budget to select an action.

The authors provide a simple yet powerful model to demonstrate that, as environments get more and more diverse, mesa-optimization will become more and more attractive:

$$x^* = \argmax_x \frac{P-f(x)}{N} + x$$

Where $P$ is the optimization power applied by the base optimizer, $f(x)$ is the total amoung of optimization power needed to get a learned algorithm capable of performing that amount of optimization, $N$ is the number of task instances, $x$ is the amount of optimization the learned algorithm can do at runtime and $x^*$ is the total optimization power applies to each task instance.

The main takeaways of the equation is that as the environment becomes more diverse, i.e. $N$ increases, $x$ dominates and mesa-optimization becomes more and more favorable.

### Compression of complex policies

Base optmizers are biased to select learned algorithms with lower complexity. However, some task require very complex policies in order to achieve good performance. Thus, the base optimizer will be incentivized to select highly compressed policies and a mesa-optimizer is an example of a highly compressed policy form the perspective of the base optimizer. It saves the base optimizer the trouble of encoding all of the details of the policy it needs to implement and instead it only needs to encode hoe to find the aforementioned policy.

### Task restriction and human modeling

Since the odds of getting a mesa-optimizer increase with the more diverse environments are, one way to prevent mesa-optimization is to train AI systems on highly restrictive tasks.

Additionally, tasks that don't require modelling humans are less likely to produce mesa-optimizers. The reason for this is that humans are often optimizers and reasoning about humans will likely require reasoning about optimization.

## The base optimizer

It is likely that the model architecture will influence the probability of getting a mesa-optimizer. Some of the factors that can contribute are:

### Reachability

*Reachability* refers to how difficult it is for a base optimizer to find a given learned algorithm.

In order for the base optimizer to produce a mesa-optimizer, it needs (1) to perform well on the objective and (2) be reachable. Now, if we consider that most base optimizers work by performing local optimization, it follow that a mesa-optimizer can only be produced if there is a path across the model space that allows local search to find it, i.e. the path should monotonizally increase.

### Model capacity

As model capacity grows, so does the space of possible learned algorithms. Thus, if the base optimizer has an incentive to find mesa-optimizers, it will be more likely to find one in a broader space. It seems intuitive that for a given model capacity, the base optimizer should try to find the learned algorithms that provide the best possible performance (the authors use "squeeze out" as much performance as possible). If this is true, the base optimizer will be biased towards compressed policies.

### Inductive biases

Simplicity biases are dangerous because the more the base optimizer is biased to find simple policies, the more it will be incentivized to find compressed policies, i.e. mesa-optimizers.

The base optimizer can also be biased towards either low time complexity or low space complexity.
- Penalizing description length favors mesa-optimizers;
- Penalizing time complexity disfavors them.

IMPORTANT: "neither a minimal-depth nor minimal size boolean circuit that solve a problem can be a mesa-optimizer".

### Statefulness

If a learned algorithm can recall past information in its history it won't need to perform all the computations when it produces its output. This decreases the penalty on time complexity and thus favors mesa-optimizers.

NOTE: I found cool the extreme example that of a hypothetical model that is able to store its state across time steps **and** across episodes.

### Hard-coded optimization

One way to counter the issues above is to explicitly include a hard-coded optimization algorithm. The better the explicit optimization the less need for implicit optimization. An example is hard-coded Monte Carlo tree search.

# The inner alignment problem






