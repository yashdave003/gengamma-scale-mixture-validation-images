# **[Do Generalized-Gamma Scale Mixtures of Normals Fit Large Image Datasets?](https://arxiv.org/abs/2512.17038)**

## Abstract

A scale mixture of normals is a distribution formed by mixing a collection of normal distributions with fixed mean but different variances. A generalized gamma scale mixture draws the variances from a generalized gamma distribution. Generalized gamma scale mixtures of normals have been proposed as an attractive class of parametric priors for Bayesian inference in inverse imaging problems. Generalized gamma scale mixtures have two shape parameters, one that controls the behavior of the distribution about its mode, and the other that controls its tail decay. 
In this paper, we provide the first demonstration that the prior model is realistic for multiple large imaging datasets. We draw data from remote sensing, medical imaging, and image classification applications. We study the realism of the prior when applied to Fourier and wavelet (Haar and Gabor) transformations of the images, as well as to the coefficients produced by convolving the images against the filters used in the first layer of AlexNet, a popular convolutional neural network trained for image classification.  We discuss data augmentation procedures that improve the fit of the model, procedures for identifying approximately exchangeable coefficients, and characterize the parameter regions that best describe the observed datasets. These regions are significantly broader than the region of primary focus in computational work. We show that this prior family provides a substantially better fit to each dataset than any of the standard priors it contains. These include Gaussian, Laplace, $\ell_p$, and Student's $t$ priors. Finally, we identify cases where the prior is unrealistic and highlight characteristic features of images that suggest the model will fit poorly.

## File Structure

```
.
├── dataset-preparation/        # Scripts to preprocess datasets
├── demos/                      # End-to-end demo notebook
├── gabor/                      # Gabor filter preliminary tests
├── learned-filters/            # Learned filter preliminary tests
├── publication/                # Figures and assets used in the paper
├── results/                    # Output reports, CDFs, and case studies
│   ├── CDFs/                   # Empirical CDF plots
│   └── case-studies/           # Per-dataset case study notebooks and outputs. 
│       └── <dataset>/       
│           └── <subset>/
│               └── <transform>/
│                   └── <channel>/
│                       ├── plots/ 
|                       ├── CSVs/
|                       ├── independence_template.ipynb  # generic independence testing pipeline
|                       ├── testing_template.ipynb  # generic testing pipeline
|                       └── <channel>-<subset>-<dataset>-<transform>.ipynb
├── transformed-data/           # Transformed images, download from Box
├── utilities/                  # Shared helper functions
└── requirements.txt            # Python dependencies
```

---

## Setup

To reproduce the findings from the ground up, follow the steps outlined below:

**1. Install uv** (if not already installed):

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

**2. Create a virtual environment and install dependencies:**

```bash
uv venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
uv pip install -r requirements.txt
```

**3. Download transformed data** from this [Box folder](https://berkeley.box.com/s/a0zmzg1aix78psr4xl7z7x46nwh3y28v). 

**(Optional) Download raw data** from the [Box folder](https://berkeley.box.com/s/cfcbjw85az6iicczvenvek8ntsbqrrfa) and place it in `raw-data/` before running experiments. Process the raw data following the instructions in `dataset-preparation/` to obtain the files in `transformed-data/`. Instructions included in `dataset-preparation\README.md` for full reproducibility.

**5. Copy the `testing_template.ipynb`** provided in `results/case-studies/` to the specific subfolder in `results` of interest, load the fields appropriately, run the notebook. Results located in the corresponding subfolders `plots/` and `CSVs`.

**6. Access aggregate results and plotting code** in `publication/paper`.


## Datasets

This repository uses seven image datasets spanning remote sensing, natural imagery, and medical imaging.

### Remote Sensing

| Dataset | # Images | Description |
|---|---|---|
| [agriVision](https://arxiv.org/abs/2001.01306) | 4,500 | Agricultural Vision — central US farmlands (256×256) |
| [pastis](https://doi.org/10.5281/zenodo.5012942) | 1,590 | Panoptic Agricultural Satellite Time Series — farm fields in France (128×128) |
| [spaceNet](https://arxiv.org/abs/2004.06500) | 3,401 | Multi-Sensor All Weather Mapping — centered in Rotterdam (400×400) |

### Natural Images

| Dataset | # Images | Description |
|---|---|---|
| [coco](https://arxiv.org/abs/1405.0312) | 4,050 | MS COCO: Common Objects in Context — split into indoor/outdoor subsets (256×256) |
| [segmentAnything](https://arxiv.org/abs/2304.02643) | 7,072 | Segment Anything dataset — natural images compiled for segmentation model training (512×512) |

### Medical Imaging

| Dataset | # Images | Description |
|---|---|---|
| [syntheticMRI2D](https://arxiv.org/abs/2209.07162) | 15,000 | 2D synthetic MRI brain images — axial (333×234), coronal (244×234), and sagittal (174×234) slices |
| [syntheticMRI3D](https://arxiv.org/abs/2209.07162) | 300 | 3D synthetic MRI brain images (160×224×160) |

![Image Panel](publication\paper\final_plots\data_panel.jpg)

---

## Citation

```bibtex
@misc{marks2025generalized,
  title     = {Do Generalized-Gamma Scale Mixtures of Normals Fit Large Image Datasets?},
  author    = {Brandon Marks and Yash Dave and Zixun Wang and Hannah Chung and Riya Patwa and Simon Cha and Michael Murphy and Alexander Strang},
  year      = {2025},
  eprint    = {2512.17038},
  archivePrefix = {arXiv},
  primaryClass  = {stat.AP},
  doi       = {10.48550/arXiv.2512.17038}
}
```
