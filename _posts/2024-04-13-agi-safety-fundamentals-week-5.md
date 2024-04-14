---
layout: post
title: Mechanistic Interpretability - AI Safety Fundamentals - Alignment Course - Week 5
date: 2024-04-13
categories: [AGI Safety Fundamentals, AI Alignment]
---

# Mechanistic Interpretability - Week 5 Resource Notes

## Zoom In: An Introduction to Circuits

The paper makes three core claims:

1. **Features** are the fundamental unit of neural networks. We can think of features as directions in the activation space. One can study features and understand them.

2. **Circuits** are collections of features that are connected by weights. Since features can be understood, it follows that circuits can also be understood.

3. We will find **universal** features and circuits across models and tasks.

### Features

Although neurons are understandable, this does not mean that they are simple or easy to understand. This section provides solid examples that neurons can be understood. The examples are:

1. Curve detectors: these neurons are found in all vision models examined by the authors. These detectors exist in families where each neuron detects the same curve but in different orientations. Taken together they capture all possible orientations.
  1. Supporting evidence:
    1. When one optimizes the input to cause curve detectors to fire reliable, it produces curves.
    2. Using examples from the ImageNet dataset that contains curves also causes these neurons to fire reliably.
    3. Synthetic examples cause the curve detectors to respond to a variety of synthetic curve images.
    4. If an example that causes a neuron to fire is rotated, this neuron gradually stops being activated and the next neuron that corresponds to the new orientation starts firing.
    5. If we look at the circuit that constructs the curve detectors we can extract a curve detection algorithm from the weights.
    6. The neurons in the next layer that uses the information from curve detectors involve curves too.
    7. Once you understand how these detectors are implemented you can implement them by setting the weights manually and reimplement the same curve detection.
2. High-low frequency detectors: these neurons look for a less intuitive type of feature. They look for high-frequency patterns on one side and a low frequency pattern on the other. They also appear in families that look for the same things but in different orientations. Furthermore, they appear to be used in boundary detection, especially when a portion of the image is out of focus.
3. Pose-invariant dog head detector: this is an example of a high-level feature which looks for dog heads in any orientation.
4. Polysemantic neurons: not all neurons are easy to understand as the examples above. The paper also shows examples of polysemantic neurons, which are neurons that fire to different kinds of unrelated inputs. For example, they show a neuron that responds to cat faces, fronts of cars and cat legs.
  1. The hypothesis for the existence of polysemantic neurons is a phenomenon called *superposition* where a circuit spreads a feature across many neurons. This presumably happens to allow the model to *simulate* a larger network with more neurons.

### Circuits

Circuits are sub-graphs of the network that consist of a set of linked features and the weights between them. When we understand the features in a circuit, we can then understand the meaning of the weights between them.

#### Curve detector circuit

The circuit for curve detectors consists of simpler curve and line detectors in earlier layer. In the layer after the curve detectors we can see complex 3D geometry and complex shapes emerging.

When we look at the weights between earlier curve detectors and late curve detectors (which in this case is a 5x5 convolution) we see positive weights arranged like the curve detector. This is interpreted as the curve detector looking for the tangent curves at each point along the curve.

Another important point is that the curve detector circuit is an "equivariant circuit", meaning that the symmetry of the between the weights and the neurons is kept as different neurons look at different orientations.

#### Oriented dog head detection

This circuit is a higher-level vision circuit that spans 4 layers. There is a collection of neurons to detect dog faces oriented to the right and to the left. This mirrored approach is maintained for 3 layers, but then invariant neurons are created!

#### Cars in superposition

There is a car detecting neuron that uses features from the previous layers related to different parts of the car: a window detector, a car body detector and a wheels' detector. These three neurons converge to form a car detector that looks for wheels at the bottom of the image, windows at the top and car bodies in the middle.

What happens in the next layers is interesting: the car feature is spread across many polysemantic neurons. This seems to be deliberate, and this phenomenon is called *superposition*.

Superposition is a way for the network to use fewer neurons and conserving them for more important tasks. As long as the features in polysemantic neurons do not co-occur the model can accurately perform its classification.

### Universality

We now switch to a different type of study mode. Instead of looking at features and circuits *intra-model* we will not look for highly correlated features and circuits across different model performing the same task. I call this *inter-model*.

The paper shows anecdotal evidence that curve detectors and high-low frequency detectors form in a variety of vision model architectures such as AlexNet, InceptionV1, InceptionV3, VGG19 and ResnetV2-50.

## Readings

- [X] [Zoom In: An Introduction to Circuits](https://distill.pub/2020/circuits/zoom-in/)
- [X] [Toy Models of Superposition](https://transformer-circuits.pub/2022/toy_model/index.html)
- [X] [Towards Monosemanticity: Decomposing Language Models With Dictionary Learning](https://transformer-circuits.pub/2023/monosemantic-features/index.html)

## Exercises

### Do the speculative circuits claims hold up?

#### Instructions

This is a brief writing-to-learn exercise, expected to be no more than half a page. It is intended to be less intensive than previous exercises given the intensity of reading this week.

Pick one of the three claims (features, circuits and universality) given in the circuits paper. Then:

Summarize what the claim is in your own words. Explain if you think you might be uncertain what the claim is.
What evidence or arguments support and reject the claim? (this can be from the circuits paper itself, the other resources, or other information you find)

#### Answer

**Universality**

The universality claim states that similar features and circuits will be found across different models and tasks.

I find this claim very powerful because, if true, it could mean that there exists a finite number of features and circuits that can be mapped out and documented. This could lead to the discovery of the fundamental reasoning units that neural networks use and could significantly de-risk catastrophic failures if we can successfully inspect large models with this granular understanding.

The evidence of universality is reasonably strong in vision models, in particular low-level features where different models with different architectures have analogous features such as curve detectors and high-low frequency filters.

One portion of the claim that I have not seen evidence is that similar features will emerge across tasks. This is not trivial for me to visualize, but if the central claim of universality is true, this could indeed be the case.

Overall, I am bullish towards mechanistic interpretability being a major contributor to the AI Alignment problem as this bottom-up approach seems (to me) more scientifically sound than other methods and, if successful, could actually guarantee inner and outer alignment since the network has "nowhere to hide".