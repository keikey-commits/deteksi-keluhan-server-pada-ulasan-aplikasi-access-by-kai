# Analisis Komparatif Kinerja SVM dan Bi-LSTM dalam Deteksi Keluhan Server pada Ulasan Aplikasi KAI Access.
Kelompok 8 (2024 E)
Ananda Keissa Az Zahra (24031554051), Laili Nurrohmatul Fadhila Z. (24031554093), Eka Putri Maharani (24031554121)

Proyek ini bertujuan untuk membangun sistem klasifikasi teks otomatis guna mendeteksi ulasan pengguna yang berkaitan dengan gangguan teknis server (seperti *downtime*, kegagalan *payment gateway*, atau *error* konektivitas) pada aplikasi **Access by KAI**. 

Dataset dan pelabelan: Scraping dari ulasan Google Play Store Access by KAI dengan pelabelan secara manual

---

## Fitur Utama & Metodologi

1. **Text Augmentation:** 
   Mengatasi keterbatasan data menggunakan teknik *Synonym Replacement*, *Random Swap*, dan *Random Deletion*, yang sukses menggandakan dataset dari 3.180 baris menjadi 6.360 ulasan.
2. **Feature Extraction:**
   * **FastText:** Diterapkan langsung pada teks augmentasi untuk menangkap variasi *sub-word* dan kosakata baru/informal.
   * **IndoBERT:** Diterapkan menggunakan teknik duplikasi teks asli untuk menjaga keutuhan struktur tata bahasa dan perhitungan *Self-Attention*.
3. **Hyperparameter Tuning:**
   * **GridSearchCV (10-Fold CV)** untuk mencari kombinasi *Kernel*, *C*, dan *Gamma* terbaik pada SVM.
   * **Optuna (TPE Algorithm)** untuk mengoptimasi unit LSTM, *Dense Layer*, *Dropout*, *Learning Rate*, dan *Batch Size* pada model Bi-LSTM.

---

## Hasil Eksperimen



### Mengapa SVM + IndoBERT?
Selain memenangkan metrik evaluasi F1-Score secara telak, model SVM dipilih sebagai arsitektur yang paling direkomendasikan karena:
1. **Beban Komputasi Rendah:** Tidak membutuhkan infrastruktur GPU yang berat saat di-*deploy* ke dalam sistem.
2. **Kecepatan Inferensi:** Mampu memproses lonjakan antrean (*bottleneck*) teks ulasan saat aplikasi KAI mengalami *down* secara *real-time* dengan jauh lebih cepat dibandingkan prediksi sekuensial Bi-LSTM.
3. **Stabilitas:** Menghasilkan simpangan baku (± 0.88%) yang sangat kecil selama proses *10-Fold Cross Validation*.

---

## 🛠️ Cara Menjalankan Proyek

1. **Clone Repositori:**
```bash
   git clone [https://github.com/username-kamu/nama-repo.git](https://github.com/username-kamu/nama-repo.git)
   cd nama-repo
