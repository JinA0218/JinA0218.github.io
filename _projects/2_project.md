---
layout: page
title: BCS.50041
description: (6th Semester) Neuroscience inspired AI - Insights from Brain Inspired Replay for Continual Learning
img: assets/img/project/bcs541.png
importance: 2
category: coursework
---
#### **Teaching AI to Remember: Insights from Brain-Inspired Replay for Continual Learning [[pdf]](https://drive.google.com/file/d/1HcYfSXhaHh8bmBdXqJt7Jze87Srz868s/view?usp=sharing) [[code]](https://github.com/JinA0218/BCS.50041_Project)[[slide]](https://drive.google.com/file/d/1HjMsyh-m6IaZrDFm8RsmBsWk8zU29QGa/view?usp=sharing)**

- authors: Jina Kim
- affiliations: KAIST, South Korea

---

## Overview

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/project/catastrophic_forgetting.png" title="concept figure" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    <strong>Catastrophic Forgetting in AI during Continual Learning.</strong>
</div>

Artificial neural networks (ANNs) excel at learning from large datasets but still suffer from **catastrophic forgetting**—the loss of previously learned knowledge when adapting to new tasks. Inspired by the **memory replay mechanisms** in the human brain, this project investigates the effectiveness of **internal replay** for **long-term memory in AI**.  

Using **CIFAR-100** in a **class-incremental learning (class-IL)** setting, we provide an in-depth analysis of internal replay, both as a standalone mechanism and in combination with **Synaptic Intelligence (SI)**. The findings highlight the **trade-off between memory stability and learning plasticity**, while also revealing limitations of current brain-inspired approaches.  

---

## Motivation

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/project/brain.png" title="concept figure" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    <strong>Memory replay in Human Brain.</strong>
</div>

Humans preserve long-term memories through **neural replay**, where patterns of past experiences are reactivated during learning and consolidation. Inspired by this, recent works (e.g., Van de Ven et al. 2020) proposed **brain-inspired replay mechanisms** to improve AI’s continual learning ability.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/project/brain_inspired_continual_learning.png" title="concept figure" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    <strong>Key components of "Brain-inspired replay for continual learning with artificial neural networks".</strong>
</div>

In particular, **Van de Ven et al. (2020)** introduced a *Brain-Inspired Replay (BIR)* framework, which extends generative replay by incorporating several biologically motivated components:
- **Replay through feedback**: integrates hippocampal-like generators with cortical-like main models.  
- **Conditional replay**: allows selective reactivation of specific classes through latent mixture modeling.  
- **Context-based gating**: mimics task-dependent neural reactivation.  
- **Internal replay**: replays latent representations rather than raw inputs, closer to how the brain replays experiences.  
- **Distillation**: uses soft targets to stabilize learning when generated samples are imperfect.  

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/project/internal_replay.png" title="concept figure" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    <strong>Internal replay as the most important component.</strong>
</div>

Their analysis highlighted **internal replay** as the *most influential* factor in mitigating catastrophic forgetting, but also showed that the overall model suffered from low absolute performance and poor scalability.  

**This work builds directly on this foundation**:  
- We isolate and study the contribution of **internal replay** in detail.  
- We evaluate its interaction with **Synaptic Intelligence (SI)**, a complementary parameter-constraining method.  
- We provide in-depth analyses (accuracy curves, reconstruction error, UMAP embeddings) to reveal not only its strengths in retention but also its limitations in representational overlap.  

This project therefore extends Van de Ven et al.’s framework by going beyond performance metrics to analyze **how and why internal replay affects learning dynamics**, aiming to inform the design of more effective brain-inspired continual learning systems.  

---

## Methodology

#### Models
We evaluate the following variants:
- **BIR (Brain-Inspired Replay)** with and without Internal Replay  
- **BIR + SI (Brain-Inspired Replay + Synaptic Intelligence)** with and without Internal Replay  

