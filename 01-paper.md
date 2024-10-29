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
  - format: tex
    output: exports/latex/
  - format: typst
    template: lapreprint-typst
    output: exports/pdf/foundation-project.pdf  
 
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
### Symbol Features Testing
The researchers showed symbols to participants in a way that varied their perceived size and position in the visual field:

Different visual angles: 
In vision science, "visual angle" refers to the angle a visual object subtends on the retina, influencing how large it appears. Changing the visual angle affects how large or small the symbols appear to the viewer.
Altering symbol size: 
This involves changing the actual size of the symbols, making them appear larger or smaller.
Eccentricity:
 This term refers to how far a symbol is from the center of the viewer's gaze or focal point. By placing symbols at different distances from the central line of sight (e.g., closer or farther to the sides of their visual field), they tested how well participants could perceive symbols in different locations.
In short, they adjusted both the size of the symbols and their distance from the center of vision to understand how these factors affect perception.
## Definitions:

Behavioral performance
: refers to how well the user performs tasks or responds to stimuli.

SSVEP amplitude 
: is the strength of the brain response generated by seeing a flickering stimulus (steady-state visually evoked potential). SSVEP is often used in BCIs because it is easy to detect when the user’s attention is on the target.

Dichotomous question
: is a question that offers only two possible answers, typically in a "yes or no" format. This type of question is straightforward and requires a clear, binary choice. Dichotomous questions are commonly used in surveys, experiments, and decision-making processes when simple, definitive responses are needed. Examples include:

"Do you prefer coffee over tea?"
"Is Berlin a city?"
"Are you a vegetarian?"
In research and testing, dichotomous questions can help streamline analysis by providing clear, easily categorizable responses.

## Experiment Setup
In this experiment, a photodiode was used to detect changes in visual stimuli on the screen, allowing for precise synchronization between the events displayed and the EEG recording. Here’s how it works:

Photodiode
: This is a small sensor that reacts to light, detecting changes in brightness or flickering on the screen.

