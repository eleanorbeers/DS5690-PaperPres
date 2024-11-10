# "Emergent Abilities" observed in LLMs

## Presentation Details

**Paper Link:** https://arxiv.org/pdf/2206.07682

**Title:** "Emergent Abilities of Large Language Models"

**Date:** August, 2022

**Authors:** Jason Wei, Yi Tay, Rishi Bommasani, Colin Raffel, Barret Zoph, Sebastian Borgeaud, Dani Yogatama, Maarten Bosma, Denny Zhou, Donald Metzler, Ed H. Chi, Tatsunori Hashimoto, Oriol Vinyals, Percy Liang, Jeff Dean, William Fedus

**Presenter:** Eleanor Beers

## Overview

### Introduction

While small language models continue to grow in popularity due to their efficiency and ability to be deployed on mobile devices with minimal computational resources, certain capabilities remain exclusive to large language models (LLMs). The immense scale of LLMs enables them to exhibit results that smaller models cannot achieve. Wei et al. refer to these unique capabilities as "emergent abilities". As we will explore further, this phenomenon is unpredictable: at certain scales, model performance experiences sudden, exponential improvements. However, since emergent abilities are a function of scale alone, they cannot be observed simply by proportionally scaling smaller models. Although current LLMs have reached unprecedented sizes, the findings in this paper raise intriguing questions: Could even greater scale reveal additional emergent abilities? Do the benefits of such a vast scale outweigh the potential risks? And ultimately, what do these emergent abilities mean for the future potential of small language models?

### Problem

Wei et al. identify and coin a new phenomenon in the field of NLP: emergent abilities in large language models. The authors formally define this concept as follows:

*An ability is emergent if it is not present in smaller models but is present in larger models.*

Studying and testing this phenomenon is challenging because it does not occur at smaller scales. Additionally, scaling performance curves have shown an unpredictable trajectory that only shifts at a very large scale threshold, known as the phase transition. Simply observing this phenomenon requires substantial computational resources. Understanding why this randomness occurs at smaller scales and predicting where the threshold exists is an even more complicated problem. This paper, however, focuses on documenting the issue and making these observations, leaving room for further investigations into the mechanisms behind the performance curves, scale, and the phenomenon of emergent abilities itself.

## Methodology and Key Findings

### Approach

As aformentioned, the authors did not set out to unveil any causes behind this phenomenon, but rather to prove its existence in a variety of contexts and provide reason for further investigation. Thus, their approach is less methodical than an experimental design but far more expanisive in its reach.

To properly investigate the phenomenon, the researchers had to define the two key variables of the phenomenon: what is "scale" in the context of emergent abilities (indepedent variable) and how can we define and measure peformance (dependent variable)?

Traditionally, model scale can be defined by three factors: computational resources, number of model parameters, and the size of the model's training dataset. In the context of emergent abilities, the most important scaling factor is pure compute. This is the factor that the authors primarily refer to when discussing scale. They use FLOPs (floating point operations per second) to measure computing scale. In their visualizations, FLOPs is represented on the X-axis, as it is the hypothesized independent vairable at play in this relationship (an increase in FLOP will correspond to an increase in peformance past a certain threshold). However, the authors also include a note about model parameters: since increased FLOPs and more model parameters typically go hand in hand, the curve of model performance and number of model parameters is very similar to that of FLOPs and model performance. However, they do not include the size of the training dataset in any of their analysis, as many LLM families have a fixed training dataset size for differeing sizes of the model that would not allow for them to properly investigate the relationship behind the concept of "emergent abilities". Despite excluding training dastaset size and primarily focusing on compute, the researchers admit that a more thorough investigation of the phenomenon might consider emergent abilities as a function of all aspects of scale, not just model size or compute.

To test "performance" of the models, they measure quality of responses to few-shot prompting: a prompting technique that provides a language model with a few input-output pairs as context for its output. They include the following example:

<img width="321" alt="Screenshot 2024-11-10 at 11 47 06 AM" src="https://github.com/user-attachments/assets/7a5c8a4c-1310-4402-bd67-68f30f8cd631">

### Findings

## Insights, Impacts, and Next Steps

### Critical Analysis

### Impact

### Future Directions

### Limitations and Potential Extensions

## Citation
[citation]




