# What is mID?

Cyber-theft of trade secrets has become a serious business threat. Digital watermarking is a popular technique to assist in identifying the source of the file leakage, whereby a unique watermark for each insider is hidden in sensitive files. However, malicious insiders may use their smartphones to photograph the secret file displayed on screens to remove the embedded hidden digital watermarks due to the optical
noises introduced during photographing. To identify the leakage source despite such screen-photo-based leakage attacks, we leverage Moiré pattern, an optical phenomenon resulted from the optical interaction between electronic screens and cameras. As such, we present mID, a new watermark-like technique that can create a carefully crafted Moiré pattern on the photo when it is taken towards the screen. We design patterns that appear to be natural yet can be linked to the identity of the leaker.We implemented mID and evaluate it with 5 display devices and 6 smartphones from various manufacturers and models. The results demonstrate that mID can achieve an average bit error rate (BER) of 0:6% and can successfully identify an ID with an average accuracy of 96%, with little influence from the type of display devices, cameras, IDs, and ambient lights. 

## How does mID work?

<img src="./images/scene.png" alt="attack" width="600px" />
Once an adversary logs into a computer or an application (e.g., an email system) with her account, mID will modify the displayed content slightly based on her identity (ID), such that when she takes pictures of the screen, the modification will create Moiré patterns in the photos. Finally, the embedded Moiré patterns are decoded to obtain the ID.

# Background

## Moiré Pattern

<img src="./images/moirepattern.png" alt="overview" width="600px" />
Moiré patterns or Moiré fringes are interference patterns created when opaque ruled patterns with transparent gaps are overlaid. Digital cameras often cause Moiré patterns when taking pictures of digital screens, e.g., TV screens or liquid-crystal displays (LCDs). The nonlinearity arises from the interference of digital screens and the Color Filter Array (CFA) on the camera image sensors, as shown in the Figure.

## Threat Model

- Screen-capturing with Smartphones.
- Untraceability over Internet.
- Photo Processing.

## Overview of mID

<img src="./images/overview.png" alt="overview" width="600px" />
mID scheme consists of encoding and decoding phases with four modules: (a) mID generation, (b) mID embedding, (c) mID extraction, and (d) mID decoding, as shown in the figure.

In the encoding phase, the mID Generation module first creates the modification that will be applied to the original display based on the IDs, and the mID Embedding module will find the best areas to apply such modification. The design goal of the encoding phase is that the modification cannot be observed visually by users but will be captured by cameras and form a seemingly natural Moiré pattern, i.e., mID. The mID Generation consists of (a) mID Framing that forms a proper frame, (b) Grating Generation that helps to create Moiré patterns, and (c) ID Encoding that adds the information of IDs to the Moiré patterns. Note that designing grating is similar to finding the carrier signals and the ID encoding is similar to finding the modulation scheme in communication. 

To generate Moiré patterns, the screen pixels are manipulated to form a display grating, which has a periodic structure and may appear as stripes. To make the patterns looks as if they are naturally generated, the display grating is designed to be vertical since the LCD panel has a vertical grating structure. Second, to encode the mID into the display grating without noticed by users, we propose a discretized bipolar non-returnto-zero encoding method, which manipulates the intensity levels of the generated Moiré patterns to represent information. As humans perceive light and color in a non-linear manner, we correct the luminance difference caused by the discretized encoding to ensure user visual uniformity. Third, to embed the generated gratings into the screen and maximize their possibility of being captured in the photos, we automatically analyze the current page of the screen and search for suitable regions for embedding.

In the decoding phase, for a given screen photo that contains embedded mID, the mID Extraction module tries to remove the camera distortion with image rectification and extracts the regions of Moiré patterns, i.e., Moiré areas, with window scanning. Then, we recover the embedded identity numbers via the mID Decoding module, in which we first transform the Moiré areas into the HSV (hue, saturation, value) color space, then perform saturation balance and enlargement for image pre-processing, and finally recover mID via k-means clustering with the assistance of check codes.

# Performance

We conduct experiments under various settings and collect over 5000 photos with 5 display devices and 6 smartphones over 3 months.

* mID achieves an average BER of 0.6% and an average NER of 4.0%, which demonstrates promises towards
screen photo forensics.
* mID performs well with little influence from the type of display devices, cameras, IDs, and ambient lights.
* mID performs well at a shooting distance of (60cm;80cm) and a shooting angle of (-20°;20°),
which are within the possible attack distances and angles adopted by adversaries as suggested by the theoretical calculation.

<img src="./images/eva_total.png" alt="moire" width="600px" />

# Citation

```
@inproceedings{cheng2021mid,
  title={mID: Tracing Screen Photos via Moir{\'e} Patterns},
  author={Cheng, Yushi and Ji, Xiaoyu and Wang, Lixu and Pang, Qi and Chen, Yi-Chao and Xu, Wenyuan},
  booktitle={30th $\{$USENIX$\}$ Security Symposium ($\{$USENIX$\}$ Security 21)},
  year={2021}
}
```

# Contact
* Prof. Wenyuan Xu (<wyxu@zju.edu.cn>)
* Prof. Xiaoyu Ji (<xji@zju.edu.cn>)
* Dr. Yushi Cheng (yushicheng@zju.edu.cn)

# Powered by

<table bgcolor="white">
<tr valign="middle">
<td width="50%" align="center" colspan="2">
 <a href="http://usslab.org">Ubiquitous System Security Laboratory (USSLab) 
</td>
<td width="50%" align="center" colspan="2">
  <a href="http://www.zju.edu.cn/english">Zhejiang University 
</td>
</tr>
<tr valign="middle">
<td width="50%" align="center" colspan="2">
  <a href="http://usslab.org"></a>
  <a href="http://usslab.org"><img 
src="./images/usslab_logo.png" height="80"></a>
</td>
<td width="50%" align="center" colspan="2">
  <a href="http://www.zju.edu.cn/english/"></a>
  <a href="http://www.zju.edu.cn/english/"><img 
src="./images/zju_logo.png" height="80"></a>
</td>
</tr>
</table>
