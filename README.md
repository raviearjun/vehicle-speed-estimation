# Estimasi Kecepatan Kendaraan menggunakan YOLOv8 & DeepSORT

Proyek ini mendemonstrasikan sistem real-time untuk mendeteksi, melacak, dan mengestimasi kecepatan kendaraan dari sebuah video. Sistem ini menggunakan YOLOv8 untuk deteksi objek dan DeepSORT untuk pelacakan.

Transformasi perspektif digunakan untuk mengubah tampilan menjadi bird's-eye view agar pengukuran jarak lebih akurat (dalam meter) yang kemudian dikonversi menjadi kecepatan (km/jam).

## Contoh Hasil

> ![gif - Made with Clipchamp (1)](https://github.com/user-attachments/assets/dbce0494-bb36-4787-aa74-f1e7987e04ce)


## Fitur Utama

- **Deteksi Objek Presisi Tinggi:** YOLOv8 untuk berbagai jenis kendaraan (mobil, motor, bus, truk, sepeda).
- **Pelacakan yang Robust:** DeepSORT melacak setiap kendaraan dengan ID unik.
- **Transformasi Perspektif:** ROI ditransformasi ke bird's-eye view untuk pengukuran.
- **Estimasi Kecepatan:** Konversi perpindahan piksel ke km/jam berdasarkan rasio meter/piksel.
- **Analisis Data:** Data kecepatan (rata-rata, median, min, maks) disimpan ke CSV.
- **Visualisasi:** Video output dianotasi dengan bounding box, ID, dan kecepatan.

## Cara Kerja Sistem

1. **Seleksi ROI:** Pengguna memilih area jalan dalam video.
2. **Kalibrasi Perspektif:** ROI diubah ke bird's-eye view, lalu dua titik diklik untuk mengukur jarak nyata (meter) terhadap jarak piksel.
3. **Deteksi & Pelacakan:**
   - YOLOv8 mendeteksi kendaraan pada setiap frame.
   - DeepSORT memberikan ID dan melacak kendaraan.
4. **Perhitungan Kecepatan:**
   - Titik tengah bounding box dikonversi ke bird's-eye view.
   - Dihitung jarak (meter) dan dibagi waktu antar frame (1/FPS), dikonversi ke km/jam.
5. **Output:** Video hasil dan file CSV kecepatan tersimpan.

## Struktur Proyek

```
vehicle-speed-estimation/
├── dataset/
│   └── Amplaz02a_part_2.mp4
├── out_csv/
│   └── Amplaz02a_part2.csv
├── out_video/
│   └── Amplaz02a_final_part2.mp4
├── vehicle_speed_estimation.ipynb
├── yolov8m.pt
├── README.md
└── requirements.txt
```

## ⚙️ Instalasi & Pengaturan

### 1. Clone Repository

```bash
git clone https://github.com/YOUR_USERNAME/vehicle-speed-estimation.git
cd vehicle-speed-estimation
```

### 2. Virtual Environment

#### Conda:

```bash
conda create --name speed-env python=3.10
conda activate speed-env
```

#### Venv (Python bawaan):

```bash
# Mac/Linux
python3 -m venv speed-env
source speed-env/bin/activate

# Windows
python -m venv speed-env
.\speed-env\Scriptsctivate
```

### 3. Instal Dependensi

**Isi `requirements.txt`:**

```
ultralytics==8.3.146
supervision==0.25.1
deep-sort-realtime==1.3.2
numpy==2.2.6
torch==2.5.1
opencv-python==4.11.0
matplotlib==3.10.3

```

Lalu jalankan:

```bash
pip install -r requirements.txt
```

### 4. Unduh Bobot YOLOv8

```bash
# wget
wget https://github.com/ultralytics/assets/releases/download/v0.0.0/yolov8m.pt

# atau curl
curl -L https://github.com/ultralytics/assets/releases/download/v0.0.0/yolov8m.pt -o yolov8m.pt
```

Letakkan `yolov8m.pt` di folder utama.

## Cara Menjalankan

1. **Letakkan Video:** Taruh di `dataset/`.
2. **Buka Notebook:** `vehicle_speed_estimation.ipynb`
3. **Atur Path di Sel 6:**

```python
SOURCE_VIDEO_PATH = "dataset/nama_video_anda.mp4"
OUTPUT_VIDEO_PATH = "out_video/hasil_video_anda.mp4"
```

4. **Pilih ROI:** Jalankan sel "Select ROI" → klik 4 titik → tekan `s`.

5. **Kalibrasi Jarak:** Klik 2 titik (objek dengan panjang nyata diketahui). Rasio meter/piksel dihitung dari:  
   `jarak_asli_dalam_meter / jarak_terukur_dalam_piksel`.

6. **Update Fungsi di Sel 14:**

```python
def calculate_distance(p1, p2):
    return np.sqrt((p2[0] - p1[0])**2 + (p2[1] - p1[1])**2) * 0.0297 # Ganti dengan rasio Anda
```

7. **Jalankan Proses Utama:** Jalankan sel-sel berikutnya.

8. **Lihat Hasil:**
   - Video: `out_video/`
   - CSV: `out_csv/`

---

> 📧 Untuk pertanyaan lebih lanjut, silakan hubungi pengembang proyek ini.
