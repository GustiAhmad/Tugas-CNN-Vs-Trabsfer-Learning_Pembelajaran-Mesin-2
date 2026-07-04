
# Klasifikasi Citra Biner: CNN dari Dasar (From Scratch) vs Transfer Learning

Proyek ini merupakan eksperimen komparatif untuk mendeteksi dan mengklasifikasikan citra digital biner (Kucing dan Anjing) menggunakan dua pendekatan deep learning yang berbeda: Convolutional Neural Network (CNN) yang dibangun dari dasar (*from scratch*) dan *Transfer Learning* memanfaatkan arsitektur pretrained model MobileNetV2 dengan strategi *Feature Extraction*.

## Identitas
* **Nama** : Gusti Ahmad Muttahid Bilhaq
* **NIM**  : 442023611097
* **Prodi**: Teknik Informatika, Universitas Darussalam Gontor

## Struktur Direktori Repository

project-cnn-vs-transfer-learning/
├── dataset/
│   └── link_dataset.txt
├── notebook/
│   └── cnn_vs_transfer_learning.ipynb
├── report/
│   └── laporan.pdf
├── README.md
└── requirements.txt

## Deskripsi dan Sumber Dataset
Eksperimen ini memanfaatkan dua sumber dataset terbuka yang berbeda untuk memenuhi ketentuan tugas:

1. **Eksperimen 1 (CNN dari Dasar)**
   * **Dataset:** CIFAR-10 Sub-kelas Kucing (*Cat*) dan Anjing (*Dog*)
   * **Resolusi:** 32 x 32 piksel (RGB)
   * **Sumber:** `torchvision.datasets.CIFAR10`
   * **Proporsi:** 8.400 sampel Latihan (70%), 1.800 sampel Validasi (15%), 1.800 sampel Pengujian (15%). Total: 12.000 gambar.

2. **Eksperimen 2 (Transfer Learning)**
   * **Dataset:** Microsoft Cats vs Dogs Dataset
   * **Resolusi:** 224 x 224 piksel (RGB)
   * **Sumber:** [Kaggle - Shaun The Sheep / Microsoft Cats vs Dogs](https://www.kaggle.com/datasets/shaunthesheep/microsoft-catsvsdogs-dataset)
   * **Proporsi:** 2.800 sampel Latihan (70%), 600 sampel Validasi (15%), 600 sampel Pengujian (15%) yang diekstraksi menggunakan *stratified sampling* dari total populasi. Total: 4.000 gambar.

## Rangkuman Hasil Eksperimen

| Parameter Evaluasi | Eksperimen 1: CNN dari Dasar | Eksperimen 2: Transfer Learning |
| :--- | :--- | :--- |
| **Arsitektur Model** | Custom Jaringan 3 Blok Konvolusi | MobileNetV2 (Feature Extraction) |
| **Jumlah Epoch** | 15 Epoch | 5 Epoch |
| **Akurasi Latihan** | 80.30% | 96.82% |
| **Akurasi Validasi** | 81.72% | 96.17% |
| **Akurasi Pengujian (Test)** | **79.83%** | **98.67%** |
| **Total Parameter** | 618,754 parameter | 2,226,434 parameter |
| **Waktu Pelatihan** | 44.47 detik | 60.85 detik |

## Cara Menjalankan Project

### 1. Instalasi Dependensi
Pastikan Anda telah memasang dependensi yang tercantum pada berkas `requirements.txt`. Anda dapat memasangnya menggunakan perintah berikut:
```bash
pip install torch torchvision numpy scikit-learn matplotlib seaborn kagglehub
```

### 2. Menjalankan Kode

1. Buka berkas `notebook/cnn_vs_transfer_learning.ipynb` menggunakan Jupyter Notebook, JupyterLab, atau Google Colab / Kaggle Notebook.
2. Pastikan lingkungan eksekusi (runtime) Anda sudah menggunakan akselerator GPU (CUDA) untuk performa komputasi yang optimal.
3. Jalankan sel kode dari atas ke bawah secara berurutan. Kode akan mengunduh dataset CIFAR-10 secara otomatis dan mengunduh dataset Kaggle menggunakan library resmi `kagglehub`.

## Ringkasan Analisis Perbandingan

* **Performa Klasifikasi:** Pendekatan *Transfer Learning* menggunakan MobileNetV2 memberikan performa akurasi pengujian yang jauh lebih superior (98.67%) dibandingkan dengan model CNN dari dasar (79.83%).
* **Efisiensi Waktu:** Metode *Feature Extraction* pada *Transfer Learning* membuktikan efisiensi konvergensi yang luar biasa, di mana akurasi tinggi dan kestabilan grafik loss tercapai hanya dalam 5 epoch pelatihan, memangkas waktu komputasi yang besar untuk mencapai akurasi optimal.
* **Pengaruh Resolusi:** Penggunaan resolusi citra input yang lebih tinggi (224 x 224 piksel) pada skenario *Transfer Learning* terbukti mempertahankan informasi spasial dan morfologi objek jauh lebih kaya dibandingkan citra resolusi rendah (32 x 32 piksel) milik CIFAR-10.