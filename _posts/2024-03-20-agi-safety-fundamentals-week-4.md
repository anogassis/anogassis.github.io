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

## AI safety via debate

### Setup

The debate is run as a game where the AIs take turns in a question-answering game.

1. A question is shown to both AIs
2. Each of the AIs state their answers up front.
3. They take turns making statements to support their answer or point flaws to their opponent's statements.
4. A judge reviews the entire debate $(question, answers, statements)$
5. This is a zero-sum game.

### Claims

- **Central claim**: In a debate game it is harder to lie than to refute a lie.
  - In other words, if one of the AIs lie, it is easier for the other AI to call you out.
- Both AIs try to tell the truth in the most convincing way possible.
- Training is stable.
- The AIs will be as strong as AIs trained without any safety measures.

### We can use short debates

Debates don't need to be super long. Instead, debates can be short and focus on a single line of argument (the strongest and best argument). This way we don't have to explore the entire debate tree, and can simply explore one path in the tree.

### The good

- Agents can admit ignorance and get rewarded by doing so.
- Agents try their hardest to tell the truth and are penalized for misleading statements.
- It is sufficient to point out just *one* flaw in the opponent's argument, there is no need to disprove everything.

### The bad

- Humans may reward agents that say what they want to hear.
- Humans might not be able to understand all debates and judge them correctly.
- Training via debate requires additional model capacity.
- Deception remains an issue.

## Readings

- [X] [Can we scale human feedback for complex AI tasks?](https://aisafetyfundamentals.com/blog/scalable-oversight-intro/?_gl=1*1e5ifox*_ga*MTk0NzgwOTgzNC4xNjk2MTg0MDUw)
- [X] [Supervising strong learners by amplifying weak experts](https://arxiv.org/pdf/1810.08575.pdf)
- [X] [AI safety via debate](https://arxiv.org/pdf/1805.00899.pdf)
- [X] []()


## Week 4 - Exercises

Many RM that are trained in the same preference data but with different HPs. Build an ensemble of models. You use averages of the weights, not the predictions. More efficient than calling the predictions many times. It leads to robustness. Reward hacking. Performance gets better in the beginning. But it doesn't work as much in the test data. WARM is more robust to distributional shift.