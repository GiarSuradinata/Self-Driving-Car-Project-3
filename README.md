# Self-Driving-Car-Project-3
Bertujuan untuk pembelajaran segmentasi menggunakan Resnet50

inal Project – Computer Vision  
Topik: **Semantic Segmentation menggunakan Deep Learning**

---

## 📌 Latar Belakang

Self Driving Car (mobil otonom) membutuhkan pemahaman lingkungan yang akurat untuk meningkatkan keselamatan berkendara.  
Salah satu komponen penting adalah **semantic segmentation**, yaitu proses mengklasifikasikan setiap pixel pada gambar ke dalam kelas tertentu (misalnya: jalan, kendaraan, pejalan kaki, bangunan, dll).

Dengan semantic segmentation, sistem dapat:
- Mengurangi human error
- Memberikan pemahaman lingkungan secara menyeluruh
- Mendukung sistem persepsi kendaraan otonom

---

## 🎯 Tujuan Project

Tujuan dari project ini adalah:
1. Melakukan **segmentasi objek** pada citra jalanan
2. Mengevaluasi performa beberapa model deep learning:
   - UNet (from scratch)
   - UNet dengan backbone ResNet-34
   - UNet dengan backbone ResNet-50
3. Membandingkan hasil model berdasarkan metrik evaluasi segmentation

---

## 🗂 Dataset

- **Sumber dataset**: Roboflow (People & Street Scene Segmentation)
- **Jumlah data**:
  - Train: 367 images
  - Validation: 101 images
- **Jenis label**: Mask segmentation (pixel-level)

### Augmentasi Data
Untuk meningkatkan generalisasi model, dilakukan augmentasi:
- Horizontal flip
- Random brightness
- Rotation

---

## 🔧 Data Preprocessing

Tahapan preprocessing meliputi:
1. Verifikasi mask:
   - Menghapus mask duplikat
   - Menghapus mask tanpa pasangan image
2. Validasi kelas:
   - Memastikan jumlah dan ID kelas konsisten
3. Konversi mask:
   - Single-channel mask dengan class ID per pixel

---

## 🧠 Model dan Konfigurasi Training

### Model yang Digunakan
- UNet (tanpa pretrained)
- UNet + ResNet-34 (pretrained)
- UNet + ResNet-50 (pretrained)

### Konfigurasi Training
| Parameter | Nilai |
|---------|------|
| Epoch | 50 / 100 |
| Batch size | 4 / 6 / 10 |
| Image size | 256 × 256, 512 × 512 |
| Optimizer | AdamW |
| Framework | PyTorch |

---

## 📊 Metrik Evaluasi

Evaluasi model dilakukan menggunakan:
- **mIoU (Mean Intersection over Union)**
- **Precision**
- **Recall**
- **F1 Score**
- **Accuracy**

---

## 📈 Hasil Perbandingan Model

| Model | mIoU | Precision | Recall | F1 | Accuracy |
|-----|-----|----------|--------|----|----------|
| UNet | 0.46 | 0.57 | 0.59 | 0.57 | 0.83 |
| UNet + ResNet-34 | 0.58 | 0.71 | 0.70 | 0.68 | 0.90 |
| **UNet + ResNet-50** | **0.70** | **0.80** | **0.80** | **0.79** | **0.93** |

### Analisis
- **UNet + ResNet-50** memberikan performa terbaik
- Backbone pretrained membantu meningkatkan kualitas segmentasi
- UNet tanpa pretrained memiliki performa terendah pada IoU dan F1

---

## 🖼 Contoh Hasil Segmentasi

Model menghasilkan output berupa:
- Ground truth mask
- Predicted mask
- Overlay antara image asli dan hasil prediksi

Perbedaan kualitas prediksi terlihat jelas antar model, terutama pada batas objek dan konsistensi kelas.

---

## ✅ Kesimpulan

- Semantic segmentation efektif untuk pemahaman lingkungan pada self driving car
- UNet dengan backbone ResNet-50 memberikan hasil paling optimal
- Penggunaan pretrained backbone sangat membantu pada dataset terbatas

---

## 🔮 Future Work

- Menggunakan dataset yang lebih besar dan beragam
- Eksplorasi arsitektur lain (DeepLab, HRNet)
- Optimasi inference untuk real-time application
- Integrasi ke pipeline autonomous driving

---

## 📚 Referensi

- UNet: Convolutional Networks for Biomedical Image Segmentation
- ResNet: Deep Residual Learning for Image Recognition
- Roboflow Dataset
