🐾 Oxford-IIIT Pet Image Classification (Transfer Learning vs Fine-Tuning)
Repositori ini berisi implementasi eksperimen klasifikasi gambar untuk 10 kelas pertama dari dataset Oxford-IIIT Pet menggunakan framework PyTorch. Kami membandingkan performa model ResNet-18 (yang dilatih dari awal, transfer learning, dan progresif fine-tuning) serta model EfficientNet-B0.

👥 Identitas Anggota Kelompok
Nama Anggota 1 - NIM
Nama Anggota 2 - NIM
🔬 Skenario Eksperimen
Kami melakukan pengujian pada 5 kondisi eksperimen yang berbeda:

B1: Baseline Scratch (ResNet-18)

Melatih arsitektur ResNet-18 dari awal tanpa menggunakan bobot pra-latih (pre-trained weights).
Menggunakan augmentasi data penuh.
B2: Feature Extraction (ResNet-18)

Menggunakan bobot pre-trained ImageNet.
Membekukan seluruh parameter ekstraktor fitur dan hanya melatih Fully Connected (FC) layer.
Menggunakan augmentasi data penuh.
B3: Progressive Fine-Tuning (ResNet-18)

Menggunakan bobot pre-trained ImageNet.
Membekukan parameter awal, namun membuka kunci latihan untuk layer4 (dengan LR  10−4 ) dan FC layer (dengan LR  10−3 ).
Menggunakan augmentasi data penuh.
B4_NoAug: Progressive Fine-Tuning Tanpa Augmentasi (ResNet-18)

Konfigurasi model dan pembelajaran sama persis dengan B3.
Dataset hanya diubah ukurannya dan di-center crop tanpa augmentasi gambar (seperti rotasi atau pergeseran warna).
B5: EfficientNet-B0 Fine-Tuning

Menggunakan arsitektur EfficientNet-B0 dengan bobot pre-trained ImageNet.
Melatih blok teratas (features[8]) dan bagian kepala klasifikasi (classifier head).
Menggunakan augmentasi data penuh.
📈 Hasil Evaluasi & Metrik
Seluruh performa model dievaluasi menggunakan metrik Akurasi Validasi, Akurasi Test, dan Macro F1-Score. Hasil ringkasan eksperimen disimpan otomatis ke dalam berkas metrics_log.csv dan metrics_log.json.

Perbandingan Singkat:
Model B1 (Scratch) cenderung memiliki performa paling rendah karena melatih jutaan parameter dengan data terbatas dari awal.
Model B2 (Feature Extraction) menunjukkan konvergensi yang sangat cepat dengan performa yang solid.
Model B3 (Fine-Tuning) dan B5 (EfficientNet) memberikan akurasi terbaik karena model mampu menyesuaikan representasi fitur abstrak tingkat tinggi ke bentuk dataset spesifik ini.
📂 Struktur Output File
metrics_log.csv & metrics_log.json: Log metrik performa masing-masing skenario.
loss_comparison_B1_B2_B3.png: Grafik perbandingan training & validation loss untuk model B1, B2, dan B3.
failure_analysis_samples.png: Sampel gambar test set yang salah diprediksi oleh model terbaik (B3) beserta skor keyakinannya (confidence score).
