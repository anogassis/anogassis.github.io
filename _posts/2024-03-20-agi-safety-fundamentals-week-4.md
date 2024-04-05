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

## Weak-to-strong generalization: Eliciting Strong Capabilities With Weak Supervision 

### Questions

- How can weak supervisors control models much smarter than them?
- Can we use weak models to supervise strong models?

### Findings

1. Strong models generalize beyond the capabilities of weak models.
2. This is more complicated than just naively fine-tuning on the weak supervision.
3. The authors think improving weak-to-strong generalization is tractable.

### Setup

1. Create a weak supervisor: small pretrained models are fine-tuned on ground truth labels. The paper uses GPT-2 as a weak supervisor.
2. Train the strong student model: finetune the larger model, in this case GPT-4, using labels generated by the weak supervisor.
3. Train the strong model on the ground truth labels: this is done to show the ceiling of performance that can be achieved.

The ideal scenario would be that using weak-to-strong generalization achieves the same performance as directly training the strong model on the ground truth. This is obviously not the case as we will see.

### Tasks evaluated

Three tasks were evaluated in the paper:

1. **Natural language benchmarks**: 22 popular natural language benchmarks were used. All datasets were converted into binary classification tasks.
2. **Chess puzzles**: on a given state of the chess board, predict the best next possible move.
3. **ChatGPT reward modeling**: Given a dialog $d$, two possible completions for the last question from the human $c_1$ and $c_2$ and a ground truth label of for the preferred completion $y$, predict $y$.

### Results

#### Naive training on weak labels

- Mixed results.
- In NLP benchmarks: 20% of the performance gap is recovered.
- In chess puzzles: it depends on the strong model size. Larger models recover less performance.
- ChatGPT reward modelling: poor by default.

#### Bootstrapping with intermediate model sizes

In this setup, instead of making straight jump from weak to strong models, the process is bootstrapped using intermediate model sizes.

Concretely, they used a setup with two intermediate model sizes. The training looks like this:

```
Model_0 --> weak_labels_0 --> Model_1
Model_1 --> weak_labels_1 --> Model_2
Model_2 --> weak_labels_2 --> Strong_Model
```

- Results in the chess puzzles were promising.
- Only small improvements in NLP tasks.
- No improvements in the RM task.

#### Auxiliary loss helps

Naively fine-tuning on the labels of the weak supervisor has one main failure mode: the strong model learns to imitate the weak model. This is obviously not desirable.

The real goal of weak-to-strong generalization is for the strong model to understand the intent of the weak supervisor but not repeat its mistakes.

To prevent this imitating behavior, the paper implements an additional loss term which reinforces the strong model's in its predictions even when they disagree with the labels generated by the weak supervisor.

- In the NLP tasks, the auxiliary loss helps when the compute gap between the weak and strong models is very large. With the smallest weak model and the largest strong model the performance gap recovery jumps from 25% to 80%.
- Generalization in the NLP tasks also improve dramatically, getting almost perfect generalization in many datasets.
- The auxiliary loss also reduces imitation behavior of weak errors.

## Readings

- [X] [Can we scale human feedback for complex AI tasks?](https://aisafetyfundamentals.com/blog/scalable-oversight-intro/?_gl=1*1e5ifox*_ga*MTk0NzgwOTgzNC4xNjk2MTg0MDUw)
- [X] [Supervising strong learners by amplifying weak experts](https://arxiv.org/pdf/1810.08575.pdf)
- [X] [AI safety via debate](https://arxiv.org/pdf/1805.00899.pdf)
- [X] [Weak-to-strong generalization: Eliciting Strong Capabilities With Weak Supervision ](https://arxiv.org/pdf/2312.09390.pdf)