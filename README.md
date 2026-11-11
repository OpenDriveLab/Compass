<p align="center">
  <img src="asset/compass_icon.png" alt="Compass 1 Logo" height="100">
</p>

<h1 align="center"><strong>Compass 1: Towards Open-World and Persistent Embodied Navigation from Monocular RGB Videos</strong></h1>

<div id="top" align="center">

<div>
  <a href="https://www.archon.tech/research/compass1"><img src="https://img.shields.io/badge/Project_Page-green" alt="Project Page"></a>
  <a href="https://arxiv.org/abs/2611.12087"><img src="https://img.shields.io/badge/arXiv-2611.12087-b31b1b" alt="arXiv"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-Apache_2.0-blue.svg" alt="Apache-2.0 license"></a>
</div>

</div>

## 📖 Introduction

<p align="center">
  <img src="asset/teaser.png" alt="Compass 1 Open-world and persistent embodied navigation" width="100%">
</p>

We present **Compass 1**, the first embodied navigation foundation model to unify language understanding and video generation while enabling memory backtracking through nearly **two minutes** of visual history. Compass 1 achieves a dominant overall success rate of **79.4%** across open-world evaluations, compared to **17.8%** for the strongest baseline.

**Developers**: [Hai Zhang](https://betray12138.github.io/resume/) and [Siqi Liang](https://github.com/stdcat)

## 📢 News

- 🎉 **2026-11-10**: The [project page](https://www.archon.tech/research/compass1) is now available!
- 🎉 **2026-11-10**: The [arXiv preprint](https://arxiv.org/abs/2611.12087) is now available!
- 🚀 **2026-12 (Expected)**: Compass 1 dataset release.
- 🚀 **2026-12 (Expected)**: Compass 1 deployment code & real-world model checkpoint release.

## 📌 Table of Contents

- 📖 [Introduction](#-introduction)
- 📢 [News](#-news)
- 🔥 [Highlights](#-highlights)
- 📊 [Results](#-results)
- 📝 [TODO List](#-todo-list)
- 📬 [Contact](#-contact)
- 📄 [License and Citation](#-license-and-citation)

## 🔥 Highlights

- **Keyframe-Level Unified Backbone & History Representation Map:** To our knowledge, we present the first keyframe-level foundation model built on a unified backbone for embodied navigation. By condensing keyframes and actions into a compact HRM, our method grants the agent persistent spatiotemporal reasoning and nearly two-minute memory backtracking capabilities with zero architectural modification.
- **Structured VQA Supervision Protocol:** We design three structured VQA categories to fully utilize the history reasoning capability and effectively resolve physical execution failure modes including premature stopping, reversed turning, direction drifting, left-right turning deadlocks, and spurious history utilization.
- **Cost-Effective Data Annotation Pipeline:** We establish a semi-automated annotation pipeline requiring human oversight solely at stage boundaries and trajectory noise filtering, enabling the release of a massive navigation corpus featuring over 500 hours of real-world interactions and over 2,000 hours of annotated web videos.
- **Thorough Physical Evaluation & Zero-Shot Cross-Embodiment Generalization:** Extensive real-world experiments demonstrate that Compass 1 drastically outperforms strong baselines across all physical navigation tasks. Remarkably, despite being trained mainly on a fixed camera height distribution, it generalizes zero-shot across diverse embodiments, and substantial camera height variations.

<p align="center">
  <img src="asset/architecture.png" alt="Overview of the history representation map and the architecture of Compass 1" width="100%">
</p>

## 📊 Results

### Overall Success Rate

To guarantee statistical rigor, each method undergoes 10 independent trials for every task across all four scenarios, accumulating **320 total evaluations per approach**.

| Method | Overall Success Rate |
|:-------|:--------------------:|
| **Compass&nbsp;1** | **79.4%** |
| AwareVLN | 17.8% |
| LightNav-0 | 11.6% |
| WNM-3D | 6.3% |
| NaVIDA | 0.3% |

### Success Rate Across All Tasks and Baselines

Success Rate (SR) · 10 trials per task in each scenario · 320 evaluations per approach.

| Task | Compass&nbsp;1 | AwareVLN | LightNav-0 | WNM-3D | NaVIDA |
| --- | --- | --- | --- | --- | --- |
| Initial-Sight Target Navigation | **98%** | 33% | 48% | 30% | 3% |
| Basic Two-Stage Navigation | **93%** | 43% | 10% | 10% | 0% |
| Long Straight-Line Navigation | **73%** | 15% | 0% | 0% | 0% |
| Multi-Stage Navigation | **50%** | 0% | 0% | 0% | 0% |
| Target-Driven Navigation | **85%** | 15% | 18% | 5% | 0% |
| Demand-Driven Navigation | **83%** | 30% | 18% | 5% | 0% |
| Basic History Backtracking | **98%** | 8% | 0% | 0% | 0% |
| Persistent History Backtracking | **58%** | 0% | 0% | 0% | 0% |

### Simulation Evaluation Results

NE: navigation error; OS: oracle success rate; SR: success rate; SPL: success weighted by path length; nDTW: normalized dynamic time warping. ↓ Lower is better; ↑ higher is better. — Not reported.

S.RGB: single-view RGB; Pano.: panoramic or multi-camera RGB; Depth: depth; Odom.: odometry.

#### R2R-CE

R2R Val-Unseen split in continuous environments.

| Method | Method Type | Observation | NE ↓ | OS ↑ | SR ↑ | SPL ↑ |
| --- | --- | --- | --- | --- | --- | --- |
| CMA\* | Multi-view | Pano. · Depth · Odom. | 6.2 | 52 | 41 | 36 |
| HPN+DN\* | Multi-view | Pano. · Depth · Odom. | 6.31 | 40 | 36 | 34 |
| Sim2Sim\* | Multi-view | Pano. · Depth · Odom. | 6.07 | 52 | 43 | 36 |
| DreamWalker\* | Multi-view | Pano. · Depth · Odom. | 5.53 | 59 | 49 | 44 |
| HNR\* | Multi-view | Pano. · Depth · Odom. | 4.42 | 67 | 61 | 51 |
| InstructNav | Multi-view | Pano. · Depth | 6.89 | — | 31 | 24 |
| ABot-N0 | Multi-view | Pano. | 3.8 | 70.8 | 66.4 | 63.9 |
| Qwen-RobotNav-4B | Multi-view | Pano. | 3.8 | 77.2 | 69.5 | 63.6 |
| Qwen-RobotNav-8B | Multi-view | Pano. | 3.53 | 78.5 | 72.1 | 66.6 |
| ABot-N1 | Multi-view | Pano. | 3.91 | 71.7 | 68.3 | 66.6 |
| NaVid | Monocular | S.RGB | 5.47 | 49 | 37 | 35 |
| Uni-NaVid | Monocular | S.RGB | 5.58 | 53.5 | 47 | 42.7 |
| NaVILA | Monocular | S.RGB | 5.22 | 62.5 | 54 | 49 |
| SparseVideoNav | Monocular | S.RGB | 4.17 | 56.1 | 48.6 | 47.4 |
| NaVIDA | Monocular | S.RGB | 4.32 | 69.5 | 61.4 | 54.7 |
| AwareVLN | Monocular | S.RGB | 4.02 | 73.5 | 65.4 | 55.1 |
| WNM-3D | Monocular | S.RGB | 4.35 | 66.7 | 63.1 | 57.9 |
| LightNav-0 | Monocular | S.RGB | 3.91 | 73.7 | 68.5 | 62.8 |
| **Compass&nbsp;1** | Monocular | S.RGB | **3.88** | **74.9** | **70.1** | **63.2** |

\* Methods using a waypoint predictor. Multi-view methods and monocular methods use different observations.

#### HM3D-OVON

Seen-category, synonyms, and unseen-category settings.

| Method | Method Type | Observation | Seen SR ↑ | Seen SPL ↑ | Synonyms SR ↑ | Synonyms SPL ↑ | Unseen SR ↑ | Unseen SPL ↑ |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Qwen-RobotNav-4B | Multi-view | Pano. | 57.7 | 24.4 | 60.1 | 25.1 | 53.1 | 20.9 |
| Qwen-RobotNav-8B | Multi-view | Pano. | 56.1 | 28.5 | 57.8 | 28.8 | 51.2 | 24 |
| ABot-N0 | Multi-view | Pano. | 55.3 | 32.1 | 55.4 | 33.2 | 54 | 30.5 |
| VLFM | Monocular | S.RGB · Depth · Odom. | 35.2 | 18.6 | 32.4 | 17.3 | 35.2 | 19.6 |
| DAgRL+OD | Monocular | S.RGB · Depth · Odom. | 38.5 | 21.1 | 39 | 21.4 | 37.1 | 19.8 |
| MTU3D | Monocular | S.RGB · Depth · Odom. | 55 | 23.6 | 45 | 14.7 | 40.8 | 12.1 |
| Uni-NaVid | Monocular | S.RGB | 41.3 | 21.1 | 43.9 | 21.8 | 39.5 | 19.8 |
| LightNav-0 | Monocular | S.RGB | 55.3 | 31.2 | 54.6 | 29.6 | 47 | 24.2 |
| **Compass&nbsp;1** | Monocular | S.RGB | **57.4** | **31.3** | **59.7** | **31.5** | **52.2** | **26.9** |

#### IntentionNav

Comparison results on demand-driven navigation tasks.

| Method | NE ↓ | OS ↑ | SR ↑ | SPL ↑ |
| --- | --- | --- | --- | --- |
| NaVIDA | 2.53 | 42.5 | 33.5 | 33.3 |
| WNM-3D | 2.99 | 43 | 30 | 29.9 |
| AwareVLN | 3.15 | 60 | 33.5 | 29.8 |
| LightNav-0 | 2.28 | 38.5 | 35.5 | 35.1 |
| **Compass&nbsp;1** | **2.35** | **50.5** | **42.5** | **42.1** |

#### IndoorUAV-VLN

Test Unseen split · All methods are fine-tuned on the dataset.

| Method | NE ↓ | OS ↑ | SR ↑ | nDTW ↑ |
| --- | --- | --- | --- | --- |
| LLaMA-UAV | 8.49 | 4.26 | 3.19 | 4.7 |
| OpenFly | 7.06 | 10.64 | 4.26 | 11.88 |
| π₀\* | 10.53 | 43.62 | 9.57 | 5.85 |
| **Compass&nbsp;1** | **5.94** | **37.23** | **18.09** | **12.14** |

\* Checkpoint open-sourced by IndoorUAV. Trajectories with up and down actions are excluded.

[Paper](https://arxiv.org/abs/2611.12087) · [Evaluation](https://www.archon.tech/research/compass1#results) · [Demo](https://www.archon.tech/research/compass1#demo)

## 📝 TODO List

- [x] Compass 1 Paper Release.
  - [x] arXiv preprint is now available!
  - [x] Project page and navigation demos are now available!
- [ ] Compass 1 Dataset Release (Expected December 2026).
  - [ ] Release the dataset with download instructions.
- [ ] Compass 1 Deployment Code & Real-World Model Checkpoint Release (Expected December 2026).
  - [ ] Release deployment code with installation instructions and usage examples.
  - [ ] Publish real-world model checkpoints and download instructions.

## 📬 Contact

For further inquiries or assistance, please contact [zhanghenryhai12138@gmail.com](mailto:zhanghenryhai12138@gmail.com) or [liangsiqi@connect.hku.hk](mailto:liangsiqi@connect.hku.hk).

## 📄 License and Citation

This repository is licensed under the [Apache-2.0 license](LICENSE).

- Please consider citing our work if it helps your research.

```bibtex
@article{archon2026compass1,
  title={Compass 1: Towards Open-World and Persistent Embodied Navigation from Monocular RGB Videos},
  author={Zhang, Hai and Liang, Siqi and Guo, Yanjun and Zhang, Shoufeng and Wang, Yunhao and Du, Hangyu and Mai, Haoguang and Li, Hongchen and Yang, Jiazhi and Zeng, Jialong and Hu, Yu and Chen, Chen and Jiang, Gangcheng and Zhuo, Zishun and Zhao, Lirui and Li, Zhigang and Qiao, Yu and Yang, Zhenjie and Zhang, Fu and Li, Hongyang},
  journal={arXiv preprint arXiv:2611.12087},
  year={2026},
  eprint={2611.12087},
  archivePrefix={arXiv},
  primaryClass={cs.CV},
  url={https://arxiv.org/abs/2611.12087}
}

@inproceedings{zhang2026sparse,
  title={Sparse Video Generation Propels Real-World Beyond-the-View Vision-Language Navigation},
  author={Zhang, Hai and Liang, Siqi and Chen, Li and Li, Yuxian and Xu, Yukuan and Zhong, Yichao and Zhang, Fu and Li, Hongyang},
  booktitle={NeurIPS},
  year={2026},
}
```
