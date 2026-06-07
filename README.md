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

<img width="1389" height="590" alt="Image" src="https://github.com/user-attachments/assets/7e3f19cc-368c-45ce-84a4-2837897647bf" />

### Mengapa SVM + IndoBERT?

Model **SVM + IndoBERT** ditetapkan sebagai arsitektur *State-of-the-Art* (SOTA) dan paling direkomendasikan dalam eksperimen ini berdasarkan keunggulan mutlak pada metrik evaluasi:

1. **Capaian F1-Macro Tertinggi (96.85%):** Sinergi ini terbukti paling tanggap dan seimbang dalam membedakan keluhan server yang sesungguhnya dari ulasan umum. Angka ini mengalahkan seluruh skenario pemodelan *Deep Learning* (Bi-LSTM) maupun representasi *sub-word* (FastText).
2. **Nilai ROC-AUC yang Impresif (0.9327):** Skor ini menunjukkan probabilitas diskriminasi kelas yang sangat baik. Model sangat teliti dan tangguh sehingga meminimalisir kemungkinan model salah menebak (*False Positive*) pada berbagai rentang batas probabilitas (*threshold*).

Kemampuan arsitektur *Transformer* pada IndoBERT dalam menangkap konteks kalimat secara utuh, dipadukan dengan efisiensi algoritma SVM dalam menemukan margin pemisah (*hyperplane*) yang optimal, menjadikannya solusi klasifikasi teks yang paling presisi untuk ulasan aplikasi Access by KAI.
