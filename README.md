# Rust Detection with YOLO

This project fine-tunes a YOLO model to detect rust in images using bounding boxes.  
The workflow covers dataset preparation, training, validation, and inference on a small custom dataset.  

---

## 📂 Dataset  
- **Images:** 100 images provided (unlabeled).  
- **Annotation tool:** [CVAT](https://cvat.org/) → exported in **YOLO Ultralytics 1.0 format**.  
- **Class:** `rust` (single-class detection).  
- **Split:** `70/20/10` for train/val/test inside `SAGER-TASK/dataset/`.  

---

## ⚙️ Environment  
- **Platform:** Google Colab (Google Drive integration).  
- **GPU:** NVIDIA Tesla T4.  
- **Frameworks:**  
  - PyTorch (via Ultralytics YOLO)  
  - OpenCV, PyYAML, Matplotlib  

---

## 🚀 Training  
- **Model tested:** YOLOv8 (n/s/m), YOLO11 (n/s/m) → **YOLO11m chosen**.  
- **Input size:** 832 (to better capture small rust spots).  
- **Epochs:** Up to 150 (early stopping at ~78).  
- **Optimizer:** AdamW (lr=0.001, weight decay=0.0005).  
- **Batch size:** 8.  
- **Augmentations used:**  
  - HSV color jitter (lighting/paint variation).  
  - Small rotations, translations, scaling, shear.  
  - Horizontal flips for viewpoint diversity.  
  - Low mosaic, **no mixup** (to preserve rust texture).  
  - Random erasing (occlusion simulation).  

---

## 📊 Results  
Validation (20 images, 36 instances):  
- **Precision (P):** ~0.52  
- **Recall (R):** ~0.44  
- **mAP@50:** ~0.42  
- **mAP@50-95:** ~0.18  

Inference speed (T4): ~16ms/image.  

---

## ⚠️ Challenges  
- **Small dataset (100 images):** Limited diversity, risk of over/underfitting.  
- **Annotation consistency:** Required multiple passes for clearer definition of rust.  
- **Low-contrast rust:** Harder to detect; mitigated by higher input size & tuned augs but remains a challenge.  

---

## 💡 Possible Improvements  
- Use **segmentation annotation** (better suited for irregular rust patterns).  
- Collect more data under varied conditions.  
- Explore larger YOLO11 variants (e.g., L).  
- Use Test-Time Augmentation (TTA).  

---


yaml
Copy code