Synchronization
: By positioning the photodiode on the display (usually in a corner where it doesn’t interfere with the participant's view), it captures the exact timing of when a visual stimulus appears or changes.

EEG Timing Accuracy
: The moment the photodiode detects a stimulus change, it sends a signal that is recorded alongside the EEG data. This enables the EEG system to record the participant’s brain response at the precise moment a stimulus appears, enhancing the accuracy of analyzing brain responses to each visual event.

The setup and equipment used for recording EEG (electroencephalography) data, focusing on electrode type, placement, and the amplifier:

EEG Recording with 29 Ag/AgCl Electrodes
: EEG data was collected from 29 electrodes made of silver/silver chloride (Ag/AgCl), which are commonly used in EEG studies due to their stable and accurate signal conduction.

Standard Positions in an Extended 10–20 Montage
: The "10–20 montage" refers to a standardized system for electrode placement on the scalp. It divides the scalp into a grid with electrodes placed at specific points (10% or 20% of measured distances) that correspond to brain areas. This extended version includes additional electrodes for more detailed data, especially in high-density recordings.

Using a BrainAmp DC Amplifier
: The BrainAmp DC Amplifier, from Brain Products GmbH, is a device that amplifies the EEG signals, making them strong enough to be accurately measured and analyzed. It records signals across a wide range of frequencies, including direct current (DC), which provides more detailed information on brain activity.

In summary, this setup ensures accurate and detailed EEG recording by using high-quality electrodes placed at standardized scalp locations and an amplifier to capture a wide frequency range.

### EOG (electrooculography) calibration process
This part describes the EOG (electrooculography) calibration process before the main experiment, allowing researchers to understand how eye movements affect the recorded signals. Here’s a breakdown:

EOG Calibration with a Moving Cross 
: To capture baseline EOG data, participants tracked a cross on the screen with their gaze. The cross moved every 1,250 milliseconds (1.25 seconds), shifting horizontally from the center by varying degrees (1 to 7 degrees). In some trials (30%), the cross also moved vertically by 2 degrees, adding complexity to the eye-tracking pattern.

Eye Blinks as Part of Calibration
: At three points, the cross was replaced by a circle, signaling participants to blink. These intentional blinks were included to understand how blinks appear in EOG data and to differentiate them from gaze shifts.

Calibration Data Collection
: Participants completed a total of 40 gaze shifts and three blinks over about a minute. The data collected from these intentional movements provided calibration, mapping EOG signal strength to specific gaze angles.

Purpose of Calibration
: This calibration was essential for detecting unintended eye movements during the experiment. By understanding the typical EOG signal patterns from known gaze shifts and blinks, researchers could evaluate whether any unintentional eye movements occurred during BCI control and adjust accordingly.

In summary, this procedure allowed the researchers to calibrate EOG data to specific gaze angles and blinks, helping ensure accurate interpretation of eye-related signals during the main experiment.

### Questions and Feedback
In this experiment, participants answered yes/no questions by directing their attention to one of two symbols on the screen: a green “+” for “yes” and a red “×” for “no.” Here’s how it worked:

Objective Questions
: The first 96 questions were factual (e.g., “Is Berlin a city?”). To keep answers balanced between “yes” and “no,” each question had an opposite version (e.g., “Is Berlin a continent?”), ensuring an even split of expected responses.

Subjective Questions
: The last 24 questions were personal, like “Are you a vegetarian?”, showing how the system could be applied in real life. These questions didn't have right or wrong answers; they were based on the participant's personal views.

BCI and Feedback
: The brain-computer interface (BCI) didn’t check if answers were correct; instead, it focused on detecting where the participant’s attention shifted—either to the “yes” or “no” symbol—using EEG signals. The BCI then showed the detected answer as feedback.

Participant Feedback
: To confirm if the BCI’s response matched their intended answer, participants pressed a button. They used their index finger if the feedback was correct and their middle finger if it wasn’t.

### Trial Structure
In this experiment, each trial had the following structure:

1. **Question Display and Response Preparation:** A question appeared on the screen, and the participant decided on their answer (yes or no). They looked at a central fixation cross, either green (for "yes") or red (for "no"), to keep their chosen answer in mind. Once ready, they pressed a button to start the sequence.

2. **Stimulus Sequence:** The trial included a sequence of ten quick visual displays, designed to optimize both speed and accuracy. Each display showed a red "×" and a green "+," with one on the left and one on the right, in random order but balanced to appear evenly on each side.

3. **Stimulus Display Details:** Each display lasted 250 milliseconds, with an interval between displays (stimulus onset asynchrony) of 850 milliseconds, randomly varied by 0-250 milliseconds. Around the positions where the symbols would appear, eight gray dots marked these spots to guide the participant’s gaze.

4. **Variations in Position and Size:** The symbols’ horizontal position (α) and size (φ) changed from trial to trial to test different conditions. They used four symbol sizes and five position levels (eccentricities), combining them in pairs for a total of eight unique settings, each repeated three times per block (24 trials per block).

5. **Feedback:** After the stimulus sequence, the BCI provided feedback, displaying either "yes" or "no" based on the participant’s attention. The participant then confirmed if the BCI feedback was correct using a button press. These responses served as "ground truth" data to train and refine the BCI.

In short, each trial involved choosing an answer, tracking a stimulus sequence, receiving BCI feedback, and confirming its accuracy, with different visual conditions tested across trials.

### EEG data preparation

This section explains how the EEG data was prepared to ensure accurate readings of brain activity, focusing on preventing bias, choosing relevant channels, and selecting specific data segments:

Re-referencing the EEG Data
: To avoid creating differences between the left and right sides of the brain due to using a single reference point (which can introduce a "hemispheric bias"), the EEG signals were referenced to the average of both the left and right mastoids (the bony areas behind each ear). This balanced reference helps create a more accurate representation of overall brain activity.

#### Example Steps for Re-referencing EEG Data:

1. **Record Raw EEG Data**: During the EEG recording, include electrodes placed on both the left and right mastoids. Let’s assume we have raw EEG signals recorded from all scalp electrodes and two additional channels specifically for the left and right mastoids.

2. **Calculate the Average Mastoid Reference**:  
   Compute the average signal from the left and right mastoid channels for each time point. If $M_{\text{left}}(t)$ is the signal from the left mastoid and $M_{\text{right}}(t)$ is from the right mastoid, then the average mastoid reference $M_{\text{avg}}(t)$ at any time $t$ can be calculated as:
```{math}
:label: mastoid-average
M_{\text{avg}}(t) = \frac{M_{\text{left}}(t) + M_{\text{right}}(t)}{2}
```
3. **Re-reference Each EEG Channel**:  
   For each EEG channel, subtract the average mastoid reference $M_{\text{avg}}(t)$ from the original EEG signal recorded at that channel. If $E_i(t)$ is the signal from EEG channel $i$, the re-referenced signal $E_i^{\prime}(t)$ for each channel $i$ is calculated as:

```{math}
:label: eeg-referenced
E_i^{\prime}(t) = E_i(t) - M_{\text{avg}}(t)
```

4. **Store or Use the Re-referenced Data**:  
   The resulting EEG signals are now re-referenced to the average mastoid, reducing any left-right bias and providing a balanced view of brain activity.

#### Example Code (Python / MNE Library)
If using Python’s MNE library, the re-referencing can be done as follows:

```python
import mne

# Load your EEG data
raw = mne.io.read_raw_yourfile()  # replace 'yourfile' with the file path

# Specify the mastoid channels
mastoids = ['M1', 'M2']  # example names for left (M1) and right (M2) mastoid channels

# Set the EEG reference to the average of M1 and M2
raw.set_eeg_reference(ref_channels=mastoids)
```

Using a Subset of Channels
: Although 29 electrodes covered the entire head (to ensure comprehensive data availability), only 14 specific channels located in the parieto-occipital region were used for analyzing visual attention. These channels (like O9, O10, and Pz) are positioned over the areas of the brain involved in processing visual stimuli and attention shifts, making them ideal for detecting changes in where participants are focusing.

Segmenting EEG Data for Each Stimulus Sequence
: For each trial, the EEG data corresponding to the specific time window of the stimulus sequence was extracted. Start and stop triggers were sent to the EEG device just before and after the stimulus sequence, marking the precise segment of data relevant to the task.

In short, these steps helped prevent bias, focused on brain regions associated with visual attention, and ensured that only relevant EEG data segments were used for analyzing attention shifts.

## Run(block),trials, stimul(epoch)
Each participant performs 7 runs in total:

First 2 Runs: No questions are presented. In these runs:

1. Run 1: The participant is asked to focus on the green cross for the entire duration.
2. Run 2: The participant is asked to focus on the red cross throughout.
3. Runs 3–6: Objective yes/no questions are presented (e.g., “Is Berlin a city?”). Each of these runs consists of 24 trials with factual questions.

4. Run 7: This final run involves subjective yes/no questions (e.g., “Are you a vegetarian?”), which allows for personal responses.


Each participant answers 120 questions over the course of 5 runs (Runs 3–7):

Runs 3–6: Each of these 4 runs includes 24 trials with objective questions, totaling 4×24=96 objective questions.
Run 7: This run includes 24 trials with subjective questions, adding up to 24 questions.
Thus, across these 5 runs, participants answer 96+24=120 questions.

## Preprocessing

### First step

This section describes how the EEG data was processed and prepared for analysis:

1. **Filtering the Data**: A 4th order zero-phase IIR Butterworth bandpass filter was used to limit the EEG data to frequencies between 1.0 and 12.5 Hz. This type of filter removes unwanted frequencies outside this range, focusing on brainwave frequencies relevant for attention and visual processing. Zero-phase filtering means there is no delay introduced to the signal, keeping the timing intact.

2. **Resampling**: After filtering, the data was resampled to 50 Hz, meaning it now captures 50 data points per second. This reduces the amount of data while retaining essential information, making processing faster and more manageable.

3. **Defining Stimulus Onsets**: The photodiode was used to detect the precise timing of each visual stimulus onset. This allowed each epoch (segment of data) to start exactly when the stimulus appeared.

3. **Epoching the Data**: The data was divided into time segments (epochs) that started from the stimulus onset and lasted for 750 milliseconds. Each epoch, therefore, contains the brain’s response to a specific stimulus within this time window.

4. **Creating Data Matrices**: Each epoch includes 38 sampling points (captured over 750 ms at 50 Hz) across 14 channels. This results in an epoch matrix 𝑋{sub}`𝑖` ∈ 𝑅{sup}`38×14`, where each row represents a time point, and each column represents data from one EEG channel.

In summary, this process filtered and segmented the EEG data to create matrices of time-locked responses to each stimulus, making the data ready for further analysis of attention-related brain signals.

### Symbol 
In this setup, each trial consists of ten **epochs**, each corresponding to one of the ten stimuli shown in sequence. Since all these epochs belong to the same trial, they all relate to the same target item the participant was focusing on.

The epochs were labeled based on the position of the green and red symbols:

- **Label $y_i = 1$**: When the green symbol appeared on the left and the red symbol on the right, that epoch was labeled with $y_i = 1$.
- **Label $y_i = -1$**: When the red symbol was on the left and the green symbol on the right, the epoch was labeled with $y_i = -1$.

These labels help in distinguishing between the two symbol positions, allowing the analysis to recognize and differentiate responses based on the side each color symbol was displayed.

### Decoding Approach

In this section, we describe the **estimation of the decoding model**, which is performed each time the classifier is trained – both online and during the folds of cross-validation. Afterward, we explain how this model is applied to unseen data to provide real-time feedback and to decode left-out trials in cross-validation.

An implementation of this decoding approach can be found in the publicly available dataset (Reichert et al., 2020b).

#### Model Estimation Using Canonical Correlation Analysis (CCA)

We use **canonical correlation analysis (CCA)** to estimate spatial filters and canonical components from the training data. CCA has been shown to be effective for decoding steady-state visually evoked potentials (SSVEPs) and event-related potentials (ERPs) (Nakanishi et al., 2015; Spüler et al., 2014; Xu et al., 2018; Xiao et al., 2020). The approach presented here builds on our previous work (Reichert et al., 2016, 2017) and is closely related to methods recently published (Reichert et al., 2020a).

CCA successively determines coefficient vectors **a** and **b** that linearly combine two sets of variables, **X** and **Y**, such that the correlation between **X a** and **Y b** is maximized. This is expressed mathematically as:

```{math}
(u, v) = \arg \max \, \text{corr}(X a, Y b)
```

where \( u \) and \( v \) are the resulting canonical variables.

In summary, this decoding approach uses CCA to create a model that identifies meaningful brain activity patterns, allowing the system to apply this model to unseen data for real-time classification and cross-validation.

[Example-code](https://gitlab.stimulate.ovgu.de/christoph.reichert/visual-spatial-attention-bci/-/tree/master?ref_type=heads)
