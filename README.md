# Vehicle Speed Estimation

Proyek ini melakukan estimasi kecepatan kendaraan pada video menggunakan deteksi objek (YOLOv8) dan pelacakan (DeepSORT), serta transformasi perspektif untuk mengukur jarak nyata.

## Fitur

- Deteksi kendaraan (mobil, motor, bus, truk, sepeda) pada video.
- Pelacakan setiap kendaraan antar frame.
- Estimasi kecepatan berdasarkan konversi piksel ke meter dan FPS video.
- Menyimpan hasil statistik ke file CSV untuk analisis lebih lanjut.

## Struktur Proyek

- `dataset/`: Folder berisi video yang ingin dideteksi dan diestimasi kecepatannya.
- `vehicle_speed_estimation.ipynb`: Notebook utama untuk deteksi, pelacakan, dan estimasi kecepatan.
- `yolov8m.pt`: Bobot model YOLOv8.
- `dataset/coco.names`: Daftar nama kelas untuk deteksi.
- `out_video/`: Folder hasil video yang sudah diberi bounding box dan estimasi kecepatan.
- `out_csv/`: Folder hasil file CSV berisi statistik lengkap kendaraan yang terdeteksi dan diestimasi kecepatannya.
- `README.md`: Dokumentasi proyek.

## Cara Penggunaan

1. Letakkan video input pada folder `dataset/`.
2. Jalankan `vehicle_speed_estimation.ipynb` di Jupyter Notebook atau VS Code.
3. Pilih ROI dan titik kalibrasi sesuai instruksi di notebook.
4. Proses akan berjalan, hasil video akan tersimpan di `out_video/` dan statistik kendaraan di `out_csv/`.

## Kebutuhan

- Python 3.8+
- OpenCV
- Ultralytics YOLO
- DeepSORT-Realtime
- Supervision
- Pandas
- Torch

Instalasi dependensi:

```sh
pip install -
```
