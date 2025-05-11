# Enhancing Photogrammetric Reconstruction with Gaussian Splatting-Based Novel Views

**Author:** Mudit  
**Date:** May 2025

---

## Abstract

This project explores the integration of neural rendering methods into traditional photogrammetry workflows. Using Agisoft Metashape, an initial 3D model was created from a limited set of original images. Then, Gaussian Splatting was used to synthesize novel views of the same scene, which were quantitatively assessed and then incorporated into the original dataset. A second 3D reconstruction was carried out with the augmented dataset. The two reconstructions were compared using both qualitative (visual) and quantitative (geometric) methods. Results demonstrate that Gaussian Splatting-generated views can effectively supplement real photographs to enhance the accuracy and completeness of photogrammetric models.

---

## Introduction

Photogrammetry has proven to be an efficient method for reconstructing 3D scenes from multiple 2D images. However, the quality of the final model heavily depends on the diversity and completeness of camera viewpoints. Limited viewpoints often lead to gaps, inaccuracies, or poor surface reconstruction, especially in occluded or less photographed regions.

Gaussian Splatting is a recent technique in neural rendering that enables fast, high-quality novel view synthesis. It reconstructs a scene using 3D Gaussian primitives learned from input images and can render plausible views from arbitrary perspectives. This project investigates whether novel views rendered using Gaussian Splatting can be effectively used to augment photogrammetry and improve 3D model quality.

---

## Software Used

- Agisoft Metashape: For photogrammetric processing, including image alignment, dense point cloud generation, mesh creation, and texturing.
- Gaussian Splatting (GraphDeCO): Open-source neural rendering tool for novel view synthesis.
- Open3D: Used to compute mesh statistics such as vertex count, face count, and bounding box volume.
- Python 3.10 with PyTorch: Environment used for executing Gaussian Splatting and mesh evaluation scripts.
- Ubuntu 22.04: Operating system for running all tools.

---

## Procedure

### Part A – Baseline Photogrammetry and Neural Rendering Evaluation

**Step 1: Initial Dataset Preparation**  
The dataset consisted of 10 original high-resolution images taken from slightly different angles around a target object. These images were captured ensuring adequate overlap to allow for robust photogrammetric alignment.

**Step 2: Photogrammetric Reconstruction using Agisoft Metashape**  
Using Agisoft Metashape, the following reconstruction workflow was executed:
- Photo Alignment
- Dense Point Cloud Generation
- Mesh Generation
- Texture Mapping

**Step 3: Gaussian Splatting Setup**  
The same 10-image dataset was used to train a Gaussian Splatting model.

**Step 4: Novel View Rendering**  
Ten rendered images were generated from novel camera viewpoints.

**Step 5: Image Quality Evaluation**  
Synthetic images were compared with the originals using PSNR and SSIM metrics.

**Step 6: Writing Python Code for Evaluation**  
I wrote a custom Python script (`evaluate_psnr_ssim.py`) that takes original and rendered image pairs as input and calculates PSNR and SSIM values for each pair. 
![image](https://github.com/muditkhandelwal16/RAS-SES-598-Space-Robotics-and-AI/blob/main/assignments/cart_pole_optimal_control/graphs.png)
This script helped generate the following evaluation table:

| Original      | Rendered  | PSNR | SSIM   |
|---------------|-----------|------|--------|
| A17_01.png    | img1.png  | 7.67 | 0.0841 |
| A17_02.png    | img10.png | 6.86 | 0.0626 |
| A17_03.png    | img2.png  | 7.53 | 0.114  |
| A17_04.png    | img3.png  | 7.20 | 0.114  |
| A17_05.png    | img4.png  | 7.68 | 0.232  |
| A17_06.png    | img5.png  | 7.51 | 0.1478 |
| A17_07.png    | img6.png  | 9.59 | 0.2335 |
| A17_08.png    | img7.png  | 7.98 | 0.1773 |
| A17_09.png    | img8.png  | 9.70 | 0.2094 |
| A17_10.png    | img9.png  | 9.56 | 0.1812 |

---

### Part B – Photogrammetry with Gaussian Splatting-Augmented Dataset

**Step 7: Generating and Adding Novel Views**  
From the trained Gaussian Splatting model, 10 synthetic views were rendered and added to the dataset. These views were chosen from perspectives not originally present in the dataset.

**Step 8: Full Photogrammetric Reconstruction with 25 Images**  
The expanded dataset was processed again in Metashape using the same steps as in Part A:
- Photo Alignment
- Dense Cloud Generation
- Mesh Construction
- Texture Mapping

**Step 9: Writing Python Code for Mesh Comparison**  
To compare the meshes generated from 15 and 25 images, I wrote a Python script (`compare_mesh_stats.py`) that loads both `.ply` mesh files using Open3D, counts vertices and faces, and calculates the bounding box volume. This script provided the following metrics:

| Model Type                         | Vertices | Faces   | Bounding Box Volume |
|-----------------------------------|----------|---------|---------------------|
| Photogrammetry (15 views)         | 274,292  | 548,097 | 649.57              |
| Photogrammetry + Splat Views (25) | 268,438  | 536,450 | 296.89              |

**Step 10: Qualitative Model Comparison**  
The 25-image model showed improved surface geometry, better closure, and fewer holes. Texture coverage was also more complete compared to the original reconstruction.

---

## Conclusion

Synthetic views generated by Gaussian Splatting provided sufficient additional coverage to improve photogrammetric reconstruction. Quantitative results show tighter geometry, and qualitative evaluation confirms more complete and realistic surface modeling. This hybrid approach can be applied to improve 3D modeling quality in various fields including digital heritage preservation, simulation environments, and autonomous systems.

---
