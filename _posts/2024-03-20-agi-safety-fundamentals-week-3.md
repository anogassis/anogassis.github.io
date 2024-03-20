---
layout: post
title: AI Safety Fundamentals - Alignment Course - Week 3
date: 2024-03-20
categories: [AGI Safety Fundamentals]
---

# Week 3 Lecture Notes

## Illustrating Reinforcement Learning from Human Feedback (RLHF)

There are at least 3 ingredients necessary to train a model with RLHF:

1. A pre-trained model (or fine-tuned model)
2. A reward model trained to predict human preferences
3. Fine-tuning the pre-trained model with RL

For brevity, I will skip the process for #1.

## Training a reward model to predict human preferences

**Goal:** train a model that takes in a sequence of text and outputs a scalar value corresponding to the human preference.

Reward models are often also a language model (LM)

**Training procedure:** Prompts are passed to the pre-trained model and responses are generated. For example, one prompt can be used to generate multiple responses. These prompt-generation(s) pairs are then ranked by human annotators. Often this is done by using two responses and selecting the best one. This creates an Elo rating by ranking models and outputs against each other. The rankings are then normalized to give a scalar reward signal and a language model is trained to predict these rankings.

It seems that the RM is typically much smaller than the pre-trained model by orders of magnitude.

## Fine-tuning with RL

Framing the task as an RL problem:

The **policy** is the LM that takes in a prompt and generates a response. The **action space** are all the possible tokens this policy can generate. This corresponds to the entire vocabulary of the model (normally 50 to 100k tokens). The **observation space** is the distribution of possible input tokens. Finally, the **reward function** is a mixture of the RM and some constraint on policy shift.

Proximal Policy Optimization ([PPO](https://huggingface.co/blog/deep-rl-ppo)) has been used successfully for this fine-tuning step.

```
(1) Input tokens --> policy --> generated response

(2) Input + response --> Reward model --> scalar on "preferability"

(3) Per token probability distributions (initial model vs policy) --> KL divergence

(4) "preferability" - KL divergence = Reward
```







## Readings

- [ ] [Illustrating Reinforcement Learning from Human Feedback (RLHF)](https://huggingface.co/blog/rlhf)

# Week 3 - Exercises
