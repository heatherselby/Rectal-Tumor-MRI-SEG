# Rectal Tumor MRI Segmentation

Deep learning models for automated rectal tumor segmentation on pre- and post-treatment MRI in locally advanced rectal cancer (LARC).

## Introduction

Traditional neoadjuvant therapy for locally advanced rectal cancer (LARC) results in pathologic complete response (pCR) in approximately 15% of patients, supporting non-operative strategies for those with clinical complete response (cCR). The subjectivity and variability in MRI-based cCR assessments highlight the need for objective, quantitative tools.

## Objective

To develop deep learning models for automated rectal tumor segmentation on pre- and post-treatment MRIs, and to identify radiomic features differentiating cCR from non-cCR patients.

## Models

| Model | Description | Training Data | Download |
|-------|-------------|---------------|----------|
| **Model 1** | Pre-treatment baseline | n = 37 reference cases | [Hugging Face](https://huggingface.co/heatherselby/RC-Model1) |
| **Model 2** | Pre-treatment semi-supervised | n = 118 (reference + pseudo-labels) | [Hugging Face](https://huggingface.co/heatherselby/RC-Model2) |
| **Model 3** | Post-treatment baseline | n = 37 post-treatment cases | [Hugging Face](https://huggingface.co/heatherselby/RC-Model3) |

## Results

### Pre-treatment Segmentation
- Radiologist-fellow inter-rater agreement: DSC = 0.748 ± 0.092
- **Model 1**: DSC = 0.682 ± 0.254
- **Model 2**: DSC = 0.769 ± 0.214 (12.8% improvement over Model 1, p < 0.001)

### Post-treatment Segmentation
- Inter-rater agreement: DSC = 0.362 ± 0.256
- **Model 3**: DSC = 0.175 ± 0.231

Post-treatment segmentation remains challenging due to treatment-induced tissue changes affecting both automated models and human raters.

## Installation & Usage

These models were trained using [nnU-Net v2](https://github.com/MIC-DKFZ/nnUNet).

### Install nnU-Net
```bash
pip install nnunetv2
```

### Download and Install Model
```bash
# Download the model zip from Hugging Face, then:
nnUNetv2_install_pretrained_model_from_zip /path/to/model.zip
```

### Run Inference
```bash
nnUNetv2_predict -i INPUT_FOLDER -o OUTPUT_FOLDER -d DATASET_ID -c 3d_fullres -tr nnUNetTrainer -p nnUNetResEncUNetMPlans
```

## Materials and Methods

We retrospectively analyzed pre- and post-treatment MRIs from 37 LARC patients enrolled in a Phase 2 TNT trial (NCT04380337). Rectal tumors were segmented on T2-weighted images by two data scientists, refined by a radiologist (reference standard), and independently segmented by a fellow.

Radiomic features were extracted from post-treatment ADC maps, filtered by reproducibility (ICC ≥ 0.8) and redundancy (Spearman r ≤ 0.95), then analyzed using unsupervised hierarchical clustering. Radiomic clustering revealed two distinct patient groups aligned with cCR and non-cCR status.

## Citation

If you use these models in your research, please cite:

```bibtex
@article{selby2026deeplearning,
  title={Deep learning analysis of MRI to assess rectal cancer treatment},
  author={Selby, Heather M. and Son, Ashley Y. and Sheth, Vipul R. and Wagner, Todd H. and Pollom, Erqi L. and Morris, Arden M.},
  journal={Frontiers in Oncology},
  volume={15},
  pages={1643852},
  year={2026},
  doi={10.3389/fonc.2025.1643852}
}
```
## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contact

[Your contact information]
