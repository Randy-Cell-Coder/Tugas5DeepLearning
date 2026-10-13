# 🐾 Oxford-IIIT Pet Image Classification
### *A Deep Learning Study on Transfer Learning vs. Fine-Tuning Strategies*

---

## 👥 Identitas Kelompok

| 👤 Nama Anggota | 🆔 NIM |
| :--- | :--- |
| **[Randy adika Fathoni]** | [2802054604] |

---

## 📌 Ringkasan Proyek

Proyek ini berfokus pada eksperimen klasifikasi gambar menggunakan **10 kelas pertama** dari dataset populer **Oxford-IIIT Pet**. Kami menganalisis, membandingkan, dan mengevaluasi efektivitas arsitektur modern **ResNet-18** dan **EfficientNet-B0** di bawah berbagai kondisi latih (*training scenarios*), mulai dari pelatihan awal (*scratch*) hingga teknik pemangkasan adaptif (*fine-tuning*).

```
Target Kelas: ['Abyssinian', 'American Bulldog', 'American Pit Bull Terrier', 'Basset Hound', 
               'Beagle', 'Bengal', 'Birman', 'Bombay', 'Boxer', 'British Shorthair']
```

---

## 🧪 Skenario & Kondisi Eksperimen

Kami merancang **5 skenario eksperimen** terstruktur untuk melihat kontribusi *pre-trained weights* dan teknik augmentasi data:

### 🔴 1. `B1` | Baseline Scratch (ResNet-18)
* **Deskripsi:** Melatih seluruh arsitektur **ResNet-18** tanpa bantuan bobot pra-latih (inisialisasi acak).
* **Data Augmentation:** Aktif (Penuh).

### 🟡 2. `B2` | Feature Extraction (ResNet-18)
* **Deskripsi:** Menggunakan bobot *pre-trained* **ImageNet-1K**. Seluruh lapisan ekstraktor fitur dibekukan (*frozen*), hanya melatih bagian kepala klasifikasi (*Fully Connected layer*).
* **Data Augmentation:** Aktif (Penuh).

### 🟢 3. `B3` | Progressive Fine-Tuning (ResNet-18) `[Best ResNet-18 Model]`
* **Deskripsi:** Menggunakan bobot *pre-trained* **ImageNet-1K**. Blok atas (`layer4`) disetel halus dengan *learning rate* rendah ($10^{-4}$), sementara kepala klasifikasi dilatih dengan $10^{-3}$.
* **Data Augmentation:** Aktif (Penuh).

### 🔵 4. `B4_NoAug` | Progressive Fine-Tuning Tanpa Augmentasi (ResNet-18)
* **Deskripsi:** Konfigurasi model dan optimizer identik dengan **B3**, namun seluruh proses augmentasi dimatikan (hanya dilakukan *resize* & *center crop*).
* **Data Augmentation:** Non-aktif.

### 🟣 5. `B5` | EfficientNet-B0 Fine-Tuning
* **Deskripsi:** Menggunakan arsitektur efisien **EfficientNet-B0** pre-trained. Melatih blok representasi teratas (`features[8]`) dan kepala klasifikasi (*classifier head*).
* **Data Augmentation:** Aktif (Penuh).

---

## 📈 Evaluasi Metrik & Analisis Performa

Evaluasi dilakukan menggunakan metrik **Akurasi Validasi**, **Akurasi Test**, dan **Macro F1-Score**. Hasil tercatat rapi pada berkas output `metrics_log.csv` & `metrics_log.json`.

### 💡 Temuan Utama:
1. **Kekuatan Pre-trained Weights:** Model **B1** (*scratch*) memiliki akurasi paling rendah (~54% Test Acc) karena ukuran dataset yang terbatas. Transfer learning langsung melompati batas ini dengan akurasi melampaui **90%**.
2. **Pengaruh Augmentasi Data:** Skenario **B3** (dengan augmentasi) menunjukkan ketahanan generalisasi yang lebih stabil dan mencegah overfitting lebih baik dibanding skenario **B4_NoAug**.
3. **Efisiensi Arsitektur:** **EfficientNet-B0 (B5)** menghasilkan performa tinggi yang bersaing ketat dengan ResNet-18 namun menggunakan parameter latih (*trainable parameters*) jauh lebih sedikit.

---

## 📂 Struktur Output File & Artefak Eksperimen

Setelah eksekusi selesai, proyek ini menghasilkan beberapa berkas visualisasi penting di direktori kerja:
* **📊 `metrics_log.csv` & `metrics_log.json`**  
  Menyimpan detail numerik performa dari kelima skenario secara komprehensif.
* **📈 `loss_comparison_B1_B2_B3.png`**  
  Kurva perbandingan *training* dan *validation loss* yang memperlihatkan laju konvergensi model.
* **🔍 `failure_analysis_samples.png`**  
  Sampel visualisasi gambar dari test set yang gagal diprediksi dengan benar oleh model terbaik, lengkap dengan label asli (*ground truth*) vs label prediksi beserta persentase keyakinannya.
