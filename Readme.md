# SoundScape Describer (SSD): Soundscape Captioning with Sound Emotional Quality Network and Large Language Model

## Introduction

### 1. SSD Training steps

1\) Download and prepare the dataset in [Dataset_ARAUS](Dataset_ARAUS); ARAUS can be downloaded [ARAUS_repository](https://github.com/ntudsp/araus-dataset-baseline-models/tree/main). <br> The labels of our annotated acoustic scenes and audio events are in [Dataset_ARAUS](Dataset_ARAUS).


2\) Use the code in [Feature_log_mel](Feature_log_mel) to extract log mel acoustic features. <br> Use the code in [Feature_loudness_ISO532_1](Feature_loudness_ISO532_1) to extract the ISO 532-1:2017 standard loudness features.

3\) Use the code in [Model_SoundEQnet](Model_SoundEQnet) to train SoundEQnet.
  
4\) In [LLM_scripts](LLM_scripts), read the audio scene, audio events, and PAQ 8-dimensional affective response corresponding to the test audio predicted by the trained SoundEQnet, and then output the corresponding soundscape descriptions. <br> Please fill in your OpenAI username and password in [LLM_scripts](LLM_scripts).

### 2. Expert evaluation of SSD soundscape caption quality

[Human_assessment](Human_assessment) contains 

1) a call for experiment; 

2) assessment raw materials: assessment dataset; participant instruction file; local and online questionnaires; 

3) assessment statistical results from a jury composed of 16 audio/soundscape experts.

<!-- 
### 3. LLM-SSD One Run

[One_Run](One_Run) provides the scripts to convert target audio clips directly into soundscape descriptions for easy inference-only use.

If you want to skip the tedious training steps and use LLM-SSD directly, go directly to [One_Run](One_Run).

Please fill in your OpenAI username and password in LLM_scripts.
-->

### 3. Other models
  
The trained models of the other 7 models in the paper have been attached to their respective folders. 

If you want to train them yourself, please follow the SSD training steps.

<br>

## Figure

### 1. Overall framework of the soundscape describer SSD

<h3 align="center"> <p></p></h3>
<div align="center">
<img src="Figure/LLM_SSD.png" width=100%/> 
</div>  

<br>

### 2. The acoustic model SoundEQnet simultaneously models acoustic scene (AS), audio event (AE), and emotion-related affective response (AR)

<h3 align="center"> <p></p></h3>
<div align="center">
<img src="Figure/SoundEQnet.png" width=100%/> 
</div> 

<br>

### 3. Process of the LLM part in the soundscape describer SSD
<h3 align="center"> <p></p></h3>
<div align="center">
<img src="Figure/LLM_part.png" width=100%/> 
</div> 



## Run models

```1) Unzip the Dataset under the application folder```

```2) Unzip the Pretrained_models under the application folder```

```3) Enter the application folder: cd application```


```python 
cd Other_ARAUS_CNN/application/
python inference.py
----------------------------------------------------------------------------------------
ASC	Acc:  87.95%
AEC	AUC:  0.85
PAQ_8D_AR	MEAN MSE: 1.196
pleasant_mse: 1.101 eventful_mse: 1.174 chaotic_mse: 1.154 vibrant_mse: 1.125 uneventful_mse: 1.302 calm_mse: 1.183 annoying_mse: 1.206 monotonous_mse: 1.319
``` 





