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

#### Formal Representation (Pseudocode)

We can represent the researchers findings formally in the following way:

1. Model scale: We let *S* represent the scale of our model, which is measured in FLOPs.
  - *S* = FLOPs

2. Phase Transition: We let *S<sub>threshold* represent the critical point in scale at which model performance is no longer random, but rather a direct function of model scale. Thus, emergent abilities are observed when:
   - *S* ≥ *S<sub>threshold*
     
3. Model performance: We measure model performance on task *T* as a function of scale *S*. We observe two distinct relationships here, depending on whether phase transition has been surpassed or not.
   - For *S* ≤ *S<sub>threshold*
     - P(*T, S*) ≈ random baseline performance
   - For *S* ≥ *S<sub>threshold*
     - P(*T, S*) increases as a function of *S*
    
4. Performance with emergence: Here we observe a noted change in performance of the model after reaching the emergence threshold, as denoted by:

   *P(T, S)* = {
   
      *f*<sub>base</sub>(*S*),      if *S* < *S*<sub>threshold</sub>
      
      *f*<sub>emergent</sub>(*S*),  if *S* >= *S*<sub>threshold</sub>
      
    }

6. Relationship between emergence and scale: We can assume performance increases exponentially after the phase transition is reached:

    *f*<sub>emergent</sub>(*S*) = *α* ⋅ *e*<sup>β (*S* - *S*<sub>threshold</sub>)</sup>

   - Where α and β are constants that control the rate of emergent performance ***after*** the threshold has been reached.
  
8. Detecting emergence: We define the following relationship to represent the relationship between the emergence threshold and scale and detect when the threshold has been met (i.e., when emergent abilities can be observed):

   *P(T, S)* - *f*<sub>base</sub>(*S*) > *δ*

   - Where δ is a performance improvement threshold, signaling emergence has been met.

### Findings

The authors’ findings on the effect of increasing model scale on performance revealed a unique phenomenon: *emergent abilities* that appear only in models exceeding a specific scale threshold. This phenomenon was observed consistently across five different types of models—LaMDA, GPT-3, Gopher, Chinchilla, and PaLM—and across eight distinct task types, all evaluated using few-shot prompting techniques. These tasks span various benchmarks, including arithmetic, word unscrambling, conceptual mapping, question-answering, and multi-task language understanding, providing a comprehensive scope for observing emergent abilities in diverse settings.

Here are the observed performance curves:

<img width="1083" alt="Screenshot 2024-11-10 at 5 29 31 PM" src="https://github.com/user-attachments/assets/67ce7215-2e1c-4d97-b087-17f11376afb2">

As shown, across nearly all model and task combinations, the performance curves follow a consistent pattern: flat, random, or weakly positive until the model reaches a certain scale threshold. At this point—where the performance curves cross the pink horizontal line marking the critical *phase transition*—performance begins to increase sharply, often at near-exponential rates. This threshold acts as a clear indicator of emergent abilities, signifying that the model has reached a scale where it can perform these tasks significantly better than random or baseline levels.

The authors also examined whether this threshold effect persisted across variations in prompt and task setup. They tested specialized prompting techniques and fine-tuning across different models, finding that even with these optimized conditions, models needed to surpass a certain scale threshold to exhibit emergent abilities. This suggests that emergent performance is inherently tied to model size and compute rather than prompt-specific optimizations.

Here are the performance curves observed under these different prompting and fine-tuning scenarios:

<img width="915" alt="Screenshot 2024-11-10 at 5 37 54 PM" src="https://github.com/user-attachments/assets/bc2f9d1c-cf6b-4508-98d0-90038c66d3e2">

These findings provide strong evidence that emergent abilities are not exclusive to one type of task or model architecture but are a consistent outcome of scaling across various contexts. This pattern reinforces the critical role of scale in unlocking capabilities that smaller models are unable to achieve, even with additional task-specific tuning.

## Insights, Impacts, and Next Steps

### Critical Analysis

### Impact

### Future Directions

### Limitations and Potential Extensions

## Citation
[citation]




