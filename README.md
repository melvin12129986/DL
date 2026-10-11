
```markdown
# 🐾 Image Classification: Oxford-IIIT Pet Dataset (10 Selected Breeds)

Repositori ini berisi implementasi eksperimen klasifikasi gambar untuk membedakan **5 ras kucing** dan **5 ras anjing** pilihan dari dataset **Oxford-IIIT Pet** menggunakan PyTorch. Eksperimen ini mencakup perbandingan pelatihan model dari awal (*from scratch*), *Feature Extraction*, *Fine-Tuning*, hingga pengujian model efisien untuk perangkat *edge*.

---

## 📊 Ringkasan Hasil Eksperimen

Berdasarkan pengujian yang telah dilakukan selama masing-masing 3 epoch, berikut adalah perbandingan performa dari berbagai konfigurasi model:

| Skenario / Model | Strategi Pelatihan | Jumlah Parameter Aktif | Epoch Terbaik | Akurasi Validasi | Macro F1-Score |
| :--- | :--- | :--- | :---: | :---: | :---: |
| **B1: ResNet18 (Scratch)** | Pelatihan penuh dari nol | 11,689,512 | 3 | 22.50% | 0.2048 |
| **B2: ResNet18 (Feature Extraction)** | Hanya melatih Classifier Head (FC) | 5,120 | 3 | 88.50% | 0.8826 |
| **B3 S1: ResNet18 (Fine-Tuning)** | **Melatih Layer 4 + FC (Tanpa Augmentasi)** | **8,393,856** | **2** | **93.50%** | **0.9315** |
| **B3 S2: ResNet18 (Fine-Tuning)** | Melatih Layer 4 + FC (Dengan Augmentasi) | 8,393,856 | 3 | 89.50% | 0.8993 |
| **B5: MobileNetV3-Small** | Melatih Stage Terakhir + FC | 657,546 | 3 | 88.00% | 0.8834 |

### 🔑 Temuan Utama:
1. **Model Terbaik:** **ResNet18 Fine-Tuning (Skenario B3 S1)** mencapai akurasi tertinggi sebesar **93.50%** dan F1-score **0.9315** pada epoch ke-2.
2. **Efisiensi Model (MobileNetV3):** MobileNetV3-Small mampu menghasilkan akurasi yang kompetitif (**88.00%**) hanya dengan **~5.7%** total parameter dari ResNet18, menjadikannya pilihan ideal untuk deployment pada perangkat berspesifikasi rendah.
3. **Analisis Representasi (Feature Map):** Melalui visualisasi aktivasi `layer4` sebelum vs sesudah fine-tuning, terlihat jelas bahwa proses fine-tuning berhasil menggeser fokus deteksi model dari fitur latar belakang umum langsung ke detail spesifik wajah dan telinga hewan.

---

## 🛠️ Cara Menjalankan Proyek

### 1. Kebutuhan Lingkungan (Prerequisites)
Pastikan Anda memiliki Python 3.8+ dan CUDA terinstal jika ingin menggunakan GPU untuk mempercepat proses training.

### 2. Instalasi Pustaka
Pasang seluruh pustaka yang dibutuhkan menggunakan perintah:
```bash
pip install -r requirements.txt
```

### 3. Struktur Dataset
Dataset **Oxford-IIIT Pet** akan otomatis diunduh dan difilter pada saat skrip pertama kali dijalankan ke dalam folder `./data`.

---

## 📁 Isi File Proyek
- `combined_training_logs.csv`: Log hasil metrik loss, akurasi, dan F1-score per epoch untuk setiap skenario.
- `notebook.ipynb`: Jupyter Notebook berisi seluruh alur eksplorasi data, training, evaluasi, analisis misklasifikasi, hingga analisis peta aktivasi (*feature maps*).
```

