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

### Humanml3D

| ID  | Year | Venue | Model<br/> (or Authors) | R Precision<br/> Top-1 $\uparrow$ |  R Precision<br/> Top-2 $\uparrow$ | R Preciion<br/> Top-3 $\uparrow$ | FID $\downarrow$ | MM Dist $\downarrow$ | MultiModality $\uparrow$ | Diversity $\rightarrow$ | code | - | 
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 1 | 2024 | CVPR | [MMM](#1001) | 0.504 $^{\pm.003}$ | 0.696 $^{\pm.003}$ | 0.794 $^{\pm.002}$ | 0.080 $^{\pm.003}$ | 2.998 $^{\pm.007}$ | 9.411 $^{\pm.058}$ | 1.164 $^{\pm.041}$ | [[o-pytorch]](https://github.com/exitudio/MMM/) | - |



## Paper List

1. <span id = "1001">**[MMM]**</span> | **CVPR'24** | MMM: Generative Masked Motion Model | [`[pdf]`](https://arxiv.org/pdf/2312.03596) | [`[o-pytorch]`](https://github.com/exitudio/MMM/)


## Feedback

If you have any suggestions or find missing papers, please feel free to contact me.

- [e-mail](mailto:run542968@gmail.com)
- [pull request](https://github.com/Run542968/Awesome-3D-Human-Motion-Generation/pulls)

## Thanks
This format of this awesome follows [this project](https://github.com/Pilhyeon/Awesome-Weakly-Supervised-Temporal-Action-Localization), thanks for such a pretty template!