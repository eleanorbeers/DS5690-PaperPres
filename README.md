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

#### Formal Representation (Pseudocode - Mathematic)

We can represent the researchers findings formally in the following way:

1. **Model scale:** We let *S* represent the scale of our model, which is measured in FLOPs.

    ![image](https://github.com/user-attachments/assets/8d8f9df5-9ed4-4994-986a-c1712570be0e)

2. **Phase Transition:** We let *S<sub>threshold* represent the critical point in scale at which model performance is no longer random, but rather a direct function of model scale. Thus, emergent abilities are observed when:

    ![image](https://github.com/user-attachments/assets/30a5d08d-6f27-4b2e-b7df-adeb12a353c3)

     
3. **Model performance:** We measure model performance on task *T* as a function of scale *S*. We observe two distinct relationships here, depending on whether phase transition has been surpassed or not.

    ![image](https://github.com/user-attachments/assets/862943a2-c07f-47bd-9cd2-520b0cae5bc5)

4. **Performance with emergence:** Here we observe a noted change in performance of the model after reaching the emergence threshold, as denoted by:

    ![image](https://github.com/user-attachments/assets/e5543a06-c6de-4c29-802b-a4dcf8b42d04)

5. **Relationship between emergence and scale:** We can assume performance increases exponentially after the phase transition is reached:

    ![image](https://github.com/user-attachments/assets/460d6fd3-3ebb-41e3-a911-6d7b6832d606)

   - Where α and β are constants that control the rate of emergent performance ***after*** the threshold has been reached.
  
6. **Detecting emergence:** We define the following relationship to represent the relationship between the emergence threshold and scale and detect when the threshold has been met (i.e., when emergent abilities can be observed):

    ![image](https://github.com/user-attachments/assets/8325827d-a0e9-40e8-92dc-acde68405c32)

   - Where δ is a performance improvement threshold, signaling emergence has been met.
  
*See **demo.ipynb** for code version of pseudocode*

### Findings

The authors’ findings on the effect of increasing model scale on performance revealed a unique phenomenon: *emergent abilities* that appear only in models exceeding a specific scale threshold. This phenomenon was observed consistently across five different types of models—LaMDA, GPT-3, Gopher, Chinchilla, and PaLM—and across eight distinct task types, all evaluated using few-shot prompting techniques. These tasks span various benchmarks, including arithmetic, word unscrambling, conceptual mapping, question-answering, and multi-task language understanding, providing a comprehensive scope for observing emergent abilities in diverse settings.

Here are the observed performance curves:

<img width="605" alt="Screenshot 2024-11-10 at 5 41 00 PM" src="https://github.com/user-attachments/assets/e022bc03-9a55-4310-8e52-c344f151f3c9">

As shown, across nearly all model and task combinations, the performance curves follow a consistent pattern: flat, random, or weakly positive until the model reaches a certain scale threshold. At this point—where the performance curves cross the pink horizontal line marking the critical *phase transition*—performance begins to increase sharply, often at near-exponential rates. This threshold acts as a clear indicator of emergent abilities, signifying that the model has reached a scale where it can perform these tasks significantly better than random or baseline levels.

The authors also examined whether this threshold effect persisted across variations in prompt and task setup. They tested specialized prompting techniques and fine-tuning across different models, finding that even with these optimized conditions, models needed to surpass a certain scale threshold to exhibit emergent abilities. This suggests that emergent performance is inherently tied to model size and compute rather than prompt-specific optimizations.

Here are the performance curves observed under these different prompting and fine-tuning scenarios:

<img width="915" alt="Screenshot 2024-11-10 at 5 37 54 PM" src="https://github.com/user-attachments/assets/bc2f9d1c-cf6b-4508-98d0-90038c66d3e2">

As discussed earlier, the researchers noted that model scale can be defined and measured in several ways beyond compute (measured in FLOPs) alone. Model size (number of parameters) and the size of the model’s training dataset are additional ways to quantify scale. However, because model size and compute typically go hand-in-hand—since larger models require more compute—the authors chose to focus on compute in their primary analysis. They did, however, include performance curves as a function of model parameters in the appendix. These curves show that similar performance patterns are observed when measuring performance by model parameters, indicating that this is another effective way to measure scale.

<img width="593" alt="Screenshot 2024-11-10 at 5 49 53 PM" src="https://github.com/user-attachments/assets/ac027266-604e-4a56-b3d4-b12a65b10df2">


## Insights, Impacts, and Next Steps 

### Impact

In this paper, the researchers identify a phenomenon unique to large-scale LLMs that they call "emergent abilities." Across a broad range of model types and tasks, a dramatic increase in performance is observed once models pass a certain scale threshold. This discovery is particularly relevant at a time when small language models (SLMs) are gaining popularity due to their efficiency and ability to run standalone on mobile devices. SLMs enable users to interact with the model directly on their device without relying on external computational resources, as would be necessary when using a traditional LLM, like ChatGPT or Claude.

Additionally, SLMs often outperform larger models in certain tasks because they are trained on specific domains, allowing them to excel in specialized areas. For example, an SLM fine-tuned on legal or medical knowledge may surpass a general-purpose LLM in those fields. These factors, among others, are driving the growth of SLMs, as they offer computational efficiency and focused expertise. However, this paper serves as a reminder that while there are compelling reasons to use smaller-scale models, increasing model scale has a significant and measurable effect on performance.

The impact of these findings lies in their demonstration that certain capabilities are only accessible in large-scale models. This is a crucial insight as it suggests that, regardless of optimization or specialized training, there are abilities that small models simply cannot achieve. By showing that these emergent abilities require substantial scale, the paper highlights a fundamental trade-off in the development of language models: the efficiency and portability of SLMs versus the enhanced, often unexpected, capabilities that come with scaling up. The results here suggest that while SLMs have their place, large-scale models remain essential for applications requiring these unique emergent abilities, especially in complex, interdisciplinary tasks where smaller models may fall short.

In addition to the positive impact of scale on model performance, the researchers also highlighted the potential for emergent risks that accompany these observed emergent abilities. If increasing scale leads to dramatic improvements in model capabilities, could it also amplify issues such as bias, toxicity, and dishonesty? These risks are already prevalent in current LLMs, where large-scale models sometimes exhibit harmful biases or generate misleading information. The researchers raise the question: as we continue to push the boundaries of scale, will these risks grow proportionately? And, if so, could they reach levels that might outweigh the benefits of further scaling? This discussion underscores the need for ongoing scrutiny as models become larger, ensuring that the development of LLMs does not lead to unintended consequences at unprecedented scales.

### Future Directions

The most obvious, and perhaps most important, direction provided by this paper is the need to continue scaling models up to reach new heights in performance. We have yet to observe a tipping point in this phenomenon, suggesting that the potential for improvement remains untapped and could be far greater than anticipated. Finding this tipping point—or even understanding if one exists—requires a deeper dive into the mechanisms behind this phenomenon and a way to predict when and why emergence occurs.

Additionally, the researchers note that while model scale has a clear impact on performance, it’s not the only factor. Continued improvements in prompting techniques and the scaling of datasets are other viable ways to enhance model performance. These approaches are appealing because they may achieve gains with far fewer computational resources than scaling up models themselves. Exploring these alternatives alongside model scaling could lead to a more balanced approach to advancing language models.

### Limitations and Potential Extensions

While the authors make a small nod to the cost of computational resources needed for continued scaling of LLMs, they do not fully address the extent of this cost, both financially and environmentally. At its current scale, ChatGPT’s daily energy use is around half a million kilowatt-hours—the same amount used to power about 180,000 U.S. households. If we keep scaling LLMs beyond their current size, energy consumption and environmental impact will only increase. With the threat of a climate crisis already looming, it raises the question: do the benefits of additional scaling outweigh the harm caused in this context?

Another overlooked limitation is the accessibility of the resources needed to build and operate large-scale models. Not all organizations have the infrastructure to support these enormous computational needs, which could mean that only a few, well-funded groups have access to the best models. This creates a concentration of power that could hold back innovation and make it harder for smaller players to compete.

If further research focuses on understanding the performance curve and the mechanisms behind emergence, we may be able to find ways to predict when emergent abilities will appear. Predicting the performance curve could help us identify where the tipping point is, allowing us to be more intentional with scaling and to avoid unnecessary costs and impacts.

## Citation

Gordon, C. (2024, March 12). *ChatGPT and generative AI innovations are creating sustainability havoc*. Forbes. https://www.forbes.com/sites/cindygordon/2024/03/12/chatgpt-and-generative-ai-innovations-are-creating-sustainability-havoc/

Wei, J., Tay, Y., Bommasani, R., Raffel, C., Zoph, B., Borgeaud, S., Yogatama, D., Bosma, M., Zhou, D., Metzler, D., Chi, E. H., Hashimoto, T., Vinyals, O., Liang, P., Dean, J., & Fedus, W. (2022). *Emergent abilities of large language models*. arXiv. https://arxiv.org/abs/2206.07682



