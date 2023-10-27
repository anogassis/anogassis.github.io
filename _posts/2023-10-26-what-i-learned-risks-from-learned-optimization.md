---
title: My key takeaways from "Risks from Learned Optimization"
date: 2023-10-26
---

# Why I read the paper

I am currently going through the AI Safety Fundamentals course. I'm currently on section 5, and one of the optional readings that appeared several times listed was "Risks from Learned Optimization". Before taking this course, I had already watched Evan Hubinger's lectures on AI safety available on the Youtube channel "AI Safety Talks". The first of his lectures focusses on his paper, and that already left me wanting to read it. So when I saw it again listed in the AI Safety Fundamentals course I decided to take my time and read the manuscript in its entirety.

## My current limitations

I am not an AI Safety professional. I do aspire to work in this field in the future. At the time of writing, I feel very overwhelmed and have the perception that the entry barriers are incredibly high. I am deeply humbled by the experts in this field.

# What is Mesa-optimization?

One of the main contributions of the paper is the concept of "mesa-optimization". This phenomenon happens when the learned algorithm during training is *itself* an optimizer. If such optimizer is created, there are several safety implications that need to be considered as the safety properties of the *base-optimizer* (the optimizer that trained the neural network) are not guaranteed to be transferred to the *mesa-optimizer*.

## Why *mesa*?

The authors explain that the term *mesa-optimization* was chosen to show that the *mesa-optimizer* is one level below the *base-optimizer*. The word mesa (below) is the opposite of meta (above).
