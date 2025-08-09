# A/B Testing — CTA Button Optimization

Analisis A/B Testing untuk menguji dampak perubahan warna dan teks pada CTA button di halaman produk e-commerce terhadap **conversion rate**.

## 1. Latar Belakang
Perusahaan e-commerce ingin meningkatkan *purchase conversion rate* pada halaman produk. Tim marketing menduga bahwa mengganti **CTA button** biru standar menjadi hijau dengan teks persuasif dapat meningkatkan konversi.

**KPI utama:** Conversion Rate (CR)  
**Metric pendukung:** Average Order Value (AOV), Bounce Rate  

## 2. Hipotesis
- **H₀ (Null Hypothesis):** Tidak ada perbedaan CR antara versi A (CTA biru) dan versi B (CTA hijau + teks baru).  
- **H₁ (Alternative Hypothesis):** Versi B memiliki CR lebih tinggi daripada versi A.  

Jenis uji: one-sided two-proportion z-test (karena hipotesis arah: B > A).

## 3. Rancangan Eksperimen
- **Unit randomisasi:** Unique visitors pada halaman produk.  
- **Pembagian traffic:** 50% ke versi A, 50% ke versi B.  
- **Periode eksperimen:** 14 hari untuk menangkap variasi harian & mingguan.  
- **Stopping rule:** Fixed horizon — berhenti saat jumlah sampel tercapai.  
- **Metric guardrails:** Pantau AOV dan bounce rate.

## 4. Perhitungan Ukuran Sampel
**Asumsi awal:**  
- Baseline CR (p₁) = 2.0% (0.020)  
- MDE (Minimal Detectable Effect) = 20% uplift relatif → p₂ = 0.024  
- α = 0.05 (one-sided), Power = 0.8  

**Hasil:** ± 78.000 user per grup.

## 5. Data & Metode Analisis
Dataset simulasi dibuat menggunakan Python (`pandas`, `numpy`).  
Analisis menggunakan **two-proportion z-test** (SciPy) dan visualisasi dengan **Matplotlib**.

## 6. Hasil Utama
| Variant | n       | Conversions | CR     |
|---------|---------|-------------|--------|
| A       | 80.000  | 1.600       | 2.00%  |
| B       | 80.000  | 1.920       | 2.40%  |

**Z-score:** 6.192  
**P-value (one-sided):** 2.97 × 10⁻¹⁰ → **signifikan** (p < 0.05)

## 7. Visualisasi
![Conversion Rate Chart](assets/plots.png)  
Grafik menunjukkan CR variant B lebih tinggi daripada variant A, dengan *confidence interval* 95%.

## 8. Interpretasi Bisnis
- Variant B memberikan uplift absolut **+0.40 percentage point** dan uplift relatif **+20%**.  
- Estimasi dampak: jika traffic bulanan 1 juta visitor dan AOV = $50, maka pendapatan tambahan ≈ **$200.000/bulan**.  
- Rekomendasi: rollout bertahap (10% → 25% → 100%) sambil memantau AOV & bounce rate.

## 9. Cara Menjalankan Analisis
```bash
pip install -r requirements.txt
jupyter notebook analysis.ipynb