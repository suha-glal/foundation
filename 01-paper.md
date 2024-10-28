---
title: Explainable AI-Driven Transfer Learning in EEG-based-Attention 
subject: Foundation in Computation
subtitle: Cross-Population Generalization
short_title: EEG-based-Attention
authors:
  - name: Soha Ahmed
    affiliations:
      - College of Information Technology
      - United Arab Emirates University
    orcid: 0000-0002-4912-4819
    email: 700044614@uaeu.ac.ae
  - name: Medha Mohan Ambali Parambil
    affiliations:
      - College of Information Technology
      - United Arab Emirates University
    orcid: 0000-0002-4912-4819
    email: 700044516@uaeu.ac.ae
license: CC-BY-4.0
keywords: explainable AI, transfer learning, EEG-based-Attention, Cross-Population Generalization, BCI
date: 2024-10-22
exports:
  - format: typst
    template: lapreprint-typst
    output: exports/foundation-project.pdf
---

+++ {"part":"abstract"}

The integration of Explainable Artificial Intelligence (XAI) and Transfer Learning (TL) in EEG-based Brain-Computer Interfaces (BCIs) for cross-population generalization is an emerging field with significant potential. Current research typically addresses XAI and TL separately, with limited approaches combining both to enhance model generalization across diverse populations. This research project aims to bridge this gap by developing an explainable AI-driven transfer learning framework focused on improving cross-population performance in EEG-based attention models. The proposed approach leverages XAI techniques, such as SHAP and LIME, to provide interpretability in model decisions and insights into EEG feature relevance, while TL methods, such as domain adaptation and iterative learning models, are employed to minimize retraining and enhance model generalization. Key contributions include enhanced explainability in BCI models, improved trust and transparency through XAI tools, and robust generalization with minimal retraining. By diagnosing model failures and identifying transferable and problematic features, this study provides actionable insights to advance both the interpretability and practical applicability of EEG-based BCI systems.

+++

# Dataset



