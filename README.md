# 🤖 Proyek Generasi Kalimat Bahasa Indonesia dengan CTVeeGAN

Proyek ini mendemonstrasikan cara menggunakan model **Conditional Time-series VEEGAN (CT-VEEGAN)** untuk menghasilkan kalimat (teks) baru dalam Bahasa Indonesia. Model ini memungkinkan kontrol atas sentimen atau kelas kalimat yang dihasilkan melalui parameter `label_class`.

## ⚙️ Persyaratan (Prasyarat)

Untuk menjalankan kode ini, Anda memerlukan lingkungan Python (disarankan menggunakan Google Colab seperti yang ditunjukkan dalam *notebook* asli).

### Instalasi Dependensi

Pastikan Anda menjalankan perintah instalasi berikut di lingkungan Anda:

```bash
# Versi spesifik scikit-learn diperlukan oleh ct-veegan
pip install scikit-learn==1.4.2

# Instalasi library utama CT-VEEGAN
pip install ct-veegan==0.2.5
```

## 🚀 Panduan Penggunaan

Ikuti langkah-langkah di bawah ini untuk menginisialisasi model dan menghasilkan kalimat.

### 1\. Inisialisasi Model

Impor `CTVeeGANWrapper` dan inisialisasi model. Wrapper akan otomatis mengunduh *checkpoint* model yang diperlukan.

```python
from ct_veegan.wrapper import CTVeeGANWrapper

# Inisialisasi model
gan = CTVeeGANWrapper()

# Ambil konfigurasi penting dari wrapper model
model_generator = gan.model
latent_dim = gan.latent_dim
latent_step_dim = gan.latent_step_dim
seq_len = gan.seq_len
device = gan.device
```

### 2\. Generasi Kalimat

Gunakan fungsi `generate_indonesian_sentences` untuk membuat kalimat baru.

#### Sintaks Fungsi

```python
generate_indonesian_sentences(
    model_generator,
    latent_dim,
    seq_len,
    latent_step_dim,
    device,
    n_generate=5,      # Jumlah kalimat yang ingin dibuat
    label_class=0      # Kelas sentimen (0 atau 1)
)
```

#### Contoh: Membuat 5 Kalimat dengan Sentimen Negatif (Kelas 0)

```python
from ct_veegan.utils import generate_indonesian_sentences

sentences_negatif = generate_indonesian_sentences(
    model_generator=model_generator,
    latent_dim=latent_dim,
    seq_len=seq_len,
    latent_step_dim=latent_step_dim,
    device=device,
    n_generate=5,
    label_class=0 # Asumsi label 0 adalah Sentimen Negatif/Keluhan
)

print("--- Hasil Generasi (Kelas 0: Negatif) ---")
for s in sentences_negatif:
    print(s)
```

#### Contoh: Membuat 5 Kalimat dengan Sentimen Positif (Kelas 1)

Untuk menghasilkan kalimat yang cenderung positif atau memuji, ubah nilai `label_class` menjadi `1`.

```python
sentences_positif = generate_indonesian_sentences(
    model_generator=model_generator,
    latent_dim=latent_dim,
    seq_len=seq_len,
    latent_step_dim=latent_step_dim,
    device=device,
    n_generate=5,
    label_class=1 # Asumsi label 1 adalah Sentimen Positif/Pujian
)

print("\n--- Hasil Generasi (Kelas 1: Positif) ---")
for s in sentences_positif:
    print(s)
```