#### Dataset
- **CIFAR-100** in **Class-Incremental Learning (Class-IL)** setup  
- Sequentially trained on **10 tasks** (10 classes each)  

#### Metrics
- **Accuracy**: Initial, final, retention ratio, forgetting score  
- **Log-Likelihood & Reconstruction Error**: Measures representational fidelity  
- **Silhouette Score & UMAP**: Evaluates latent space separability  

---

## Key Results

- **Retention vs Forgetting**: 

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/project/reten_forgetting.png" title="concept figure" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    <strong>Retention Ratio and Forgetting Score per task.</strong> Retention ratio comparison (left) and forgetting score comparison (right) between BIR(w/ IR), BIR(w/o IR), BIR+SI(w/ IR), BIR+SI(w/o IR) for all tasks. Dashed lines refer to as the average test accuracy throughout all the tasks for each model.
</div>

Internal replay (IR) improves **retention ratio** and reduces **forgetting score**, especially when combined with SI. 

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/project/acc.png" title="concept figure" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    <strong>Initial accuracy and Final accuracy per task.</strong> Initial test accuracy comparison (left) and final test accuracy comparison (right) between BIR(w/ IR), BIR(w/o IR), BIR + SI(w/ IR), BIR + SI(w/o IR) for all tasks. Dashed lines refer to the average test accuracy throughout all the tasks for each model.
</div>

However, IR also reduces **initial accuracy**, indicating a stability–plasticity trade-off.  

- **Representation Quality**

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/project/log_like.png" title="concept figure" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    <strong>Log likelihood distribution and Reconstruction error distribution.</strong> Comparison of log likelihood distribution (left) and reconstruction error distribution (right) between model with internal replay (BIR(w/ IR)) and model without internal replay (BIR(w/o IR)).
</div>

IR models fit the data better (higher log-likelihood, lower reconstruction error).

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/project/umap.png" title="concept figure" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    <strong>Silhouette score andUMAPvisualization of embeddings on layer fcE.fcLayer2.linear.</strong> (a)Comparisonof silhouette score between model with internal replay (BIR(w/IR)) and model without internal replay (BIR(w/oIR)). UMAP visualization of embeddings on task7 for (b) BIR (w/IR), (c) BIR+SI (w/IR), (d) BIR (w/oIR), (e) BIR+SI (w/oIR). The experiments are held on layer fcE.fcLayer2.linear.
</div>

But hidden layer embeddings remain **poorly separated**, with **high representational overlap** across tasks.  

- **Trade-Off Observed**

**BIR + SI (w/ IR)** achieves the best long-term stability.  
**BIR (w/o IR)** achieves the best short-term plasticity.  

---

## Analysis & Insights
- **Internal Replay** helps mitigate catastrophic forgetting but lowers task-level learning capacity.  
- **Synaptic Intelligence (SI)** provides stability by protecting critical parameters, but slows adaptation.  
- **Open Problem**: How to retain strong initial performance while preventing forgetting.  

---
## Future Directions
- Investigate **sparsity of context-gating masks**
- Explore **layer-wise replay placement**
- Extend analysis with **hippocampus-inspired mechanisms** (e.g., conditional replay, spatial memory)
- Align AI replay models with **neuroscience theories** of memory consolidation

## Key References
- van de Ven, G.M., Siegelmann, H.T. & Tolias, A.S. Brain-inspired replay for continual learning with artificial neural networks. Nat Commun 11, 4069 (2020).
- Zenke, F., Poole, B., & Ganguli, S. (2017, July). Continual learning through synaptic intelligence. In International conference on machine learning (pp. 3987-3995). PMLR.
- Bear, M., Connors, B., & Paradiso, M. A. (2020). Neuroscience: Exploring the brain, enhanced edition: Exploring the brain. Jones & Bartlett Learning.
- More can be found in [[pdf]](https://drive.google.com/file/d/1HcYfSXhaHh8bmBdXqJt7Jze87Srz868s/view?usp=sharing)