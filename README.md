# Deteksi Warna
Berikut adalah kodingan untuk Algoritma Deteksi Warna :
```python

# Install library yang diperlukan
!pip install matplotlib opencv-python

# Import library
import cv2
import numpy as np
import matplotlib.pyplot as plt
from google.colab import files

# Fungsi untuk mengupload gambar
def upload_image():
    uploaded = files.upload()
    for filename in uploaded.keys():
        return filename

# Fungsi untuk mendeteksi warna merah dan mengecek kematangan tomat
def detect_tomato_ripeness(image_path):
    # Baca gambar
    image = cv2.imread(image_path)
    image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)

    # Konversi ke HSV
    hsv = cv2.cvtColor(image, cv2.COLOR_BGR2HSV)

    # Rentang warna merah dalam HSV
    lower_red1 = np.array([0, 50, 50])
    upper_red1 = np.array([10, 255, 255])
    lower_red2 = np.array([170, 50, 50])
    upper_red2 = np.array([180, 255, 255])

    # Masker untuk warna merah
    mask1 = cv2.inRange(hsv, lower_red1, upper_red1)
    mask2 = cv2.inRange(hsv, lower_red2, upper_red2)
    red_mask = mask1 + mask2

    # Hitung total pixel warna merah
    red_pixels = np.sum(red_mask > 0)
    total_pixels = image.shape[0] * image.shape[1]
    red_percentage = (red_pixels / total_pixels) * 100

    # Kriteria kematangan (misal: lebih dari 50% merah dianggap matang)
    ripeness_status = "Matang" if red_percentage > 50 else "Belum Matang"

    # Tampilkan hasil
    print(f"Persentase warna merah: {red_percentage:.2f}%")
    print(f"Status tomat: {ripeness_status}")

    # Plot gambar asli dan masker merah
    plt.figure(figsize=(12, 6))
    plt.subplot(1, 2, 1)
    plt.imshow(image_rgb)
    plt.title("Gambar Asli")
    plt.axis("off")

    plt.subplot(1, 2, 2)
    plt.imshow(red_mask, cmap="gray")
    plt.title("Masker Warna Merah")
    plt.axis("off")

    plt.show()

# Upload gambar dan cek kematangan
image_path = upload_image()
detect_tomato_ripeness(image_path)
```
Hasil Output: 

![tomat](https://github.com/user-attachments/assets/2303d876-6b04-4b35-a26c-b271a6ee37db)
```
Persentase warna merah: 30.43%
Status tomat: Belum Matang
```
Berikut adalah penjelasan singkat tentang cara kerja kode:

1. Upload Gambar: ```Bagian upload_image()``` memungkinkan pengguna untuk mengunggah gambar tomat.<br>
2. Deteksi Warna Merah: Program menggunakan ruang warna HSV untuk mendeteksi warna merah pada gambar.<br>
4. Hitung Dominasi Merah: Persentase warna merah dihitung berdasarkan jumlah piksel yang sesuai dengan masker merah.<br>
5. Cek Kematangan: Jika persentase warna merah lebih dari 50%, tomat dianggap matang.<br>
6. Visualisasi: Menampilkan gambar asli dan hasil deteksi warna merah.<br>

Anda dapat menjalankan kode ini di Google Colab. Setelah mengunggah gambar tomat, program akan memberikan hasil analisis secara otomatis.
