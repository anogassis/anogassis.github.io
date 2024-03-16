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

# Week 2 - Exercises

## Identifying uncertainties

### Instructions:

Spend ~30 minutes answering the question: What are my key uncertainties about the alignment problem?

You might want to consider:

- Are there any 'obvious' potential solutions to AI safety that come to mind? (We'd encourage brainstorming a long list first, before trying to argue about them)
- How likely do you think it is that human-level machine intelligence arises in the next 10 years? What about 100 years?
- Do you think AI systems that we build will actually pursue convergent instrumental goals (mentioned at 13:16 in Intro to AI safety)? Why and why not?
- Will AI systems be safe by default? Why and why not?
- What might be some real-world consequences of misalignment?
- Will we have one big AI system? Many copies of the same powerful AI? Lots of different AI systems?
- Who's intentions or which "values" should we be aligning AI systems with? How would you handle different stakeholders wanting to align AI systems with different intentions or values?
​
In particular, if you're convinced one way on a particular topic, we'd encourage really digging into the opposite argument. You're also encouraged to browse the optional resources (below), or do your own research to help fill in key gaps in your understanding.

### Answer (written in 30 minutes):

#### Epistemic Status

I have been studying alignment for a relatively shot period of time compared of about 1 year or so. I became more interested in it after the release of GPT-3.5, the original model of ChatGPT.

Most of my initial exposure to the alignment problem was through the Lex Friedman podcast where I listened to the interviews of [Max Tegmark](https://lexfridman.com/max-tegmark-3/) and [Eliezer Yudkowsky](https://lexfridman.com/eliezer-yudkowsky/). More recently, I finished reading [The Precipice](https://80000hours.org/the-precipice/) which assigns the risk of an existential catastrophe due to unaligned AI in the next 100 year as 1 in 6. I have also watched most of [Rob Miles'](https://www.youtube.com/@RobertMilesAI) videos, watched Evan Hubinger's [AI Safety Talks](https://www.youtube.com/watch?v=NmDRFwRczVQ) and gone through most of the material of last year's curriculum of the AI Safety Fundamentals from BlueDot Impact (which I am currently retaking with a cohort of students). Thus, it is fair to say that I am biased towards the "doomer" and X-risk side of the debate. I have also not spent enough time looking at the counterarguments on this debate. I have watched a debate between [Eliezer Yudkowsky and George Hotz](https://www.youtube.com/watch?v=6yQEA18C-XI) and very recently listened to Lex Fridman's interview of [Yann LeCun](https://lexfridman.com/yann-lecun-3/) which is probably the best articulated counterargument I have been currently exposed to.

#### A messy explanation of my current view

Currently, I think that human-level AI, AGI and super AGI represent a risk unlike any other risk humanity has faced in the past. I find the current empirical evidence on misalignment related to goal misgeneralization and specification gaming strong examples that we currently do not know how to properly specify good objectives for AI systems even for simple agents. I also find, in general, that the thought experiments and scenarios described by "doomers" very plausible.

All that being sad, here are some things that currently bother me on the Alignment Problem:

- We don't have a good test bed to evaluate AGI because we don't have AGI.
- Interpreting the trained models and the training procedure of even simple models seem to be very hard. We currently have to play with very small (models) toy examples.
- Is it possible for humans to truly control super-intelligence? Every time I think of this I only see failure happening.
- How far can scaling of autoregressive models go? Is it possible that these models will reach a capability that is truly dangerous?
  - Yann LeCun believes that autoregressive models are not enough to achieve AGI.
- If the training procedure is the problem, then we have to find a replacement to SGD.
  - If in the model space there is only one aligned model and many proxy-aligned models, how should the training procedure look like to ensure the aligned model is selected?

## Case Study - Variable generalization performance of a deep learning model to detect pneumonia in chest radiographs: A cross-sectional study

[LINK](https://journals.plos.org/plosmedicine/article?id=10.1371/journal.pmed.1002683#sec026)

### Summary of discussion (generated by GPT-4):

- Pneumonia-screening CNNs trained on data from different hospitals failed to generalize across external sites and did not base predictions solely on pathology. This challenges the rapid deployment of deep learning in radiological imaging without extensive real-world testing.
- The study revealed CNNs could predict pneumonia based on hospital-specific indicators rather than underlying pathology, indicating poor generalization and reliance on confounding factors like image acquisition and processing differences.
- Deep learning in medicine faces challenges due to the vast number of parameters in models, complicating the identification of specific prediction drivers and traditional concepts of model overfitting. Practices to ensure model transparency and reproducibility clash with deep learning's complexity.
- Even tailor-made CNNs for single-site use may not mitigate confounding variables, as differences in equipment and practices within a hospital can bias predictions, underscoring the need for extensive external testing.
- Adapting CNN architectures for radiological imaging to preserve high-resolution data and domain-specific information could improve model robustness, reducing reliance on confounding factors.
- Model performance varied between internal and external test sets, influenced by data construction, clinical data characteristics, and potentially confounding variables, highlighting the complexity of generalizing deep learning models in medicine.
- Confounding factors specific to medical practices may enable models to generalize well but limit their clinical applicability, emphasizing the need for careful clinical question framing and extensive real-world testing of CNN-based diagnostic systems.
- The study's limitations include the inability to fully assess factors behind hospital-specific model biases and the influence of differing patient populations and diagnostic criteria across datasets, as well as the need to consider patient history and clinical presentation in diagnoses.

### Questions

1. What do you think the human-level intended outcome for the system was?
The human-level intended outcome was to create the pneumonia-screening system that would learn the pathology of the patients and categorize them based on the pathology. This would allow the system to generalize well across different sites.
2. What was the goal specified to the model?
To categorize whether a given radiograph had pneumonia.
3. What did the model actually do?
The model learned confounding variables not related to pathology. It predicted pneumonia based on hospital-specific indicators, not pneumonia.
4. Is this outer or inner misalignment?
To me this is inner misalignment because the system learned to identify hospitals and not the pathology of pneumonia.
5. Only if outer: What flaw in the reward signal is being exploited? Why does this achieve the goal specified, but not the human-level outcome?
6. Only if inner: What change in distribution occurred between training and deployment? (anthropomorphising the policy here) What learned goal does the model appear to pursue when deployed?
Changes in image quality, procedure, markings of origin. The model appears to try to identify the site that performed the radiograph.
8. Does this failure have any traits that are similar to a scheming or sycophantic model? (the answer will be no for some case studies!)
No.