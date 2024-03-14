---
layout: post
title: AI Safety Fundamentals - Alignment Course - Week 2
date: 2024-03-13
categories: [AGI Safety Fundamentals]
---

# Week 2 Lecture Notes

## What is AI alignment?

### AI Safety

AI Safety is the broad field concerned with reducing AI risks. It can be subdivided in many subfields:
- Alignment: making sure that the AI system does what their creators intended them to do.
  - Cases of misalignment:
    - Image generators that exacerbate stereotypes or are unrealistically diverse.
    - Medical classifiers that look for rulers in the images instead of features that are relevant.
    - Chatbots that tell people what they want to hear vs telling them the truth.
- Moral philosophy: is concerned in identifying what are the "good" intentions that an AI system should have. Determining what is "good" is difficult since we humans can have different values and thus different definitions of what is good.
- Competence: designing AI systems that are competent to perform the task they are designed to do.
  - Cases of failures:
    - Giving dangerous medical advice.
    - House prices wrongly predicted leading to significant financial loss.
- Governance: concerned with making sure that dangerous AI systems are not developed.
- Resilience: essentially building capabilities to better cope with negative AI uses.
- Security: protecting the AI system from attacks.
This subcategorization is only a starting point. Many real problems in AI safety will fall in more than one category.

### AI Alignment

AI alignment is commonly broken into outer and inner alignment.

```
Human Objective → Specified Objective → Learned Objective
         (Outer Alignment)      (Inner Alignment)
```

#### Outer Alignment

*Other terms for outer alignment include: reward misspecification, reward hacking, specification gaming, Goodharting.*

Defining a good reward function that represent the intended objective can be very difficult in complex environments. A misspecified reward function is normally a proxy that correlates with what we want.

#### Inner Alignment

*Other terms for inner alignment include: goal misgeneralization*

Inner alignment is concerned with making sure that the goal the learned policy pursues is aligned with the reward function we established.

## Why AI alignment could be hard with modern deep learning

Key takeaways:

- "Saint" models are likely hard to find by SGD. We're more likely to train "Sycophant" and "Schemer" models.
- A misaligned model is one that competently pursues goals which are at odds with human interests.

## Goal Misgeneralisation: Why Correct Specifications Aren’t Enough For Correct Goals

- Goal Misgeneralization (GMG) happens when the system is capable of carrying out the intended task (the capability generalizes) but instead it pursues a different goal (the goal does not generalize).
- In the example, the blue dot is capable to navigate the environment and visit the spheres. But instead of learning to visit the spheres in the right order, it learns to follow the red dot.

### Other examples of GMG

- In Tree Gridworld the goal is to learn to chop trees sustainably. The agent is capable to chop trees at a given rate but learns to chop trees as fast as possible causing mass deforestation.
- The Gopher LLM was trained to evaluate math expressions with a varying number of unknowns. It is certainly capable of evaluating the expressions, but instead is learns to ask the human questions even when there are no unknowns in the expression.

## Readings

- [X] [What is AI alignment?](https://aisafetyfundamentals.com/blog/what-is-ai-alignment/?_gl=1*1g1dlq*_ga*MTk0NzgwOTgzNC4xNjk2MTg0MDUw*_ga_8W59C8ZY6T*MTcxMDMyMTg0Ny4yNC4xLjE3MTAzMjE4NDguMC4wLjA.)
- [X] [Why AI alignment could be hard with modern deep learning](https://www.cold-takes.com/why-ai-alignment-could-be-hard-with-modern-deep-learning/#how-deep-learning-works-at-a-high-level)
- [X] [Goal Misgeneralisation: Why Correct Specifications Aren’t Enough For Correct Goals](https://deepmindsafetyresearch.medium.com/goal-misgeneralisation-why-correct-specifications-arent-enough-for-correct-goals-cf96ebc60924)