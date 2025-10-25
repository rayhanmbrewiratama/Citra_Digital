# THRESHOLDING CITRA: Perbandingan Segmentasi Lokal dan Global

## Deskripsi Proyek

Repositori ini berisi kode Python yang mendemonstrasikan dan membandingkan berbagai teknik **Thresholding** sebagai metode dasar untuk **Segmentasi Citra** dalam Pengolahan Citra Digital (PID).

Thresholding adalah proses memisahkan piksel citra menjadi dua kategori (umumnya _foreground_ dan _background_) berdasarkan perbandingan nilai intensitas piksel dengan nilai ambang ($T$) tertentu. Fokus utama demonstrasi ini adalah mengatasi tantangan **pencahayaan yang tidak merata** pada citra.

### Metodologi Perbandingan

Kode ini membandingkan tiga kategori penentuan nilai ambang ($T$):

| Kategori            | Metode                                    | Prinsip Kerja                                                                                              | Keunggulan/Kelemahan                                                                                                                            |
| :------------------ | :---------------------------------------- | :--------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------- |
| **Global Manual**   | `cv2.THRESH_BINARY`                       | $T$ ditetapkan secara manual untuk seluruh citra.                                  | Cepat, tetapi sangat tidak akurat jika pencahayaan tidak merata.                                                   |
| **Global Otomatis** | **Otsu's Method** (`cv2.THRESH_OTSU`)     | $T$ tunggal dihitung secara otomatis untuk memaksimalkan varians antar kelas. | Optimal untuk citra dengan histogram bimodal , tetapi gagal jika pencahayaan tidak merata. |
| **Adaptive/Lokal**  | **Adaptive Mean** & **Adaptive Gaussian** | $T$ dihitung secara _lokal_ dari _neighborhood_ setiap piksel.                | **Solusi terbaik** untuk citra dengan pencahayaan tidak merata, _shadow_, atau _highlight_.                             |

---

##  File: `thresholding_comparison.py`

Kode utama dibuat dalam _script_ Python ini untuk menjalankan langkah-langkah demonstrasi secara berurutan.

### Langkah-langkah Utama Kode

1.  **Import Pustaka:** Mengimpor `cv2` (OpenCV), `numpy`, dan `matplotlib.pyplot`.
2.  **Generate Citra Uji:**
    - Membuat citra sintetis untuk mensimulasikan **pencahayaan yang tidak seragam** (gradien horizontal).
    - Menyisipkan **objek uji** (kotak abu-abu) di tengah citra.
3.  **Aplikasi Global Thresholding:**
    - [cite\_start]Menerapkan _Thresholding_ Manual ($T=127$)[cite: 126].
    - [cite\_start]Menerapkan _Otsu's Method_ (`cv2.THRESH_OTSU`) untuk mencari _threshold_ optimal[cite: 201].
4.  **Aplikasi Adaptive Thresholding:**
    - [cite\_start]Menerapkan **Adaptive Mean** (`cv2.ADAPTIVE_THRESH_MEAN_C`)[cite: 225].
    - [cite\_start]Menerapkan **Adaptive Gaussian** (`cv2.ADAPTIVE_THRESH_GAUSSIAN_C`)[cite: 225].
    - [cite\_start]Parameter yang digunakan mencakup `blockSize` (ukuran _neighborhood_) dan $C$ (konstanta yang dikurangi dari mean/weighted mean)[cite: 230, 231].
5.  **Visualisasi Hasil:** Menampilkan citra asli dan semua hasil segmentasi biner dalam satu plot _grid_ menggunakan `matplotlib` untuk perbandingan visual kualitatif.

---

##  Persyaratan Sistem

Untuk menjalankan kode ini, Anda memerlukan lingkungan Python dengan pustaka berikut:

- **Python 3.x**
- **OpenCV** (`opencv-python`)
- **NumPy** (`numpy`)
- **Matplotlib** (`matplotlib`)

### Instalasi Dependensi

Anda dapat menginstal semua pustaka yang diperlukan menggunakan `pip`:

```bash
pip install opencv-python numpy matplotlib
```
