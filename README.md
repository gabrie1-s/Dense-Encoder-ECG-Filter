# Dense Encoder ECG Filter
![Python 3.10](https://img.shields.io/badge/python-3.10-green.svg?style=plastic)
![Tensorflow 2.17.0](https://img.shields.io/badge/TensorFlow-2.17.0-orange.svg?style=plastic)
![cuDNN 12.3](https://img.shields.io/badge/cudnn-12.3-green.svg?style=plastic)

This is the tensorflow implementation of TiDE Filter and TiDE Classifier from the Dense Encoder ECG Filter paper, published in CinC 2024.

<p align="center">
<img src=".\imgs\tide.png" height = "480" alt="" align=center />
<br><br>
<b>Figure 1.</b> Proposed adaptations of TiDE architecture. The left model is the TiDE Classifier and the right one is the TiDE Filter.
</p>

 TiDE (Time-series Dense Encoder) is a model originally used for time series forecasting. 
 Here we adapted it for ECG filtering and ECG signal quality classification.

## Tide Classifier
The TiDE Classifier is a streamlined variant of the original TiDE model adapted for ECG signal quality classification. 
Its primary task is to precisely identify clean ECG signal segments (those suitable for further analysis).
This classifier is trained on 10-second windows of ECG signals from the BUT QDB dataset, reclassified into two categories:

* Clean: Corresponds to class 1 (where significant ECG waveforms like P, T, and QRS are visible and measurable).
* Non-clean: Corresponds to classes 2 and 3 (with high or considerable noise).

## TiDE Filter
The TiDE Filter, also a variant of the original TiDE model, is then trained filter noisy ECG signals. 
The model is trained on a dataset where artificial noise types have been added to clean ECG signals. 
The training objective is to reconstruct the clean signal from its noisy version.

## Deterministic Filter
We compared the model with what we call a Deterministic Filter, composed by: 
* Wavelet decomposition/reconstruction
* High-pass Butterwort filter
* Low-pass Butterwort filter
* Notch filter

## Filtering Results
|  |  RMSE  |  MAE  |
| --- |  ---  |  ---  |
|TiDE Filter | 0.042(±0.048)| 0.03(±0.038)|
|Deterministic Filter| 0.08(±0.18)| 0.05(±0.096)|

<p align="center">
<img src=".\imgs\clean.png" height = "200" alt="" align=center />
<br><br>
<b>(a)</b> Clean Signal
</p>

<p align="center">
<img src=".\imgs\noisy.png" height = "200" alt="" align=center />
<br><br>
<b>(b)</b> Signal with artificial noise addition
</p>

<p align="center">
<img src=".\imgs\df.png" height = "200" alt="" align=center />
<br><br>
<b>(c)</b> Output of the Deterministic Filter
</p>

<p align="center">
<img src=".\imgs\tide_f.png" height = "200" alt="" align=center />
<br><br>
<b>(d)</b> Output of the TiDE Filter
</p>

<p align="center">
<b>Figure 2.<b> Comparison between the filtering of different model
</p>
 
## References
[1] Das A, Kong W, Leach A, Mathur S, Sen R, Yu R. Long-term forecasting with tide: Time-series dense encoder.
