---
layout: post
title: AI Safety Fundamentals - Alignment Course - Week 4
date: 2024-03-31
categories: [AGI Safety Fundamentals, AI Alignment]
---

# Week 4 Resource Notes

## Can we scale human feedback for complex AI tasks?

- It is hard to give accurate feedback to complex tasks. So we need some technique to be able to give good feedback to system of increasing capability. This is called scalable oversight because it would allow us humans to continue to provide effective oversight to AI systems that surpass our capabilities in all possible tasks.
- **Task decomposition**: in task decomposition the goal is to take a given complex task and keep breaking it down into smaller and smaller pieces until these pieces are easy enough for humans to judge and provide feedback. This does not seem to be a very active area of research according to the article because breaking down complex task can be very difficult to break down all possible problems into smaller and smaller pieces. Techniques in the field of task decomposition include:
    - **Iterated amplification**: this is essentially what is described above. Take one problem and break it down into smaller pieces. An example is the work by OpenAI to summarize books. You can start by summarizing every page, then every chapter then the whole book.
    - **Iterated distillation and amplification**: this adds a distillation step that can be used to then train more capable systems. For example, in the book summarization task, we can then take the final summary and create a new dataset that maps `the whole book --> summary`.
    - **Recursive reward modelling**: in this case, we allow humans with access to an AI model to provide the feedback. This sounds life amplification to me, since the capability of the human is "amplified" by having access to a model. We use this improved feedback to train a better reward model to then train a better AI model, then repeat. This seems to be an active area with OpenAI and DeepMind.
- **Constinutional AI**: we already discussed this in Week 3.
- **Debate**: here we two AI models debating on a given topic. The AIs take turns and with each response try to further cement their position while also pointing out flaws in the counterargument being presented by the other AI. At the end of the debate a human reviews the history and determines which AI gets a reward. Humans could also intervene and provide either feedback or questions during the debate. This approach has a few problems:
    - **Models can collude**: models can cooperate and mislead the human into thinking that they are debating to further a common goal. For example, gaining more compute.
    - **Cases of irreducible complexity**: some arguments might be strong but also complex, relying on counter-intuitive facts. In these cases the correct argument may be too complex and not rewarded correctly by the human.
- **Weak-to-strong generalization**: use weaker systems to provide oversight to stronger, more capable systems. This involves using a smaller but aligned model to provide feedback to a stronger but unaligned model. Think of an aligned version of GPT-2 providing feedback to the pre-trained version of GPT-4. OpenAI is currently exploring this approach.

## Supervising strong learners by amplifying weak experts

- In Iterated Amplification we have a human $H$ with access to several copies of a model $M$ performing a complex task. The setup of $H + nM$ is denoted $Amplify^H(M)$. *Note*: the paper calls the model $X$ instead of $M$.
- $Amplify^H(M)$ provides the training signal to the later version of M, $\{M_1, M_2, ..., M_n\}$ so that M becomes increasingly more capable. I expect the role of the human to become increasingly smaller as M becomes more capable. At the limit, can this become $Amplify^M(M)$? In other words, can the model use and coordinate other copies of itself?

## Readings

- [X] [Can we scale human feedback for complex AI tasks?](https://aisafetyfundamentals.com/blog/scalable-oversight-intro/?_gl=1*1e5ifox*_ga*MTk0NzgwOTgzNC4xNjk2MTg0MDUw)
- [X] [Supervising strong learners by amplifying weak experts](https://arxiv.org/pdf/1810.08575.pdf)
- [X] []()
- [X] []()


## Week 4 - Exercises

