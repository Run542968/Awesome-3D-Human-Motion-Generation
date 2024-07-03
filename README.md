# Awesome-3D-Human-Motion-Generation

3D Human Motion Generation aims to generate natural and plausible motions from conditions such as text descriptions, action labels, music, etc.

This repository is built mainly to track mainstream **Text-to-Motion** works, and also contains papers and datasets related to it.

*Last updated: 2024/07/03 (Partial ECCV'24 added)*

## Content Catalog
- [Datasets](#Datasets)
- [Metircs](#metrics)
- [Performance Tables](#performance-tables)
	- [Humanml3D](#humanml3d)
	- [KIT-ML](#kit-ml)
- [Paper List](#paper-list)
- [Feedback](#feedback)

## Datasets

### Text-to-Motion
- **Humanml3D** | [`[project]`](https://github.com/EricGuo5513/HumanML3D) | [`[paper]`](https://openaccess.thecvf.com/content/CVPR2022/papers/Guo_Generating_Diverse_and_Natural_3D_Human_Motions_From_Text_CVPR_2022_paper.pdf)
- **KIT-ML** | [`[project]`](https://motion-annotation.humanoids.kit.edu/dataset/)
- **PoseScript** | [`[project]`](https://europe.naverlabs.com/research/computer-vision/posescript/) | [`[paper]`](https://arxiv.org/pdf/2210.11795)
- **Motion-X** | [`[project]`](https://github.com/IDEA-Research/Motion-X)| [`[paper]`](https://arxiv.org/abs/2307.00818)
- **CombatMotion** | [`[project]`](https://github.com/fyyakaxyy/AnimationGPT)

## Metrics

### Motion quality
- **Frechet Inception Distance (FID)** $\downarrow$ 
	- FID is adopted as a principal metric to evaluate the feature distributions between the generated and real motions. The feature extractor employed is from [T2M].

### Motion diversity
- **MultiModality (MModality)** $\uparrow$ 
	- MModality measures the generation diversity conditioned on the same text. Specifically, MModality represents the average variance for a single text prompt by computing Euclidean distances of 10 generated pairs of motions.
- **Diversity** $\rightarrow$ i.e., closer to real motion is better
	- Diversity measures the variability and richness of the generated action sequences, which is calculated by averaging Euclidean distances of random samples from 300 pairs of motion.

### Condition matching
- **R-Precision** $\uparrow$ 
	- R-Precision measures the similarity between the text description and the generated motion sequence and indicates the probability that the real text appears in the top-k after sorting.
- **Multi-Modal Distance (MM Dist)** $\downarrow$ 
	- MM Dist represents the average Euclidean distance between the motion feature of each generated motion and the text feature of its corresponding text description in the test set.

## Performance Tables
Notably! The symbol of 'o-' and 'u-' in **Code Link** indicate the official and the unofficial implementations, respectively.
- Please note, [`[Seq2Seq]`](#1001), [`[Language2Pose]`](#1002), [`[Text2Gesture]`](#1003), [`[Hier]`](#1004) and [`[TEMOS]`](#1005) don't report results in terms of above metrics. 
	- The [`[Seq2Seq]`](#1001), [`[Language2Pose]`](#1002), [`[Text2Gesture]`](#1003) and [`[Hier]`](#1004)'s results come from [`[TM2T]`](#1006).
	- The [`[TEMOS]`](#1005)'s come from [`[MMM]`](#1017).
- &dagger;: denotes a different evaluator is used.
### Humanml3D

| ID  | Year | Venue | <div style="width: 90pt">Model<br/> (or Authors)</div>  | <div style="width: 60pt">R Precision<br/> Top-1 ↑</div> | <div style="width: 60pt">R Precision<br/> Top-2 ↑</div> | <div style="width: 60pt">R Preciion<br/> Top-3 ↑</div> | <div style="width: 60pt">FID ↓ </div> | <div style="width: 60pt">MM Dist ↓</div> | <div style="width: 90pt">MultiModality ↑</div> | <div style="width: 70pt">Diversity →</div> | <div style="width: 70pt">code</div> | - | 
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| - | - | - | [Real Motion](#1006) | $0.511^{\pm.003}$ | $0.703^{\pm.003}$ | $0.797^{\pm.002}$ | $0.002^{\pm.000}$ | $2.974^{\pm.008}$ | - | $9.503^{\pm.065}$ | - | - |
| - | - | - | [Real Motion &dagger;](#10016) | $0.539^{\pm.004}$ | $0.721^{\pm.003}$ | $0.810^{\pm.003}$ | $0.001^{\pm.000}$ | $1.462^{\pm.006}$ | - | $5.298^{\pm.047}$ | - | - |
| 1 | 2018 | NeurIPS | [Seq2Seq](#1001) | $0.180^{\pm.002}$ | $0.300^{\pm.002}$ | $0.396^{\pm.002}$ | $11.75^{\pm.035}$ | $5.529^{\pm.007}$ | - | $6.223^{\pm.061}$ | [`[u-pytorch]`](https://github.com/chahuja/language2pose) | - |
| 2 | 2019 | 3DV | [Language2Pose](#1002) | $0.246^{\pm.002}$ | $0.387^{\pm.002}$ | $0.486^{\pm.004}$ | $11.02^{\pm.046}$ | $5.296^{\pm.008}$ | - | $7.676^{\pm.058}$ | [`[o-pytorch]`](https://github.com/chahuja/language2pose) | - |
| 3 | 2021 | IEEE VR | [Text2Gesture](#1003) | $0.165^{\pm.001}$ | $0.267^{\pm.002}$ | $0.345^{\pm.002}$ | $5.012^{\pm.030}$ | $6.030^{\pm.008}$ | - | $6.409^{\pm.071}$ | [`[o-pytorch]`](https://github.com/UttaranB127/Text2Gestures) | - |
| 4 | 2021 | ICCV | [Hier](#1004) | $0.301^{\pm.002}$ | $0.425^{\pm.002}$ | $0.552^{\pm.004}$ | $6.523^{\pm.024}$ | $5.012^{\pm.018}$ | - | $8.332^{\pm.042}$ | [`[o-pytorch]`](https://github.com/anindita127/Complextext2animation) | - |
| 5 | 2022 | ECCV | [TEMOS](#1005) | $0.424^{\pm.002}$ | $0.612^{\pm.002}$ | $0.722^{\pm.002}$ | $3.734^{\pm.028}$ | $3.703^{\pm.008}$ | $0.368^{\pm.018}$ | $8.973^{\pm.071}$ | [`[o-pytorch]`](https://github.com/Mathux/TEMOS) | - |
| 6 | 2022 | ECCV | [TM2T](#1006) | $0.424^{\pm.003}$ | $0.618^{\pm.003}$ | $0.729^{\pm.002}$ | $1.501^{\pm.017}$ | $3.467^{\pm.011}$ | $2.424^{\pm.093}$ | $8.589^{\pm.076}$ | [`[o-pytorch]`](https://github.com/EricGuo5513/TM2T) | - |
| 7 | 2022 | CVPR | [T2M](#1007) | $0.455^{\pm.003}$ | $0.636^{\pm.003}$ | $0.736^{\pm.002}$ | $1.087^{\pm.021}$ | $3.347^{\pm.008}$ | $2.219^{\pm.074}$ | $9.175^{\pm.083}$ | [`[o-pytorch]`](https://github.com/EricGuo5513/text-to-motion) | - |
| 8 | 2023 | ICLR | [MDM](#1008) | $0.320^{\pm.005}$ | $0.498^{\pm.004}$ | $0.611^{\pm.007}$ | $0.544^{\pm.044}$ | $5.566^{\pm.027}$ | $2.799^{\pm.072}$ | $9.559^{\pm.086}$ | [`[o-pytorch]`](https://github.com/GuyTevet/motion-diffusion-model) | - |
| 9 | 2022 (2024) | Arxiv (TPAMI) | [MOtionDiffuse](#1009) | $0.491^{\pm.001}$ | $0.681^{\pm.001}$ | $0.782^{\pm.001}$ | $0.630^{\pm.001}$ | $3.113^{\pm.001}$ | $1.553^{\pm.042}$ | $9.410^{\pm.049}$ | [`[o-pytorch]`](https://github.com/mingyuan-zhang/MotionDiffuse) | - |
| 10 | 2023 | CVPR | [MLD](#1010) | $0.481^{\pm.003}$ | $0.673^{\pm.003}$ | $0.772^{\pm.002}$ | $0.473^{\pm.013}$ | $3.196^{\pm.010}$ | $2.413^{\pm.079}$ | $9.724^{\pm.082}$ | [`[o-pytorch]`](https://github.com/chenfengye/motion-latent-diffusion) | - |
| 11 | 2023 | CVPR | [T2M-GPT](#1011) | $0.491^{\pm.003}$ | $0.680^{\pm.003}$ | $0.775^{\pm.002}$ | $0.116^{\pm.004}$ | $3.118^{\pm.011}$ | $1.856^{\pm.011}$ | $9.761^{\pm.081}$ | [`[o-pytorch]`](https://github.com/Mael-zys/T2M-GPT) | - |
| 12 | 2023 | ICCV | [Fg-T2M](#1012) | $0.492^{\pm.002}$ | $0.683^{\pm.003}$ | $0.783^{\pm.002}$ | $0.243^{\pm.019}$ | $3.109^{\pm.007}$ | $1.614^{\pm.049}$ | $9.278^{\pm.072}$ | - | - |
| 13 | 2023 | ICCV | [M2DM](#1013) | $0.497^{\pm.003}$ | $0.682^{\pm.002}$ | $0.763^{\pm.003}$ | $0.352^{\pm.005}$ | $3.134^{\pm.010}$ | $3.587^{\pm.072}$ | $9.926^{\pm.073}$ | - | - |
| 14 | 2023 | ICCV | [AttT2M](#1014) | $0.499^{\pm.003}$ | $0.690^{\pm.002}$ | $0.786^{\pm.002}$ | $0.112^{\pm.006}$ | $3.038^{\pm.007}$ | $2.452^{\pm.051}$ | $9.700^{\pm.090}$ | [`[o-pytorch]`](https://github.com/ZcyMonkey/AttT2M) | - |
| 15 | 2023 | NeurIPS | [MotionGPT](#1015) | $0.492^{\pm.003}$ | $0.681^{\pm.003}$ | $0.778^{\pm.002}$ | $0.232^{\pm.008}$ | $3.096^{\pm.008}$ | $2.008^{\pm.084}$ | $9.528^{\pm.071}$ | [`[o-pytorch]`](https://github.com/OpenMotionLab/MotionGPT) | - |
| 16 | 2023 | NeurIPS | [ReMoDiffuse &dagger;](#1016) | $0.510^{\pm.005}$ | $0.698^{\pm.006}$ | $0.795^{\pm.004}$ | $0.103^{\pm.004}$ | $2.974^{\pm.016}$ | $1.795^{\pm.043}$ | $9.018^{\pm.075}$ | [`[o-pytorch]`](https://github.com/mingyuan-zhang/ReMoDiffuse) | - |
| 17 | 2024 | CVPR | [MMM](#1017) | $0.504^{\pm.003}$ | $0.696^{\pm.003}$ | $0.794^{\pm.002}$ | $0.080^{\pm.003}$ | $2.998^{\pm.007}$ | $1.164^{\pm.041}$ | $9.411^{\pm.058}$ | [`[o-pytorch]`](https://github.com/exitudio/MMM/) | - |
| 18 | 2024 | CVPR | [MoMask](#1018) | $0.521^{\pm.002}$ | $0.713^{\pm.002}$ | $0.807^{\pm.002}$ | $0.045^{\pm.002}$ | $2.958^{\pm.008}$ | $1.241^{\pm.040}$ | - | [`[o-pytorch]`](https://github.com/EricGuo5513/momask-codes) | - |
| 19 | 2024 | ECCV | [MotionLCM](#1019) | $0.502^{\pm.003}$ | $0.698^{\pm.002}$ | $0.798^{\pm.002}$ | $0.304^{\pm.012}$ | $3.012^{\pm.007}$ | $2.259^{\pm.092}$ | $9.607^{\pm.066}$ | [`[o-pytorch]`](https://github.com/Dai-Wenxun/MotionLCM) | - |
| 20 | 2024 | ECCV | [Motion Mamba](#1020) | $0.502^{\pm.003}$ | $0.693^{\pm.002}$ | $0.792^{\pm.002}$ | $0.281^{\pm.009}$ | $3.060^{\pm.058}$ | $2.294^{\pm.058}$ | $9.871^{\pm.084}$ | [`[o-pytorch]`](https://github.com/steve-zeyu-zhang/MotionMamba/) | - |



### KIT-ML

| ID  | Year | Venue | <div style="width: 90pt">Model<br/> (or Authors)</div>  | <div style="width: 60pt">R Precision<br/> Top-1 ↑</div> | <div style="width: 60pt">R Precision<br/> Top-2 ↑</div> | <div style="width: 60pt">R Preciion<br/> Top-3 ↑</div> | <div style="width: 60pt">FID ↓ </div> | <div style="width: 60pt">MM Dist ↓</div> | <div style="width: 90pt">MultiModality ↑</div> | <div style="width: 70pt">Diversity →</div> | <div style="width: 70pt">code</div> | - | 
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| - | - | - | [Real Motion (GT)](#1006) | $0.424^{\pm.005}$ | $0.649^{\pm.006}$ | $0.779^{\pm.006}$ | $0.031^{\pm.004}$ | $2.788^{\pm.012}$ | - | $11.08^{\pm.097}$ | - | - |
| - | - | - | [Real Motion &dagger;](#10016) | $0.475^{\pm.006}$ | $0.690^{\pm.004}$ | $0.791^{\pm.005}$ | $0.002^{\pm.000}$ | $1.337^{\pm.012}$ | - | $6.371^{\pm.058}$ | - | - |
| 1 | 2018 | NeurIPS | [Seq2Seq](#1001) | $0.103^{\pm.003}$ | $0.178^{\pm.005}$ | $0.241^{\pm.006}$ | $24.86^{\pm.348}$ | $7.960^{\pm.031}$ | - | $6.744^{\pm.106}$ | [`[u-pytorch]`](https://github.com/chahuja/language2pose) | - |
| 2 | 2019 | 3DV | [Language2Pose](#1002) | $0.221^{\pm.005}$ | $0.373^{\pm.004}$ | $0.483^{\pm.005}$ | $6.545^{\pm.072}$ | $5.147^{\pm.030}$ | - | $9.073^{\pm.100}$ | [`[o-pytorch]`](https://github.com/chahuja/language2pose) | - |
| 3 | 2021 | IEEE VR | [Text2Gesture](#1003) | $0.156^{\pm.004}$ | $0.255^{\pm.004}$ | $0.338^{\pm.005}$ | $12.12^{\pm.183}$ | $6.964^{\pm.029}$ | - | $9.334^{\pm.079}$ | [`[o-pytorch]`](https://github.com/UttaranB127/Text2Gestures) | - |
| 4 | 2021 | ICCV | [Hier](#1004) | $0.255^{\pm.006}$ | $0.432^{\pm.007}$ | $0.531^{\pm.007}$ | $5.203^{\pm.107}$ | $4.986^{\pm.027}$ | - | $9.563^{\pm.072}$ | [`[o-pytorch]`](https://github.com/anindita127/Complextext2animation) | - |
| 5 | 2022 | ECCV | [TEMOS](#1005) | $0.353^{\pm.006}$ | $0.561^{\pm.007}$ | $0.687^{\pm.005}$ | $3.717^{\pm.051}$ | $3.417^{\pm.017}$ | $0.532^{\pm.034}$ | $10.84^{\pm.100}$ | [`[o-pytorch]`](https://github.com/Mathux/TEMOS) | - |
| 6 | 2022 | ECCV | [TM2T](#1006) | $0.280^{\pm.005}$ | $0.463^{\pm.006}$ | $0.587^{\pm.005}$ | $3.599^{\pm.153}$ | $4.591^{\pm.026}$ | $3.292^{\pm.081}$ | $9.473^{\pm.117}$ | [`[o-pytorch]`](https://github.com/EricGuo5513/TM2T) | - |
| 7 | 2022 | CVPR | [T2M](#1007) | $0.361^{\pm.006}$ | $0.559^{\pm.007}$ | $0.681^{\pm.007}$ | $3.022^{\pm.107}$ | $3.488^{\pm.028}$ | $2.052^{\pm.107}$ | $10.72^{\pm.145}$ | [`[o-pytorch]`](https://github.com/EricGuo5513/text-to-motion) | - |
| 8 | 2023 | ICLR | [MDM](#1008) | $0.164^{\pm.004}$ | $0.291^{\pm.004}$ | $0.396^{\pm.004}$ | $0.497^{\pm.021}$ | $9.191^{\pm.022}$ | $1.907^{\pm.214}$ | $10.85^{\pm.109}$ | [`[o-pytorch]`](https://github.com/GuyTevet/motion-diffusion-model) | - |
| 9 | 2022 (2024) | Arxiv (TPAMI) | [MOtionDiffuse](#1009) | $0.417^{\pm.004}$ | $0.621^{\pm.004}$ | $0.739^{\pm.004}$ | $1.954^{\pm.064}$ | $2.958^{\pm.005}$ | $0.730^{\pm.013}$ | $11.10^{\pm.143}$ | [`[o-pytorch]`](https://github.com/mingyuan-zhang/MotionDiffuse) | - |
| 10 | 2023 | CVPR | [MLD](#1010) | $0.390^{\pm.008}$ | $0.609^{\pm.008}$ | $0.734^{\pm.007}$ | $0.404^{\pm.027}$ | $3.204^{\pm.027}$ | $2.192^{\pm.071}$ | $10.80^{\pm.117}$ | [`[o-pytorch]`](https://github.com/chenfengye/motion-latent-diffusion) | - |
| 11 | 2023 | CVPR | [T2M-GPT](#1011) | $0.402^{\pm.006}$ | $0.619^{\pm.005}$ | $0.737^{\pm.006}$ | $0.717^{\pm.041}$ | $3.053^{\pm.026}$ | $1.912^{\pm.036}$ | $10.86^{\pm.094}$ | [`[o-pytorch]`](https://github.com/Mael-zys/T2M-GPT) | - |
| 12 | 2023 | ICCV | [Fg-T2M](#1012) | $0.418^{\pm.005}$ | $0.626^{\pm.004}$ | $0.745^{\pm.004}$ | $0.571^{\pm.047}$ | $3.114^{\pm.015}$ | $1.019^{\pm.029}$ | $10.93^{\pm.083}$ | - | - |
| 13 | 2023 | ICCV | [M2DM](#1013) | $0.416^{\pm.004}$ | $0.628^{\pm.004}$ | $0.743^{\pm.004}$ | $0.515^{\pm.029}$ | $3.015^{\pm.017}$ | $3.325^{\pm.370}$ | $11.417^{\pm.970}$ | - | - |
| 14 | 2023 | ICCV | [AttT2M](#1014) | $0.413^{\pm.006}$ | $0.632^{\pm.006}$ | $0.751^{\pm.006}$ | $0.870^{\pm.039}$ | $3.039^{\pm.021}$ | $2.281^{\pm.047}$ | $10.96^{\pm.123}$ | [`[o-pytorch]`](https://github.com/ZcyMonkey/AttT2M) | - |
| 15 | 2023 | NeurIPS | [MotionGPT](#1015) | $0.366^{\pm.005}$ | $0.558^{\pm.004}$ | $0.680^{\pm.005}$ | $0.510^{\pm.016}$ | $3.527^{\pm.021}$ | $2.328^{\pm.117}$ | $10.35^{\pm.084}$ | [`[o-pytorch]`](https://github.com/OpenMotionLab/MotionGPT) | - |
| 16 | 2023 | NeurIPS | [ReMoDiffuse &dagger;](#1016) | $0.427^{\pm.014}$ | $0.641^{\pm.004}$ | $0.765^{\pm.055}$ | $0.155^{\pm.006}$ | $2.814^{\pm.012}$ | $1.239^{\pm.028}$ | $10.80^{\pm.105}$ | [`[o-pytorch]`](https://github.com/mingyuan-zhang/ReMoDiffuse) | - |
| 17 | 2024 | CVPR | [MMM](#1017) | $0.381^{\pm.005}$ | $0.590^{\pm.006}$ | $0.718^{\pm.005}$ | $0.429^{\pm.019}$ | $3.146^{\pm.019}$ | $1.105^{\pm.026}$ | $10.633^{\pm.097}$ | [`[o-pytorch]`](https://github.com/exitudio/MMM/) | - |
| 18 | 2024 | CVPR | [MoMask](#1018) | $0.433^{\pm.007}$ | $0.656^{\pm.005}$ | $0.781^{\pm.005}$ | $0.204^{\pm.011}$ | $2.779^{\pm.022}$ | $1.131^{\pm.043}$ | - | [`[o-pytorch]`](https://github.com/EricGuo5513/momask-codes) | - |
| 19 | 2024 | ECCV | [Motion Mamba](#1020) | $0.419^{\pm.006}$ | $0.645^{\pm.005}$ | $0.765^{\pm.006}$ | $0.307^{\pm.041}$ | $3.021^{\pm.025}$ | $1.678^{\pm.064}$ | $11.02^{\pm.098}$ | [`[o-pytorch]`](https://github.com/steve-zeyu-zhang/MotionMamba/) | - |



## Paper List
### Text-to-Motion
1. <span id = "1001">**[Seq2Seq]**</span> | **NeurIPS'18** | Generating Animated Videos of Human Activities from Natural Language Descriptions | [`[pdf]`](https://nips2018vigil.github.io/static/papers/accepted/9.pdf) | [`[u-pytorch]`](https://github.com/chahuja/language2pose) |
2. <span id = "1002">**[Language2Pose]**</span> | **3DV'19** | Language2Pose: Natural Language Grounded Pose Forecasting | [`[pdf]`](https://arxiv.org/pdf/1907.01108) | [`[o-pytorch]`](https://github.com/chahuja/language2pose) |
3. <span id = "1003">**[Text2Gesture]**</span> | **IEEE VR'21** | Text2Gestures: A Transformer-Based Network for Generating Emotive Body Gestures for Virtual Agents | [`[pdf]`](https://arxiv.org/pdf/2101.11101) | [`[o-pytorch]`](https://github.com/UttaranB127/Text2Gestures) |
4. <span id = "1004">**[Hier]**</span> | **ICCV'21** | Synthesis of Compositional Animations from Textual Descriptions | [`[pdf]`](https://arxiv.org/pdf/2103.14675) | [`[o-pytorch]`](https://github.com/anindita127/Complextext2animation) |
5. <span id = "1005">**[TEMOS]**</span> | **ECCV'22** | TEMOS: Generating diverse human motions from textual descriptions | [`[pdf]`](https://arxiv.org/pdf/2204.14109) | [`[o-pytorch]`](https://github.com/Mathux/TEMOS) |
6. <span id = "1006">**[TM2T]**</span> | **ECCV'22** | TM2T: Stochastic and Tokenized Modeling for the Reciprocal Generation of 3D Human Motions and Texts | [`[pdf]`](https://arxiv.org/pdf/2207.01696) | [`[o-pytorch]`](https://github.com/EricGuo5513/TM2T) |
7. <span id = "1007">**[T2T]**</span> | **CVPR'22** | Generating Diverse and Natural 3D Human Motions from Text | [`[pdf]`](https://openaccess.thecvf.com/content/CVPR2022/papers/Guo_Generating_Diverse_and_Natural_3D_Human_Motions_From_Text_CVPR_2022_paper.pdf) | [`[o-pytorch]`](https://github.com/EricGuo5513/text-to-motion) |
8. <span id = "1008">**[MDM]**</span> | **ICLR'23** | MDM: Human Motion Diffusion Model | [`[pdf]`](https://arxiv.org/pdf/2209.14916) | [`[o-pytorch]`](https://github.com/GuyTevet/motion-diffusion-model) |
9. <span id = "1009">**[MotionDiffuse]**</span> | **Arxiv'22 (TPAMI'24)** | MDM: Human Motion Diffusion Model | [`[pdf]`](https://arxiv.org/pdf/2208.15001) | [`[o-pytorch]`](https://github.com/mingyuan-zhang/MotionDiffuse) |
10. <span id = "1010">**[MLD]**</span> | **CVPR'23** | Executing your Commands via Motion Diffusion in Latent Space | [`[pdf]`](https://arxiv.org/pdf/2212.04048) | [`[o-pytorch]`](https://github.com/chenfengye/motion-latent-diffusion) |
11. <span id = "1011">**[T2m-GPT]**</span> | **CVPR'23** | T2M-GPT: Generating Human Motion from Textual Descriptions with Discrete Representations | [`[pdf]`](https://arxiv.org/pdf/2301.06052) | [`[o-pytorch]`](https://github.com/Mael-zys/T2M-GPT) |
12. <span id = "1012">**[Fg-T2M]**</span> | **ICCV'23** | Fg-T2M: Fine-Grained Text-Driven Human Motion Generation via Diffusion Model | [`[pdf]`](https://arxiv.org/pdf/2309.06284) | - |
13. <span id = "1013">**[M2DM]**</span> | **ICCV'23** | Priority-Centric Human Motion Generation in Discrete Latent Space | [`[pdf]`](https://arxiv.org/pdf/2308.14480) | - |
14. <span id = "1014">**[AttT2M]**</span> | **ICCV'23** | AttT2M: Text-Driven Human Motion Generation with Multi-Perspective Attention Mechanism | [`[pdf]`](https://arxiv.org/pdf/2309.00796) | [`[o-pytorch]`](https://github.com/ZcyMonkey/AttT2M) |
15. <span id = "1015">**[MotionGPT]**</span> | **NeurIPS'23** | MotionGPT: Human Motion as a Foreign Language | [`[pdf]`](https://arxiv.org/pdf/2306.14795) | [`[o-pytorch]`](https://github.com/OpenMotionLab/MotionGPT) |
16. <span id = "1016">**[ReMoDiffuse &dagger;]**</span> | **NeurIPS'23** | ReMoDiffuse: Retrieval-Augmented Motion Diffusion Model | [`[pdf]`](https://arxiv.org/pdf/2304.01116) | [`[o-pytorch]`](https://github.com/mingyuan-zhang/ReMoDiffuse) |
17. <span id = "1017">**[MMM]**</span> | **CVPR'24** | MMM: Generative Masked Motion Model | [`[pdf]`](https://arxiv.org/pdf/2312.03596) | [`[o-pytorch]`](https://github.com/exitudio/MMM/) |
18. <span id = "1018">**[MoMask]**</span> | **CVPR'24** | MoMask: Generative Masked Modeling of 3D Human Motions | [`[pdf]`](https://arxiv.org/pdf/2312.00063) | [`[o-pytorch]`](https://github.com/EricGuo5513/momask-codes) |
19. <span id = "1019">**[MotionLCM]**</span> | **ECCV'24** | MotionLCM: Real-time Controllable Motion Generation via Latent Consistency Model | [`[pdf]`](https://arxiv.org/pdf/2404.19759) | [`[o-pytorch]`](https://github.com/Dai-Wenxun/MotionLCM) |
20. <span id = "1020">**[Motion Mamba]**</span> | **ECCV'24** | Motion Mamba: Efficient and Long Sequence Motion Generation with Hierarchical and Bidirectional Selective SSM | [`[pdf]`](https://arxiv.org/pdf/2403.07487) | [`[o-pytorch]`](https://github.com/steve-zeyu-zhang/MotionMamba/) |

### Spatial Contraints
1. <span id = "2001">**[GMD]**</span> | **ICCV'23** | Guided motion diffusion for controllable human motion synthesis | [`[pdf]`](https://arxiv.org/pdf/2305.12577) | [`[o-pytorch]`](https://github.com/korrawe/guided-motion-diffusion) |
2. <span id = "2002">**[PhysDiff]**</span> | **ICCV'23** | PhysDiff: Physics-Guided Human Motion Diffusion Model | [`[pdf]`](https://arxiv.org/pdf/2212.02500) | - |
3. <span id = "2003">**[PriorMDM]**</span> | **ICLR'24** | Human Motion Diffusion as a Generative Prior | [`[pdf]`](https://arxiv.org/pdf/2303.01418) | [`[o-pytorch]`](https://github.com/priorMDM/priorMDM) |
4. <span id = "2004">**[OmniControl]**</span> | **ICLR'24** | Omnicontrol: Control any joint at any time for human motion generation | [`[pdf]`](https://arxiv.org/pdf/2310.08580) | [`[o-pytorch]`](https://github.com/neu-vi/omnicontrol) |


## Feedback

If you have any suggestions or find missing papers, please feel free to contact me.

- [e-mail](mailto:run542968@gmail.com)
- [pull request](https://github.com/Run542968/Awesome-3D-Human-Motion-Generation/pulls)

## Thanks
This format of this awesome follows [this project](https://github.com/Pilhyeon/Awesome-Weakly-Supervised-Temporal-Action-Localization), thanks for such a pretty template!