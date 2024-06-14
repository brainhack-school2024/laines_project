
![GMseg](https://github.com/brainhack-school2024/laines_project/assets/77469192/c5196472-1e44-4d3c-93e1-f84255b66516)

# Spinal cord gray matter contrast-region-agnostic segmentation


# Aboud me!
<a href="https://github.com/Nilser3">
   <img src="https://avatars.githubusercontent.com/u/77469192?v=4?s=100" width="100px;" alt=""/>
   <br /><sub><b>Nilser Laines Medina</b></sub>
</a>

Hi! I'm a PhD student at Aix Marseille Université and Polytechnique de Montréal. 
My background is in Biomedical Signal and Image Processing and Neurosciences. 
For the brainhack school, I would work on automatic segmentation of the spinal sord Gray Matter (GM) across multiple MRI contrasts and regions (cervical, thoracic and lumbar) on open GM data invivo and exvivo.

# Introduction
Analyzing gray matter (GM) in the spinal cord is of significant interest to better understand various diseases such as multiple sclerosis (MS), amyotrophic lateral sclerosis (ALS), spinal cord injuries (SCI), spinal cord tumors, and other pathologies involving the spinal cord through the measurement of the cross-sectional area (CSA) (Papinutto and Henry 2019; Prados et al. 2017). The segmentation of GM will be crucial for measure the cross-sectional area (CSA). 

## Research problem: 
<br /><img src="https://github.com/brainhack-school2024/laines_project/assets/77469192/c9bed3dc-0ad8-47a1-9933-5fcd36f3e41e" width="700px;" alt=""/>


# Main Objectives
- Organize GM Open datasets on BIDS 
- Provide a preprocessing pipeline for training/testing nnU-net models
- Train a contrast-region-agnostic model for segment the spinal cord Gray Matter 
- Make the model available to everyone!

# Data

| Data  | Source  | Sequence  | In-plane resolution (mm2)  | Category/N  | N of 2D slices  | Region |
|-|-|-|-|-|-|-|
| gmseg-challenge  | [challenge](http://niftyweb.cs.ucl.ac.uk/program.php?p=CHALLENGE) | 3T T2s | 0.28x0.28  | HC/80 | ~2000  | cervical  |
| marseille-3T-t2s  | [OSF](https://osf.io/ymrgk/)   | 3T T2s  | 0.47x0.47  | HC/25  | ~500  | cervical, thoracic, lumbar  |
| exvivo 1  |  [Link 1](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5988447)  | 9.4T T2w|  50x50x200 µ  | HC/1  | ~3500 | cervical, thoracic, lumbar  |
| exvivo 2  | [Link 2](https://erda.ku.dk/public/archives/492d3cc45b7c910829a64d1c196b33e7/published-archive.html#)   | 7T DTI FA | 100 µ  isotropic | HC/1  | ~3500 | cervical, thoracic, lumbar  |

# Tools & Methods
- Pre processing: [Spinal Cord Toolbox](https://spinalcordtoolbox.com/), [ivadomed](https://ivadomed.org/)
- Deep Learning: 2D [nnUNetV2 framework](https://github.com/MIC-DKFZ/nnUNet)
- Data analyse: Matplotlib, seaborn
- Computational resources: [Compute Canada](https://ccdb.alliancecan.ca/security/login)

# Experiments
## 1. Data organization: Exvivo data 3D sliptting 

<br /><img src="https://github.com/brainhack-school2024/laines_project/assets/77469192/8513dac2-c0a1-44e6-ac4f-7c6b82845faf" width="500px;" alt=""/>

## 2. Curves of training (Best fold)

<br /><img src="https://github.com/brainhack-school2024/laines_project/assets/77469192/5d76bf1f-7af3-4344-8dfb-949615b25890" width="500px;" alt=""/>

This model will be named `Butterfly_seg`

# Results
### 1. Dice Score Coeficient on test split 
![image](https://github.com/brainhack-school2024/laines_project/assets/77469192/f3966ba9-d312-4b82-93cf-930382309489)

### 2. Some visalization of automatic segmentations
<br /><img src="https://github.com/brainhack-school2024/laines_project/assets/77469192/cf0a185d-5c56-4913-86b3-aceafd57446f" width="700px;" alt=""/>



# Implementation on nnUNet
With [SlicerNNUnet](https://github.com/KitwareMedical/SlicerNNUnet) module is possible to implement [nnUNetV2](https://github.com/MIC-DKFZ/nnUNet) pre-trained models on [Slicer (v5.7.0)](https://download.slicer.org/). 
We could implement `Butterfly_seg` in Slicer by following these steps:

I. Install [3D Slicer version 5.7.0](https://download.slicer.org/), then install the module[SlicerNNUnet](https://github.com/KitwareMedical/SlicerNNUnet) from the extensions explorer (see Fig.01).

**Fig.01**

<img src="https://github.com/spinalcordtoolbox/spinalcordtoolbox/assets/77469192/9d7964d2-66e3-464d-ac1a-04caaaced63b" width="200px;" alt=""/>

II. Download and unzip the `Butterfly_seg` from [here](https://amubox.univ-amu.fr/s/79y3WtYqGF9Ga8x)

III. nnUNet Install: Follow the instructions on first row of Fig. 02

**Fig.02**

<img src="https://github.com/brainhack-school2024/laines_project/assets/77469192/732e01cb-70e4-4e87-aab4-2e3b889ee0e2" width="500px;" alt=""/>


IV. Implementation
- Navigate and select the `Butterfly_seg` folder (See Fig.02) on `Model path`
- Folds: Choose the fold that is currently implemented (4 for us), however we could also implement the 5 trained folds.
- Apply !! 🚀🚀🚀🚀


# Deliverables
1. Data management pipeline: Dicom to nifti to BIDS 
2. Preprocessing pipeline for training/testing for GM contrast-agnostic segmentation Using nnUnet
3. Model Open source available for nnUNet implementation
4. Jupyter notebook for data analysis

# Conclusion
1. `Butterfly_seg` performs well with in-vivo and ex-vivo MRI images
- Bias: Only 2 ex-vivo specimens 
2. `Butterfly_seg` performs well at cervical, thoracic and lumbar levels.
- Imbalance class cervical / thoracic / lumbar images.
3. Does not yet generalize to other contrasts (7T T1maps, 7T UNIT1).
- Other contrasts should be included in training
4. `Butterfly_seg` has been implemented in Slicer 

# Perspectives
- Request data containing new contrasts (AMIRA, 7T T1 maps, 7T DWI, PSIR, MTR, T1w, exvivo-data)
- Try other deep learning approaches

# Acknowledgements
Thank the organizers of the Brainhack School 2024 where I formalized a lot of knowledge that will be useful for my doctoral project.


# References

1. B. De Leener et al., ‘SCT: Spinal Cord Toolbox, an open-source software for processing spinal cord MRI data’, NeuroImage, vol. 145, pp. 24–43, Jan. 2017, doi: 10.1016/j.neuroimage.2016.10.009.
2. Calabrese, Evan, Syed M. Adil, Gary Cofer, Christian S. Perone, Julien Cohen-Adad, Shivanand P. Lad, and G. Allan Johnson. 2018. “Postmortem Diffusion MRI of the Entire Human Spinal Cord at Microscopic Resolution.” NeuroImage. Clinical 18 (March): 963–71.
3. Gros, Charley, Andreanne Lemay, Olivier Vincent, Lucas Rouhier, Anthime Bucquet, Joseph Paul Cohen, and Julien Cohen-Adad. 2020. “Ivadomed: A Medical Imaging Deep Learning Toolbox.” arXiv [eess.IV]. arXiv. http://arxiv.org/abs/2010.09984.
4. Henmar, Simon, Erik B. Simonsen, and Rune W. Berg. 2020. “What Are the Gray and White Matter Volumes of the Human Spinal Cord?” Journal of Neurophysiology 124 (6): 1792–97.
5. Isensee, F., Jaeger, P. F., Kohl, S. A. A., Petersen, J., & Maier-Hein, K. H. (2021). nnU-Net: A self-configuring method for deep learning-based biomedical image segmentation. Nature Methods, 18(2), https://doi.org/10.1038/s41592-020-01008-z
6. Massire, Aurélien, Henitsoa Rasoanandrianina, Maxime Guye, and Virginie Callot. 2020. “Anterior Fissure, Central Canal, Posterior Septum and More: New Insights into the Cervical Spinal Cord Gray and White Matter Regional Organization Using T1 Mapping at 7T.” NeuroImage 205 (January): 116275.
7. Papinutto, Nico, and Roland G. Henry. 2019. “Evaluation of Intra-and Interscanner Reliability of MRI Protocols for Spinal Cord Gray Matter and Total Cross-Sectional Area Measurements.” Journal of Magnetic Resonance Imaging: JMRI 49 (4): 1078–90.
8. Paquin, M-Ê, M. M. El Mendili, C. Gros, S. M. Dupont, J. Cohen-Adad, and P-F Pradat. 2018. “Spinal Cord Gray Matter Atrophy in Amyotrophic Lateral Sclerosis.” AJNR. American Journal of Neuroradiology 39 (1): 184–92.
9. Perone, C.S., Calabrese, E. & Cohen-Adad, J. Spinal cord gray matter segmentation using deep dilated convolutions. Sci Rep 8, 5966 (2018). https://doi-org.lama.univ-amu.fr/10.1038/s41598-018-24304-3
10. Prados, Ferran, John Ashburner, Claudia Blaiotta, Tom Brosch, Julio Carballido-Gamio, Manuel Jorge Cardoso, Benjamin N. Conrad, et al. 2017. “Spinal Cord Grey Matter Segmentation Challenge.” NeuroImage 152 (May): 312–29.