This dataset is part of the Frontiers Research Topic on "Datasets for Brain-Computer Interface Applications" and was initially used in a study to assess the performance of a gaze-independent Brain-Computer Interface (BCI) based on covert spatial attention shifts [Reichert et.al, 2020](https://doi.org/10.3389/fnins.2020.591777). The BCI aims to decode binary decisions based on visual stimuli presented in opposite visual hemifields. Participants communicated their responses by covertly shifting attention, while EEG and EOG data were recorded. This dataset is particularly useful for research in BCI, attention modeling, and EEG-based decision decoding, providing valuable insights into how spatial attention shifts can be detected and decoded.

The dataset contains EEG and eye-movement data from 18 participants, with recordings including horizontal and vertical EOG, and EEG channel data during BCI experiments. These recordings are segmented into trials, including participant intentions (ground truth for classifier training), stimulus onset triggers, and feedback from the BCI.
[Link to the dataset: EEG-based BCI (002-2020)](http://bnci-horizon-2020.eu/database/data-sets)

## Background

:::{figure} ./images/visiual-attention.svg
:label: Spatial_attention 
Flowchart illustrating the relationship between visual attention, spatial attention, overt attention, covert attention, and the N2pc neural signal. Covert attention leads to N2pc, while overt attention involves eye movements toward stimuli.
:::


[](#Spatial_attention) illustrates the hierarchical relationship between visual attention, spatial attention, overt attention, covert attention, and the N2pc neural signal. At the top, **visual attention** represents the broad cognitive ability to focus on specific elements of the visual environment. Visual attention is further categorized into spatial attention, which refers to focusing on particular locations in the visual field.

**Spatial attention** is divided into two types:

- **Overt attention**, where attention is directed by moving the eyes toward a stimulus, represented by an eye with arrows pointing outward.

- **Covert attention**, where attention is shifted to a target without eye movement, represented by dashed lines showing focus on the periphery while maintaining central gaze.

**N2pc** is linked specifically to covert attention. It represents a neural signal that is measurable using EEG when a person focuses attention on an item in the periphery without moving their eyes. This component is key in decoding spatial attention shifts in brain-computer interface (BCI) applications. The N2pc is shown as a brainwave pattern associated with these covert attention shifts.

peripheral vision (the edges of your visual field)

:::{table} Summary of the Dataset  
:label: table-summary  
:align: center  

| **Category**               | **Description**                                                                                        |  
|----------------------------|--------------------------------------------------------------------------------------------------------|  
| **Number of Participants**  | 18                                                                                                     |  
| **Data Format**             | MATLAB (.mat) files                                                                                    |  
| **Types of Data Recorded**  | EEG, horizontal EOG (HEOG), vertical EOG (VEOG)                                                        |  
| **Sampling Rate**           | 250 Hz                                                                                                |  
| **Stimuli**                 | Red "x" cross and green "+" cross, presented in opposite visual hemifields                             |  
| **BCI Task**                | Covert spatial attention shifts to red or green crosses corresponding to "yes"/"no" decisions          |  
| **Number of Trials**        | 24 per run (first two runs involved focusing on one side, others involved answering objective questions)|  
| **Channels Recorded**       | 30 Ag/AgCl EEG electrodes + horizontal and vertical EOG                                                |  
| **Trial Information**       | Stimulus presentation, intention, feedback, eccentricity of stimuli, symbol size                       |  
| **Additional Files**        | Example MATLAB code for analyzing the BCI experiment data                                              | 
 

:::

## Dataset Exploration

### Distribution of Subjects Demogrphic information

:::{figure} #HandednessGenderPieChart
:label: fig-HandednessGenderPieChart
:::

[](#fig-HandednessGenderPieChart) shows the **distribution of handedness and gender** across participants. The left pie chart represents the handedness, where a large majority (94.4%) of participants are right-handed, with only 5.6% being left-handed. The right pie chart depicts the gender distribution, showing that 55.6% of participants are female and 44.4% are male. This distribution helps in understanding the demographic composition of the participants, which may impact certain experimental results, such as responses in a BCI experiment.

:::{figure} #AgeLanguageDist
:label: fig-AgeLanguageDist
:::
[](#fig-AgeLanguageDist) illustrates the distribution of two additional demographic variables: **Age** and **Language**. The left histogram shows the distribution of participants by age, ranging from 18 to 38 years old, with peaks at 25, 27, and 37 years. The majority of participants are clustered around the mid-twenties and late thirties. The right bar chart shows the distribution of participants by language, revealing that most participants (16) speak German, while a small number (2) speak English. These demographic insights provide important context for the diversity in the dataset.



### EOG Signal vs. Gaze Shift Plot

The **EOG Signal vs. Gaze Shift plot** is key for calibrating BCIs by mapping eye movements (EOG signals) to gaze shifts (horizontal and vertical), improving:

- **Gaze tracking**: Accurately maps eye movements to gaze direction.
- **Artifact reduction**: Filters noise from EEG data caused by eye movements.
- **Personalization**: Customizes BCI for each user.

This calibration helps the BCI interpret user intent and improves accuracy in decoding eye movements.

:::{figure} #EOGVsGazeShift
:label: fig-EOGVsGazeShift
:::

[](#fig-EOGVsGazeShift) displays two scatter plots showing the relationship between **EOG signal strength** and **gaze shift**:

#### 1. **Horizontal EOG Signal vs. Horizontal Gaze Shift**
- **X-axis**: Horizontal EOG (HEOG)
- **Y-axis**: Horizontal Gaze Shift (degrees)

**Interpretation**:
- Positive HEOG correlates with gaze shifts to the right; negative HEOG with shifts to the left.
- A clear linear relationship indicates accurate detection of horizontal gaze shifts.

#### 2. **Vertical EOG Signal vs. Vertical Gaze Shift**
- **X-axis**: Vertical EOG (VEOG)
- **Y-axis**: Vertical Gaze Shift (degrees)

**Interpretation**:
- Most points are around 0° (straight ahead), with minor clusters at ±2°.
- Less vertical gaze movement, and weaker correlation compared to horizontal shifts.

#### Summary:
- The **horizontal plot** shows a strong correlation between HEOG and gaze shift, aiding BCI calibration for left/right movements.
- The **vertical plot** shows limited variation, suggesting less informative VEOG signals for significant vertical movements.

### Oddball Paradigm

The **oddball paradigm** is an experimental design used in cognitive neuroscience and psychology to study how the brain responds to unexpected or rare stimuli.

#### Key Components:
- **Standard Stimuli**: Repetitive, frequent stimuli.
- **Oddball Stimuli**: Rare, deviant stimuli that differ from the standard ones.
- **Response**: Participants may be asked to detect and respond to the oddball stimuli.

#### Types of Oddball Paradigms:
- **Auditory Oddball**: Standard and oddball stimuli are sounds.
- **Visual Oddball**: Standard and oddball stimuli are visual (e.g., images or shapes).
- **Motor Oddball**: Subjects make specific motor responses to the oddball stimuli.

#### Purpose:
- The oddball paradigm is used to study attention, cognitive processing, and event-related potentials (ERPs), especially the **P300 wave**.
- It helps in understanding cognitive processes and disorders like schizophrenia, ADHD, and Alzheimer's.

#### Example:
In an auditory oddball experiment, participants hear a series of beeps at one pitch (standard stimuli) and occasionally hear a beep at a different pitch (oddball stimulus). The brain’s response to the oddball stimulus, often reflected in the **P300 wave**, is of particular interest to researchers.


## Preprocessing

[Example-code](https://gitlab.stimulate.ovgu.de/christoph.reichert/visual-spatial-attention-bci/-/tree/master?ref_type=heads)
