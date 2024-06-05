# Automatic soundscape captioner (SoundSCaper): Soundscape Captioning using Sound Affective Quality Network and Large Language Model

Paper link: 

<br>

- [SoundSCaper](#automatic-soundscape-captioner--soundscaper---soundscape-captioning-using-sound-affective-quality-network-and-large-language-model)
  * [Introduction](#introduction)
    + [1. SoundSCaper training steps](#1-soundscaper-training-steps)
    + [2. Expert evaluation of soundscape caption quality](#2-expert-evaluation-of-soundscape-caption-quality) 
    + [3. Other models](#3-other-models)
  * [Figure](#figure)
    + [1. Overall framework of the automatic soundscape captioner (SoundSCaper)](#1-overall-framework-of-the-automatic-soundscape-captioner-soundscaper)
    + [2. The acoustic model SoundEQnet simultaneously models acoustic scene (AS), audio event (AE), and emotion-related affective response (AR)](#2-the-acoustic-model-soundeqnet-simultaneously-models-acoustic-scene-as-audio-event-ae-and-emotion-related-affective-response-ar)
    + [3. Process of the LLM part in the SoundSCaper](#3-process-of-the-llm-part-in-the-soundscaper)
	+ [4. Spearman's rho correlation between different ARs and AEs predicted by SoundAQnet](#4-spearmans-rho-correlation-r-between-different-ars-and-aes-predicted-by-soundaqnet)
	+ [5. Spearman's rho correlation between different AEs and 8D ARs predicted by SoundAQnet](#5-spearmans-rho-correlation-r-between-different-aes-and-8d-ars-predicted-by-soundaqnet)
  * [Run models](#run-models)
    + [1. ARAUS_CNN](#1-araus_cnn)
    + [2. Baseline CNN](#2-baseline-cnn)
    + [3. Hierachical CNN](#3-hierachical-cnn)
    + [4. MobileNetV2](#4-mobilenetv2)
    + [5. YAMNet](#5-yamnet)
    + [6. CNN-Transformer](#6-cnn-transformer)
    + [7. PANNs](#7-panns)
    + [8. SoundEQnet](#8-soundeqnet)

<br>

## Introduction

### 1. SoundSCaper training steps

1\) Download and prepare the dataset in [Dataset_ARAUS](Dataset_ARAUS); ARAUS can be downloaded [ARAUS_repository](https://github.com/ntudsp/araus-dataset-baseline-models/tree/main). <br> The labels of our annotated acoustic scenes and audio events are in [Dataset_ARAUS](Dataset_ARAUS).


2\) Use the code in [Feature_log_mel](Feature_log_mel) to extract log mel acoustic features. <br> Use the code in [Feature_loudness_ISO532_1](Feature_loudness_ISO532_1) to extract the ISO 532-1:2017 standard loudness features.

3\) Use the code in [Model_SoundEQnet](Model_SoundEQnet) to train SoundEQnet.
  
4\) In [LLM_scripts](LLM_scripts), read the audio scene, audio events, and PAQ 8-dimensional affective response corresponding to the test audio predicted by the trained SoundEQnet, and then output the corresponding soundscape descriptions. <br> Please fill in your OpenAI username and password in [LLM_scripts](LLM_scripts).

### 2. Expert evaluation of soundscape caption quality

[Human_assessment](Human_assessment) contains 

1) a call for experiment; 

2) assessment raw materials: assessment dataset; participant instruction file; local and online questionnaires; 

3) assessment statistical results from a jury composed of 16 audio/soundscape experts.

There are two sheets in the file "SoundSCaper_expert_evaluation_results.xlsx". 

Sheet 1 is the statistical results of 16 human experts and SoundSCaper on the evaluation dataset D1 from the test set.

Sheet 2 is the statistical results of 16 human experts and SoundSCaper on the model-unseen mixed external dataset D2, which has 30 samples randomly selected from 5 external audio scene datasets with varying lengths and acoustic properties.

<!-- 
### 3. SoundSCaper One Run

[One_Run](One_Run) provides the scripts to convert target audio clips directly into soundscape descriptions for easy inference-only use.

If you want to skip the tedious training steps and use LLM-SoundSCaper directly, go directly to [One_Run](One_Run).

Please fill in your OpenAI username and password in LLM_scripts.
-->

### 3. Other models
  
The trained models of the other 7 models in the paper have been attached to their respective folders. 

If you want to train them yourself, please follow the SoundSCaper training steps.

<br>

## Figure

### 1. Overall framework of the automatic soundscape captioner (SoundSCaper)

<h3 align="center"> <p></p></h3>
<div align="center">
<img src="Figure/overall_framework.png" width=100%/> 
</div>  

<br>

### 2. The acoustic model SoundEQnet simultaneously models acoustic scene (AS), audio event (AE), and emotion-related affective response (AR)

<h3 align="center"> <p></p></h3>
<div align="center">
<img src="Figure/SoundEQnet.png" width=100%/> 
</div> 

<br>

### 3. Process of the LLM part in the SoundSCaper
<h3 align="center"> <p></p></h3>
<div align="center">
<img src="Figure/LLM_part.png" width=100%/> 
</div> 

For full prompts and the LLM script, please see [here](LLM_scripts/SoundSCaper_LLM.py).


<br>

### 4. Spearman's rho correlation ($r$) between different ARs and AEs predicted by SoundAQnet
<h3 align="center"> <p></p></h3>
<div align="center">
<img src="Figure/fig_PAQ2_event15.png" width=100%/> 
</div> 


For all 8D AR results, please see [here](Figure/PAQ8ARs.png).

<br>

### 5. Spearman's rho correlation ($r$) between different AEs and 8D ARs predicted by SoundAQnet
<h3 align="center"> <p></p></h3>
<div align="center">
<img src="Figure/fig_event2_PAQ8.png" width=100%/> 
</div> 

For all 15 AE results, please see [here](Figure/event15.png).

## Run models

Please download the testing set (about 3 GB) from [here](https://drive.google.com/file/d/1Rzse5NfbNKyT3mNgcz-y1GUueAnjlOR1/view?usp=sharing), and place it under the Dataset folder.
 

### 1. ARAUS_CNN

```python 
cd Other_ARAUS_CNN/application/
python inference.py
*****
Number of 3576 audios in testing
Parameters num: 0.521472 M
ASC	Acc:  89.42 %
AEC	AUC:  0.85
PAQ_8D_AR	MSE MEAN: 1.125
pleasant_mse: 0.976 eventful_mse: 1.097 chaotic_mse: 1.106 vibrant_mse: 1.061
uneventful_mse: 1.246 calm_mse: 1.059 annoying_mse: 1.198 monotonous_mse: 1.259
``` 

### 2. Baseline CNN

```python 
cd Other_Baseline_CNN/application/
python inference.py
*****
Parameters num: 1.0099 M
ASC	Acc:  86.96 %
AEC	AUC:  0.92
PAQ_8D_AR	MSE MEAN: 1.301
pleasant_mse: 0.991 eventful_mse: 1.445 chaotic_mse: 1.330 vibrant_mse: 1.466
uneventful_mse: 1.378 calm_mse: 1.079 annoying_mse: 1.261 monotonous_mse: 1.457
``` 

### 3. Hierachical CNN

```python 
cd Other_Hierarchical_CNN/application/
python inference.py
*****
Parameters num: 1.009633 M
ASC	Acc:  90.77 %
AEC	AUC:  0.89
PAQ_8D_AR	MSE MEAN: 1.194
pleasant_mse: 1.071 eventful_mse: 1.295 chaotic_mse: 1.123 vibrant_mse: 1.049
uneventful_mse: 1.286 calm_mse: 1.087 annoying_mse: 1.327 monotonous_mse: 1.313
``` 

### 4. MobileNetV2

```python 
cd Other_MobileNetV2/application/
python inference.py
*****
Parameters num: 2.259164 M
ASC	Acc:  89.89 %
AEC	AUC:  0.92
PAQ_8D_AR	MSE MEAN: 1.140
pleasant_mse: 0.951 eventful_mse: 1.147 chaotic_mse: 1.164 vibrant_mse: 0.986
uneventful_mse: 1.338 calm_mse: 1.120 annoying_mse: 1.173 monotonous_mse: 1.241
``` 

### 5. YAMNet

```python 
cd Other_YAMNet/application/
python inference.py
*****
Parameters num: 3.2351 M
ASC	Acc:  88.46 %
AEC	AUC:  0.91
PAQ_8D_AR	MSE MEAN: 1.205
pleasant_mse: 1.028 eventful_mse: 1.228 chaotic_mse: 1.230 vibrant_mse: 1.058
uneventful_mse: 1.388 calm_mse: 1.170 annoying_mse: 1.262 monotonous_mse: 1.275
``` 

### 6. CNN-Transformer

```python 
cd Other_CNN_Transformer/application/
python inference.py
*****
Parameters num: 12.293996 M
ASC	Acc:  92.74 %
AEC	AUC:  0.93
PAQ_8D_AR	MSE MEAN: 1.334
pleasant_mse: 1.097 eventful_mse: 1.389 chaotic_mse: 1.328 vibrant_mse: 1.285
uneventful_mse: 1.510 calm_mse: 1.239 annoying_mse: 1.360 monotonous_mse: 1.466
``` 

### 7. PANNs

1) Please download the trained model [PANNs_AS_AE_AR](https://drive.google.com/file/d/11oIX8cAmqi4a55r8fnj6nMjOA1p-OHHw/view?usp=sharing) ~304MB 
2) unzip it 
3) put the model "final_model.pth" under the "Other_PANNs\application\system\model" 

```python  
cd Other_PANNs/application/
python inference.py
*****
Parameters num: 79.731036 M
ASC	Acc:  93.13 %
AEC	AUC:  0.91
PAQ_8D_AR	MSE MEAN: 1.165
pleasant_mse: 1.010 eventful_mse: 1.165 chaotic_mse: 1.132 vibrant_mse: 1.072
uneventful_mse: 1.344 calm_mse: 1.133 annoying_mse: 1.146 monotonous_mse: 1.319
``` 
 
### 8. SoundEQnet

```python 
cd SoundEQnet/application/
python inference.py
*****
Parameters num: 2.701812 M
ASC	Acc:  95.76 %
AEC	AUC:  0.94
PAQ_8D_AR	MSE MEAN: 1.027
pleasant_mse: 0.870 eventful_mse: 1.029 chaotic_mse: 1.047 vibrant_mse: 0.965
uneventful_mse: 1.134 calm_mse: 0.967 annoying_mse: 1.062 monotonous_mse: 1.140
``` 


