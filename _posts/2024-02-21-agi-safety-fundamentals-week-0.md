---
layout: post
title: AGI Safety Fundamentals - Week 0
date: 2024-02-21
categories: [AGI Safety Fundamentals]
---

# Week 0 Lecture Notes

## Intro to Large Language Models

- Llama 2 70B used 10TB of text, 6000 GPUs for 12 days, costing ~$2M and using ~1e24 FLOPS.
- Training runs of SOTA models runs in tens to hundreds of millions of dollars.
- Neural Nets are empirical artifacts that require sofisticated evaluations to work with these models.
- Pre-training is about acquiring knowledge. Fine-tunning is about alignment. RLHF further fine-tunes the model based on labelled comparisons.
- LLMs can be used to automate labelling.
- The next word prediction accuracy of LLMs is highly predictable based on:
  - The number of model parameters
  - The number of dimensions
- This accuracy is correlated with real word performance in tasks we care about.
- LLMs can be augmented by equipping them with tool use.
- Multimodality [audio, images, video, text] is the new frontier.
- There is excitment to give LLMs system 2 thinking.
- How to achieve self-improvement in language?
- Think of LLMs as the kernel for an emerging LLM OS, a new computing stack.
- LLM security attacks (just a few of many):
  - Jailbreak
  - Prompt injection
  - Data poisoning
  - There will be a cat and mouse race to discover new attacks

## Compute Trends Across Three Eras of Machine Learning

- Training compute for ML models has been doubling every 6 months.
  - 10B times since 2010.
- Three eras of compute:
  - Pre Deep Learning Era:
    - Compute grows slowly roughly following Moore's Law.
    - Period of 1952 through 2010.
    - Doubling time of 18 months.
  - Deep Learning Era:
    - Compute grows faster.
    - Period of 2010 through 2022.
    - 6-month doubling time.
  - Large-Scale Era:
    - New large scale models that are 100 to 1000x larger than the previous era.
    - Starts in 2015.
    - Doubling time of 10 months.
  - 

## Readings

- [X] [[1hr Talk] Intro to Large Language Models](https://www.youtube.com/watch?v=zjkBMFhNj_g)
- [X] [Compute Trends Across Three Eras of Machine Learning]([link-to-reading-2](https://epochai.org/blog/compute-trends))
- [ ] [Title of Reading 3](link-to-reading-3)

## Exercises

- [ ] Exercise 1: Description of Exercise 1
- [ ] Exercise 2: Description of Exercise 2
- [ ] Exercise 3: Description of Exercise 3

## Additional Notes
