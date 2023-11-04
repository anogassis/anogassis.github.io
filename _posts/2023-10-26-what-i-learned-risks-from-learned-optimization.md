---
title: My notes from "Risks from Learned Optimization"
date: 2023-11-01
---

# Why I read the paper

I am currently going through the AI Safety Fundamentals course. I'm currently on section 5, and one of the optional readings that appeared several times listed was "Risks from Learned Optimization". Before taking this course, I had already watched Evan Hubinger's lectures on AI safety available on the YouTube channel "AI Safety Talks". The first of his lectures focuses on his paper, and that already left me wanting to read it. So when I saw it again listed in the AI Safety Fundamentals course I decided to take my time and read the manuscript in its entirety. What follows is a mixture of notes, summaries and questions I have about the manuscript.

## My current limitations

I am not an AI Safety professional, but I do aspire to work in this field in the future. At the time of writing, I feel very overwhelmed and have the perception that the entry barriers are incredibly high. I am deeply humbled by the experts in this field.

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





