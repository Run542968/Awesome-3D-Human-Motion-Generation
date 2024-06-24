# Awesome-3D-Human-Motion-Generation

3D Human Motion Generation aims to generate natural and plausible motions from conditions such as text descriptions, action labels, music, etc.

This repository is built mainly to track mainstream **Text-to-Motion** works, and also contains papers and datasets related to it.

*Last updated: 2024/06/17 (CVPR'24 added)*

## Content Catalog
- [Datasets](#Datasets)
- [Performance Tables](#performance-tables)
	- Humanml3D
	- KIT-ML
- [Paper List](#paper-list)
- [Feedback](#feedback)

## Datasets

### Text-to-Motion
- **Humanml3D** | [`[project]`](https://github.com/EricGuo5513/HumanML3D) | [`[paper]`](https://openaccess.thecvf.com/content/CVPR2022/papers/Guo_Generating_Diverse_and_Natural_3D_Human_Motions_From_Text_CVPR_2022_paper.pdf)
- **KIT-ML** | [`[project]`](https://motion-annotation.humanoids.kit.edu/dataset/)
- **PoseScript** | [`[project]`](https://europe.naverlabs.com/research/computer-vision/posescript/) | [`[paper]`](https://arxiv.org/pdf/2210.11795)
- **Motion-X** | [`[project]`](https://github.com/IDEA-Research/Motion-X)| [`[paper]`](https://arxiv.org/abs/2307.00818)
- **CombatMotion** | [`[project]`](https://github.com/fyyakaxyy/AnimationGPT)

### Metrics

#### Motion quality
- **Frechet Inception Distance (FID)** $\downarrow$ 
	- FID is adopted as a principal metric to evaluate the feature distributions between the generated and real motions. The feature extractor employed is from [T2M].

#### Motion diversity
- **MultiModality (MModality)** $\uparrow$ 
	- MModality measures the generation diversity conditioned on the same text. Specifically, MModality represents the average variance for a single text prompt by computing Euclidean distances of 10 generated pairs of motions.
- **Diversity** $\rightarrow$ i.e., closer to real motion is better
	- Diversity measures the variability and richness of the generated action sequences, which is calculated by averaging Euclidean distances of random samples from 300 pairs of motion.

#### Condition matching
- **R-Precision** $\uparrow$ 
	- R-Precision measures the similarity between the text description and the generated motion sequence and indicates the probability that the real text appears in the top-k after sorting.
- **Multi-Modal Distance (MM Dist)** $\downarrow$ 
	- MM Dist represents the average Euclidean distance between the motion feature of each generated motion and the text feature of its corresponding text description in the test set.

## Performance Tables
Notably! The symbol of 'o-' and 'u-' in **Code Link** indicate the official and the unofficial implementations, respectively.
- Please note, [`[Seq2Seq]`](#1001), [`[Language2Pose]`](#1002), [`[Text2Gesture]`](#1003), [`[Hier]`](#1004) and [`[TEMOS]`](#1002) don't report results in terms of above metrics. 
	- The [`[Seq2Seq]`](#1001), [`[Language2Pose]`](#1002), [`[Text2Gesture]`](#1003) and [`[Hier]`](#1004)'s results come from [`[TM2T]`](#1003).
	- The [`[TEMOS]`](#1002)'s come from [`[MMM]`](#1001).
### Humanml3D

| ID  | Year | Venue | <div style="width: 90pt">Model<br/> (or Authors)</div>  | <div style="width: 60pt">R Precision<br/> Top-1 ↑</div> | <div style="width: 60pt">R Precision<br/> Top-2 ↑</div> | <div style="width: 60pt">R Preciion<br/> Top-3 ↑</div> | <div style="width: 60pt">FID ↓ </div> | <div style="width: 60pt">MM Dist ↓</div> | <div style="width: 90pt">MultiModality ↑</div> | <div style="width: 70pt">Diversity →</div> | <div style="width: 70pt">code</div> | - | 
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| - | - | - | [Real Motion (GT)](#1006) | 0.511 $^{\pm.003}$ | 0.703 $^{\pm.003}$ | 0.797 $^{\pm.002}$ |  0.002 $^{\pm.000}$ | 2.974 $^{\pm.008}$ | - | 9.503 $^{\pm.065}$ | - | - |
| 1 | 2018 | NeurIPS | [Seq2Seq](#1001) | 0.180 $^{\pm.002}$ | 0.300 $^{\pm.002}$ | 0.396 $^{\pm.002}$ | 11.75 $^{\pm.035}$ | 5.529 $^{\pm.007}$ | - | 6.223 $^{\pm.061}$ | [`[u-pytorch]`](https://github.com/chahuja/language2pose) | - |
| 2 | 2019 | 3DV | [Language2Pose](#1002) | 0.246 $^{\pm.002}$ | 0.387 $^{\pm.002}$ | 0.486 $^{\pm.004}$ | 11.02 $^{\pm.046}$ | 5.296 $^{\pm.008}$ | - | 7.676 $^{\pm.058}$ | [`[o-pytorch]`](https://github.com/chahuja/language2pose) | - |
| 3 | 2021 | IEEE VR | [Text2Gesture](#1003) | 0.165 $^{\pm.001}$ | 0.267 $^{\pm.002}$ | 0.345 $^{\pm.002}$ | 5.012 $^{\pm.030}$ | 6.030 $^{\pm.008}$ | - | 6.409 $^{\pm.071}$ | [`[o-pytorch]`](https://github.com/UttaranB127/Text2Gestures) | - |
| 4 | 2021 | ICCV | [Hier](#1004) | 0.301 $^{\pm.002}$ | 0.425 $^{\pm.002}$ | 0.552 $^{\pm.004}$ | 6.523 $^{\pm.024}$ | 5.012 $^{\pm.018}$ | - | 8.332 $^{\pm.042}$ | [`[o-pytorch]`](https://github.com/anindita127/Complextext2animation) | - |
| 5 | 2022 | ECCV | [TEMOS](#1005) | 0.424 $^{\pm.002}$ | 0.612 $^{\pm.002}$ | 0.722 $^{\pm.002}$ | 3.734 $^{\pm.028}$ | 3.703 $^{\pm.008}$ | 0.368 $^{\pm.018}$ | 8.973 $^{\pm.071}$ | [`[o-pytorch]`](https://github.com/Mathux/TEMOS) | - |
| 6 | 2022 | ECCV | [TM2T](#1006) | 0.424 $^{\pm.003}$ | 0.618 $^{\pm.003}$ | 0.729 $^{\pm.002}$ | 1.501 $^{\pm.017}$ | 3.467 $^{\pm.011}$ | 2.424 $^{\pm.093}$ | 8.589 $^{\pm.076}$ | [`[o-pytorch]`](https://github.com/EricGuo5513/TM2T) | - |


| 2 | 2024 | CVPR | [MMM](#1001) | 0.504 $^{\pm.003}$ | 0.696 $^{\pm.003}$ | 0.794 $^{\pm.002}$ | 0.080 $^{\pm.003}$ | 2.998 $^{\pm.007}$ | 1.164 $^{\pm.041}$ | 9.411 $^{\pm.058}$ | [`[o-pytorch]`](https://github.com/exitudio/MMM/) | - |

### KIT-ML

| ID  | Year | Venue | <div style="width: 90pt">Model<br/> (or Authors)</div>  | <div style="width: 60pt">R Precision<br/> Top-1 ↑</div> | <div style="width: 60pt">R Precision<br/> Top-2 ↑</div> | <div style="width: 60pt">R Preciion<br/> Top-3 ↑</div> | <div style="width: 60pt">FID ↓ </div> | <div style="width: 60pt">MM Dist ↓</div> | <div style="width: 90pt">MultiModality ↑</div> | <div style="width: 70pt">Diversity →</div> | <div style="width: 70pt">code</div> | - | 
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| - | - | - | [Real Motion (GT)](#1006) | 0.424 $^{\pm.005}$ | 0.649 $^{\pm.006}$ | 0.779 $^{\pm.006}$ |  0.031 $^{\pm.004}$ | 2.788 $^{\pm.012}$ | - | 11.08 $^{\pm.097}$ | - | - |
| 1 | 2018 | NeurIPS | [Seq2Seq](#1001) | 0.103 $^{\pm.003}$ | 0.178 $^{\pm.005}$ | 0.241 $^{\pm.006}$ | 24.86 $^{\pm.348}$ | 7.960 $^{\pm.031}$ | - | 6.744 $^{\pm.106}$ | [`[u-pytorch]`](https://github.com/chahuja/language2pose) | - |
| 2 | 2019 | 3DV | [Language2Pose](#1002) | 0.221 $^{\pm.005}$ | 0.373 $^{\pm.004}$ | 0.483 $^{\pm.005}$ | 6.545 $^{\pm.072}$ | 5.147 $^{\pm.030}$ | - | 9.073 $^{\pm.100}$ | [`[o-pytorch]`](https://github.com/chahuja/language2pose) | - |
| 3 | 2021 | IEEE VR | [Text2Gesture](#1003) | 0.156 $^{\pm.004}$ | 0.255 $^{\pm.004}$ | 0.338 $^{\pm.005}$ | 12.12 $^{\pm.183}$ | 6.964 $^{\pm.029}$ | - | 9.334 $^{\pm.079}$ | [`[o-pytorch]`](https://github.com/UttaranB127/Text2Gestures) | - |
| 4 | 2021 | ICCV | [Hier](#1004) | 0.255 $^{\pm.006}$ | 0.432 $^{\pm.007}$ | 0.531 $^{\pm.007}$ | 5.203 $^{\pm.107}$ | 4.986 $^{\pm.027}$ | - | 9.563 $^{\pm.072}$ | [`[o-pytorch]`](https://github.com/anindita127/Complextext2animation) | - |
| 5 | 2022 | ECCV | [TEMOS](#1005) | 0.353 $^{\pm.006}$ | 0.561 $^{\pm.007}$ | 0.687 $^{\pm.005}$ | 3.717 $^{\pm.051}$ | 3.417 $^{\pm.017}$ | 0.532 $^{\pm.034}$ | 10.84 $^{\pm.100}$ | [`[o-pytorch]`](https://github.com/Mathux/TEMOS) | - |
| 6 | 2022 | ECCV | [TM2T](#1006) | 0.280 $^{\pm.005}$ | 0.463 $^{\pm.006}$ | 0.587 $^{\pm.005}$ | 3.599 $^{\pm.153}$ | 4.591 $^{\pm.026}$ | 3.292 $^{\pm.081}$ | 9.473 $^{\pm.117}$ | [`[o-pytorch]`](https://github.com/EricGuo5513/TM2T) | - |





## Paper List
1. <span id = "1001">**[Seq2Seq]**</span> | **NeurIPS'18** | Generating Animated Videos of Human Activities from Natural Language Descriptions | [`[pdf]`](https://nips2018vigil.github.io/static/papers/accepted/9.pdf) | [`[u-pytorch]`](https://github.com/chahuja/language2pose) |
2. <span id = "1002">**[Language2Pose]**</span> | **3DV'19** | Language2Pose: Natural Language Grounded Pose Forecasting | [`[pdf]`](https://arxiv.org/pdf/1907.01108) | [`[o-pytorch]`](https://github.com/chahuja/language2pose) |

3. <span id = "1003">**[Text2Gesture]**</span> | **IEEE VR'21** | Text2Gestures: A Transformer-Based Network for Generating Emotive Body Gestures for Virtual Agents | [`[pdf]`](https://arxiv.org/pdf/2101.11101) | [`[o-pytorch]`](https://github.com/UttaranB127/Text2Gestures) |

4. <span id = "1004">**[Hier]**</span> | **ICCV'21** | Synthesis of Compositional Animations from Textual Descriptions | [`[pdf]`](https://arxiv.org/pdf/2103.14675) | [`[o-pytorch]`](https://github.com/anindita127/Complextext2animation) |
5. <span id = "1005">**[TEMOS]**</span> | **ECCV'22** | TEMOS: Generating diverse human motions from textual descriptions | [`[pdf]`](https://arxiv.org/pdf/2204.14109) | [`[o-pytorch]`](https://github.com/Mathux/TEMOS) |
6. <span id = "1006">**[TM2T]**</span> | **ECCV'22** | TM2T: Stochastic and Tokenized Modeling for the Reciprocal Generation of 3D Human Motions and Texts | [`[pdf]`](https://arxiv.org/pdf/2207.01696) | [`[o-pytorch]`](https://github.com/EricGuo5513/TM2T) |

1. <span id = "1001">**[MMM]**</span> | **CVPR'24** | MMM: Generative Masked Motion Model | [`[pdf]`](https://arxiv.org/pdf/2312.03596) | [`[o-pytorch]`](https://github.com/exitudio/MMM/) |

## Feedback

If you have any suggestions or find missing papers, please feel free to contact me.

- [e-mail](mailto:run542968@gmail.com)
- [pull request](https://github.com/Run542968/Awesome-3D-Human-Motion-Generation/pulls)

## Thanks
This format of this awesome follows [this project](https://github.com/Pilhyeon/Awesome-Weakly-Supervised-Temporal-Action-Localization), thanks for such a pretty template!