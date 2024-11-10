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

As aforementioned, the authors did not aim to uncover the underlying causes of emergent abilities but instead set out to establish their existence across various contexts and highlight the need for further research. Their approach, therefore, is less of a controlled experimental design and more exploratory, casting a wider net to capture instances of emergent abilities.

To properly investigate this phenomenon, the researchers first had to define the two core variables at play: how to measure scale (independent variable) in the context of emergent abilities and how to define and evaluate performance (dependent variable) effectively.

In traditional NLP research, model scale is commonly defined by three factors: computational resources, the number of model parameters, and the size of the model’s training dataset. Here, the authors focus primarily on compute (measured in FLOPs, or floating point operations per second) as the key measure of scale, with FLOPs placed on the X-axis in their visualizations. The hypothesis is that compute acts as the independent variable, where an increase in FLOPs will lead to an increase in performance after a certain threshold is crossed. Although FLOPs are the primary scale indicator, the authors note the strong correlation between compute and model parameters; typically, as models require more FLOPs, they also have more parameters. Thus, the performance curve in relation to model parameters often mirrors the FLOPs-based curve. However, they exclude training dataset size from their analysis since many language model (LLM) families maintain a fixed dataset size across varying model sizes, making it challenging to isolate its effects on emergent abilities. The researchers acknowledge that a more comprehensive investigation might consider emergent abilities as a function of multiple scaling aspects, beyond just compute and model size.

To measure model performance, the authors rely on few-shot prompting, a technique where the model is provided with a small number of input-output examples to guide its response. An example prompt might look like this:

<img width="321" alt="Screenshot 2024-11-10 at 11 47 06 AM" src="https://github.com/user-attachments/assets/7a5c8a4c-1310-4402-bd67-68f30f8cd631">

Performance is then typically assessed in terms of accuracy, though the specific performance metric varies depending on the task. For example, in a word unscramble task, exact match percentage is used, as the objective is for the model to produce the exact correct word. In contrast, accuracy is used for arithmetic tasks, where the model’s ability to solve problems correctly is the primary focus.

To demonstrate the widespread nature of emergent abilities, the researchers tested various well-known models, including LaMDA, GPT-3, Gopher, Chinchilla, and PaLM, on prompts such as TruthfulQA, word-in-context, word unscramble, and Multi-Task NLU. This selection of prompts and models was intended to show that emergent abilities are not confined to specific models or tasks.

Furthermore, to illustrate the robustness of emergent abilities, the authors explore cases where specialized prompting or fine-tuning is applied. Despite these additional techniques, the phenomenon of emergent abilities remains consistent: performance improvement does not occur until the model reaches a substantial scale threshold. This consistency was demonstrated using LaMDA and Anthropic models, reinforcing the conclusion that emergent abilities depend significantly on scale.



### Findings

## Insights, Impacts, and Next Steps

### Critical Analysis

### Impact

### Future Directions

### Limitations and Potential Extensions

## Citation
[citation]




