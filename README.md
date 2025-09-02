[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/AdiEkaChandra/color-blindness-correction/blob/main/SDI_Hacktiv_Data_Adi_Eka_Chandra_Diana.ipynb)

# Evaluasi Efektivitas Koreksi Buta Warna (Color Blindness Correction)

## Gambaran Umum
Aksesibilitas visual merupakan aspek penting dalam desain digital. Salah satu tantangan utamanya adalah **buta warna** yang memengaruhi lebih dari 300 juta orang di seluruh dunia. Proyek ini bertujuan untuk mengevaluasi efektivitas **koreksi buta warna (daltonization)** dengan dataset publik dari Kaggle. Analisis difokuskan pada tiga defisiensi warna umum: **protanopia**, **deuteranopia**, dan **tritanopia**.  

## Dataset
- **Sumber**: [Color Blindness Simulation and Correction (Kaggle)](https://www.kaggle.com/datasets/sakshivyavahare20/color-blindness-simulation-and-correction)  
- **Struktur**:
  ```
  data/
    ├─ original/               
    ├─ simulated/             
    │   ├─ protanopia/
    │   ├─ deuteranopia/
    │   └─ tritanopia/
    └─ corrected/              
        ├─ protanopia/
        ├─ deuteranopia/
        └─ tritanopia/
  ```

## Proses Analisis
1. **Preprocessing**  
   - Menyamakan dimensi gambar untuk konsistensi.  
   - Konversi ke ruang warna **CIELAB**, karena lebih sesuai dengan persepsi manusia.  
   - Sampling piksel untuk perhitungan ΔE00.  

2. **Metrik yang Digunakan**  
   - **ΔE00 (CIEDE2000)** → mengukur perbedaan warna yang benar-benar dirasakan manusia.  
   - **SSIM** → mengevaluasi kesamaan struktur visual.  
   - **PSNR** → menilai kualitas sinyal gambar.  

3. **Analisis**  
   - Membandingkan *original vs simulated* (tingkat distorsi) dan *original vs corrected* (efektivitas koreksi).  
   - Menghitung **improvement**:  
     - `impr_ΔE00 = ΔE00_sim − ΔE00_cor`  
     - `impr_SSIM = SSIM_cor − SSIM_sim`  
     - `impr_PSNR = PSNR_cor − PSNR_sim`  
   - Hasil dihitung secara keseluruhan dan per tipe defisiensi.  

4. **Visualisasi**  
   - Diagram batang ΔE00 improvement per tipe defisiensi.  
   - Triplet gambar (Original – Simulated – Corrected) untuk contoh nyata.  

## Insight & Temuan
- **ΔE00 turun signifikan** (>50%), membuktikan koreksi mendekatkan warna ke kondisi normal.  
- **SSIM dan PSNR meningkat**, memastikan struktur dan kualitas gambar tetap terjaga.  
- **Protanopia & Deuteranopia** mendapat perbaikan paling besar, sementara **Tritanopia** moderat.  
- Insight ini menunjukkan bahwa daltonization efektif khususnya untuk kasus buta warna merah-hijau (yang paling umum secara global).  

## Kesimpulan & Rekomendasi
- **Kesimpulan**: Daltonization terbukti efektif meningkatkan aksesibilitas visual tanpa merusak persepsi normal.  
- **Rekomendasi**:  
  1. Integrasikan daltonization dalam **tool desain digital** (UI/UX, web).  
  2. Lakukan **user testing langsung** pada komunitas buta warna untuk validasi lebih lanjut.  
  3. Bangun fitur **pengecekan otomatis aksesibilitas warna** pada software desain.  

## Dukungan AI
AI digunakan pada dua bagian utama:  
1. **Machine Learning (RandomForestClassifier)** untuk baseline klasifikasi defisiensi → membuktikan distribusi warna tiap tipe berbeda.  
2. **Large Language Model (IBM Granite via LangChain)** untuk:  
   - Merangkum hasil numerik menjadi narasi laporan profesional.  
   - Mempercepat proses pelaporan dengan output yang konsisten.  

## Cara Menjalankan
1. Buka [Google Colab Notebook](https://colab.research.google.com/drive/1U_9B-K9bulpIPg2sgkNCyc2FjRyh5iCF?usp=sharing).  
2. Upload dataset ke folder `/content/data/` dengan struktur di atas (atau gunakan Kaggle API).  
3. Jalankan seluruh sel.   

## Struktur Repository
```
color-blindness-correction/
 ├─ SDI_Hacktiv_Data_Adi_Eka_Chandra_Diana.ipynb
 ├─ data/
 │   ├─ original/
 │   ├─ simulated/{protanopia,deuteranopia,tritanopia}/
 │   └─ corrected/{protanopia,deuteranopia,tritanopia}/
 └─ README.md
```

## Lisensi
Proyek ini dibuat untuk tujuan edukasi dalam program **IBM x Hacktiv8 Student Development Initiative**.
