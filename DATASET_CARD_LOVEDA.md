---
# For reference on dataset card metadata, see the spec: https://github.com/huggingface/hub-docs/blob/main/datasetcard.md?plain=1
# Doc / guide: https://huggingface.co/docs/hub/datasets-cards
task_categories:
- image-segmentation
task_domain:
- remote-sensing
language:
- en
tags:
- remote-sensing
- land-cover
- semantic-segmentation
- domain-adaptation
- aerial-imagery
size_categories:
- 1K<n<10K
---

# Dataset Card for LoveDA

## Dataset Summary

LoveDA is a remote sensing land-cover dataset for domain adaptive semantic segmentation. It contains 5,987 high-resolution aerial images (1,024 × 1024 pixels) collected from two distinct geographic domains — urban and rural — across three Chinese cities. Unlike previous datasets, LoveDA specifically addresses the challenge of domain shift between urban and rural scenes, making it a benchmark for evaluating transferable learning in land-cover classification.

## Dataset Details

### Dataset Description

- **Curated by:** Nanjing University, Wuhan University, and Chinese Academy of Sciences
- **Shared by:** The LoveDA research team
- **License:** CC BY-SA 4.0

Deep learning approaches have achieved promising results in land-cover mapping using high-spatial-resolution (HSR) imagery. However, urban and rural scenes exhibit vastly different geographic landscapes, and the insufficient generalization of these algorithms hinders city- or country-level mapping. Most existing datasets only promote the research of semantic representation learning, ignoring model transferability. LoveDA was created to advance transferable semantic learning by providing a real (non-simulated) dataset for training and evaluating models that generalize between urban and rural domains.

The dataset deliberately challenges models with: multi-scale objects, complex background samples, and inconsistent class distributions across domains.

### Dataset Sources

- **Repository:** https://github.com/Junjue-Wang/LoveDA
- **Paper:** https://arxiv.org/abs/2109.09417

## Uses

### Direct Use

- Train and benchmark semantic segmentation models for land-cover classification on high-resolution aerial imagery
- Train and benchmark unsupervised domain adaptation (UDA) methods to transfer knowledge from urban to rural scenes (and vice versa) without manual labels
- Evaluate model generalization capabilities across geographically distinct domains

### Out-of-Scope Use

- Real-time or operational large-scale mapping without fine-tuning
- Non-aerial or satellite-only imagery (the dataset is specific to drone/aerial imagery at 0.3m resolution)
- Non land-cover segmentation tasks

## Dataset Structure

The dataset consists of:

| Split | Urban | Rural | Total |
|-------|-------|-------|-------|
| Train | 1,812 | 1,095 | 2,907 |
| Val | 482 | 206 | 688 |
| Test | 1,341 | 1,051 | 2,392 |
| **Total** | **3,635** | **2,352** | **5,987** |

- **Image size:** 1,024 × 1,024 pixels
- **Resolution:** 0.3 m/pixel
- **Number of classes:** 7 land-cover categories (background, building, road, water, barren, forest, agriculture)
- **Format:** RGB images with corresponding label masks (PNG)

## Dataset Creation

### Curation Rationale

LoveDA was created to fill the gap in domain-adaptive remote sensing datasets. Existing datasets treated urban and rural scenes as a single domain, which does not reflect real-world deployment scenarios where models must generalize across fundamentally different landscapes. LoveDA provides a standardized benchmark for evaluating whether segmentation models can transfer knowledge between urban and rural environments.

### Source Data

#### Data Collection and Processing

- **Source:** Aerial/drone imagery acquired over three Chinese cities
- **Resolution:** 0.3 m ground sampling distance
- **Processing:** Images were cropped into 1,024 × 1,024 pixel tiles. Pixel-level annotations were produced for each tile across 7 land-cover categories.
- **Splits:** Separate train/val/test splits were created for urban and rural domains to enable domain adaptation experiments (Urban→Rural and Rural→Urban).

#### Who are the source data producers?

The imagery and annotations were produced by the LoveDA research team from Nanjing University, Wuhan University, and the Chinese Academy of Sciences.

### Annotations

#### Annotation process

Pixel-level semantic annotations were created for all 5,987 images. Each pixel is assigned one of 7 classes. The annotation was performed by trained annotators using aerial imagery interpretation.

#### Who are the annotators?

The annotations were produced by the research team involved in the LoveDA project.

#### Personal and Sensitive Information

The dataset consists of aerial imagery of urban and rural landscapes. No personally identifiable information is included. Buildings and infrastructure are visible but cannot be linked to specific individuals.

## Bias, Risks, and Limitations

- **Geographic bias:** The dataset is limited to three Chinese cities. Models trained on LoveDA may not generalize to other countries or continents with different urban planning patterns or rural landscapes.
- **Domain shift:** The urban-rural domain gap is intentionally large, which may cause models trained on one domain to perform poorly on the other without domain adaptation techniques.
- **Class imbalance:** Some classes (e.g., background, road) dominate the pixel distribution, which can bias models toward majority classes.
- **Resolution specificity:** At 0.3 m resolution, the dataset may not transfer directly to coarser-resolution satellite imagery (e.g., Sentinel-2 at 10m).
- **Temporal limitation:** The imagery represents a single time period; seasonal variations are not captured.

### Recommendations

Users should:
- Report results separately for urban and rural domains
- Use domain adaptation techniques when deploying across domains
- Be cautious when extrapolating results to other geographic regions
- Consider class imbalance mitigation strategies during training

## Citation

**BibTeX:**

```bibtex
@inproceedings{mitchell2019model,
  title={Model Cards for Model Reporting},
  author={Mitchell, Margaret and Wu, Simone and Zaldivar, Andrew and Barnes, Parker and Vasserman, Lucy and Hutchinson, Ben and Spitzer, Elena and Raji, Inioluwa Deborah and Gebru, Timnit},
  booktitle={Proceedings of the Conference on Fairness, Accountability, and Transparency},
  pages={220--229},
  year={2019}
}
```

**APA:**

Mitchell, M., Wu, S., Zaldivar, A., Barnes, P., Vasserman, L., Hutchinson, B., Spitzer, E., Raji, I. D., & Gebru, T. (2019). Model Cards for Model Reporting. In *Proceedings of the Conference on Fairness, Accountability, and Transparency* (pp. 220–229).

## Glossary

- **Domain Adaptation (DA):** A machine learning technique that enables a model trained on one data distribution (source domain) to perform well on a different but related distribution (target domain).
- **Unsupervised Domain Adaptation (UDA):** Domain adaptation where the target domain has no labeled data.
- **Semantic Segmentation:** The task of assigning a class label to every pixel in an image.
- **HSR (High Spatial Resolution):** Imagery with pixel size typically ≤ 1 meter.
- **Domain Shift:** The difference in data distribution between training (source) and deployment (target) environments.

## More Information

For more details about the dataset, please visit:
- Official repository: https://github.com/Junjue-Wang/LoveDA
- Paper: https://arxiv.org/abs/2109.09417

## Dataset Card Authors

Julian Andrés Quintero Rincón

## Dataset Card Contact

- **Nombre:** Julian Andrés Quintero Rincón
- **Correo electrónico:** juaquinteror@udistrital.edu.co
- **Código:** 20211025017
- **Asignatura:** Inteligencia Artificial aplicada al Territorio
- **Docente:** Paulo Cesar Coronado Sánchez
