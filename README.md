# Laporan Praktikum Kecerdasan Buatan - Pertemuan 9
## Implementasi Algoritma Genetika untuk 0/1 Knapsack

**NIM:** H1D024018 | **Topik:** Algoritma Genetika

---

## 1. Pendahuluan

Praktikum ini mengimplementasikan **Algoritma Genetika (GA)** untuk menyelesaikan masalah **0/1 Knapsack**. 

**0/1 Knapsack:** Memilih barang dengan nilai maksimal tanpa melampaui kapasitas tas (50 unit).

**Algoritma Genetika** menyelesaikan dengan: inisialisasi populasi → seleksi → crossover → mutasi → iterasi hingga konvergensi.

---

## 2. Modul-Modul Program

### 2.1 Arsitektur
```
main.py ← InisialisasiPopulasi.py ← EvaluasiFitness.py
      ← selection.py ← crossover.py ← mutation.py
```

### 2.2 Data Barang (9 item, Kapasitas: 50)
| Barang | Nilai | Bobot | Barang | Nilai | Bobot |
|--------|-------|-------|--------|-------|-------|
| B1 | 60 | 10 | B6 | 70 | 9 |
| B2 | 100 | 20 | B7 | 80 | 15 |
| B3 | 120 | 30 | B8 | 90 | 10 |
| B4 | 90 | 25 | B9 | 25 | 3 |
| B5 | 69 | 11 | | | |

---

## 3. Penjelasan Modul

### 3.1 InisialisasiPopulasi.py
Membuat populasi awal dengan gen biner acak. Gen 1 = barang dipilih, Gen 0 = tidak dipilih.
```python
def inisialisasi_populasi(jumlah_populasi, jumlah_gen)
```
Contoh: `[1, 0, 1, 0, 1, 1, 0, 1, 0]` untuk 9 barang.

### 3.2 EvaluasiFitness.py
Menghitung nilai fitness = total nilai barang (jika bobot ≤ kapasitas, else 0).
```python
def hitung_fitness(kromosom, barang, kapasitas_tas)
```
Rumus:
```
Fitness = Σ nilai jika Σ bobot ≤ kapasitas
Fitness = 0 jika Σ bobot > kapasitas
```

### 3.3 selection.py
**Roulette Wheel Selection:** Seleksi berbanding lurus dengan fitness.
**Tournament Selection:** Pilih k individu acak, ambil yang terbaik.

### 3.4 crossover.py
Tiga tipe penyilangan menghasilkan anak dari 2 orang tua:

| Tipe | Deskripsi | Contoh |
|------|-----------|--------|
| **One-Point** | Potong 1 titik, tukar bagian | `[1,0\|0,0,1]` |
| **Two-Point** | Potong 2 titik, tukar tengah | `[1\|1,0\|1,0]` |
| **Uniform** | Pakai mask, tukar posisi tertentu | Mask-based swap |

### 3.5 mutation.py
Mengubah gen untuk eksplorasi:

| Tipe | Aksi |
|------|------|
| **Swap** | Tukar 2 posisi acak |
| **Inversion** | Balik urutan gen |
| **Uniform** | Flip gen dengan prob 0.1 |

### 3.6 main.py
Program utama dengan parameter:
- **Generasi:** 50
- **Populasi:** 20
- **Prob. Crossover:** 0.5
- **Prob. Mutasi:** 0.1
- **Kapasitas:** 50

**Alur:**
1. Inisialisasi 20 individu acak
2. Setiap generasi: seleksi → crossover → mutasi
3. Tampilkan grafik fitness & solusi terbaik

---

## 4. Hasil & Analisis

**Konfigurasi:**
- Generasi: 50 | Populasi: 20 | Crossover: 0.5 | Mutasi: 0.1

**Grafik Output:**
- Garis Biru: Fitness tertinggi per generasi
- Garis Kuning: Fitness terendah per generasi  
- Garis Merah: Fitness rata-rata per generasi
- Titik Abu-abu: Semua nilai fitness individu

**Analisis:** Fitness meningkat progresif dan stabil setelah beberapa generasi, menunjukkan konvergensi algoritma.

---

## 5. Teori Singkat

**Istilah Kunci:**
- **Kromosom:** Solusi (array biner)
- **Gen:** Elemen solusi (0 atau 1)
- **Fitness:** Kualitas solusi
- **Seleksi:** Pilih individu baik
- **Crossover:** Kombinasi 2 solusi
- **Mutasi:** Perubahan acak

**Keunggulan GA:**
✓ Fleksibel & robust untuk optimasi  
✓ Tidak perlu derivat  
✓ Tidak terjebak optimal lokal (karena mutasi)

**Keterbatasan:**
✗ Konvergensi lambat  
✗ Sensitif terhadap parameter  
✗ Hasil tidak dijamin optimal

---

## 6. Cara Menjalankan

**Instalasi:**
```bash
pip install matplotlib numpy
```

**Jalankan:**
```bash
python main.py
```

**Ubah Parameter (opsional):**
Edit baris terakhir `main.py`:
```python
run_ga(jumlah_generasi=100, jumlah_populasi=50, 
       prob_crossover=0.7, prob_mutasi=0.2, kapasitas_tas=50)
```

---