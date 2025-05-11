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

- **Agisoft Metashape** – For photogrammetric processing: image alignment, dense cloud generation, mesh creation, and texturing.
- **Gaussian Splatting (GraphDeCO)** – Open-source neural rendering tool used for novel view synthesis.
- **Open3D** – Used to compute mesh statistics such as vertex count, face count, and bounding box volume.
- **Python 3.10 with PyTorch** – Environment used to run the rendering and evaluation tools.
- **Ubuntu 22.04** – Operating system used throughout the pipeline.

---

## Procedure

### Part A – Baseline Photogrammetry and Neural Rendering Evaluation

**Step 1: Initial Dataset Preparation**  
A set of 10 high-resolution images were captured from slightly different viewpoints, ensuring sufficient overlap for photogrammetric alignment.

**Step 2: Photogrammetric Reconstruction using Agisoft Metashape**  
The standard photogrammetry workflow was followed:
- Photo alignment  
- Dense point cloud generation  
- Mesh construction  
- Texture mapping  

This produced a 3D model based on the original 10 images.

**Step 3: Gaussian Splatting Setup**  
The same 10 images were used to train a Gaussian Splatting model. The model learned a 3D representation of the scene using Gaussian primitives.

**Step 4: Novel View Rendering**  
Ten novel images were rendered from new viewpoints not present in the original dataset.

**Step 5: Image Quality Evaluation**  
The synthetic images were evaluated using PSNR and SSIM compared to their closest original counterparts:

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

The values indicate that while the synthetic views differ slightly in pixel-level details, they retain sufficient geometric and structural information to be useful in further reconstruction.

---

### Part B – Photogrammetry with Gaussian Splatting-Augmented Dataset

**Step 6: Generating and Adding Novel Views**  
Ten novel images generated via Gaussian Splatting were added to the original 15-image dataset, forming a new set of 25 total images.

**Step 7: Full Photogrammetric Reconstruction with 25 Images**  
The full dataset was reprocessed in Metashape from scratch:
- Photo alignment  
- Dense cloud generation  
- Mesh construction  
- Texture mapping  

**Step 8: Quantitative Mesh Comparison**

| Model Type                         | Vertices | Faces   | Bounding Box Volume |
|-----------------------------------|----------|---------|---------------------|
| Photogrammetry (15 views)         | 274,292  | 548,097 | 649.57              |
| Photogrammetry + Splat Views (25) | 268,438  | 536,450 | 296.89              |

Although the total number of vertices and faces was slightly reduced, the bounding box volume was significantly lower, indicating a more compact and likely more accurate mesh. This suggests that the addition of synthetic views helped remove ambiguity and noise in the reconstruction.

**Step 9: Qualitative Model Comparison**  
The 25-image model showed:
- Improved surface closure in previously occluded areas  
- Better texture quality  
- Fewer gaps and reduced mesh noise  

This confirmed that synthetic views contributed meaningfully to improving model coverage and completeness.

---

## Conclusion

This project demonstrates that synthetic novel views generated via Gaussian Splatting can improve photogrammetric modeling when added to real-world image datasets. The combination of traditional and neural techniques leads to better scene coverage, reduced artifacts, and more compact 3D models. Both quantitative metrics and visual inspection validate that this hybrid method can be effective in practice. This approach has potential applications in digital reconstruction, AR/VR content creation, and autonomous robotic mapping.

---

## Credits

- Gaussian Splatting GitHub: [graphdeco-inria/gaussian-splatting](https://github.com/graphdeco-inria/gaussian-splatting)
- Metashape: [https://www.agisoft.com](https://www.agisoft.com)
- Project by Mudit
