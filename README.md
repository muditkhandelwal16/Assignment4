# Enhancing Photogrammetric Reconstruction with Gaussian Splatting-Based Novel Views

This project investigates whether novel views generated using **Gaussian Splatting**, a neural rendering technique, can be used to improve traditional **photogrammetric 3D reconstruction**.

We use a two-part approach:

### 📌 Part A: Baseline Model and Splatting Evaluation
- A set of original photographs (10–15 images) was used to generate a 3D mesh using **Agisoft Metashape**.
- **Gaussian Splatting** was applied to the same dataset to synthesize novel views.
- The synthetic images were compared with original images using **PSNR** and **SSIM** metrics to evaluate rendering quality.

### 📌 Part B: Gaussian-Augmented Photogrammetry
- 10 novel images rendered by Gaussian Splatting were added to the original set.
- A fresh photogrammetric model was built using the **25-image dataset**.
- Quantitative comparison (vertices, faces, bounding box volume) and qualitative evaluation showed improvements in the final reconstruction.

---

### 🔧 Tools & Software Used
- [Agisoft Metashape](https://www.agisoft.com/)
- [Gaussian Splatting (GraphDeCO)](https://github.com/graphdeco-inria/gaussian-splatting)
- Python 3.10 + PyTorch
- Open3D for mesh analysis
- Ubuntu 22.04

---

### 📄 Report

A detailed project report documenting all steps, results, tables, and analysis is available here:

📥 [Download Full Report (Word Doc)](./Mudit_Gaussian_Splatting_Report.docx)

---

### 📷 Example Results (Optional Section)
> _You can add visual examples like meshes, comparisons, and synthetic views here if available._

---

### ✅ Conclusion

This project demonstrates that neural rendering outputs like those from **Gaussian Splatting** can meaningfully augment photogrammetric datasets and improve 3D reconstruction quality. This hybrid approach could be useful for applications in digital heritage, robotics, or simulation where complete 3D models are crucial.

---

### 📫 Contact
Created by **Mudit**  
For questions or collaboration, feel free to open an issue or fork the repository.
