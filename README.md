# Histogram

Kali ini saya akan mencoba menggunakan Histogram Equalization dengan menggunakan bahas python
Untuk IDE nya disini saya menggunakan Google Colab untuk memudahkan pengerjaan


# Algoritma
berikut adalah algoritma yang saya gunakan
```
'Histogram Equalization
For i = 0 To Picture1.ScaleWidth - 1
    For j = 0 To Picture1.ScaleHeight - 1
        w = Picture1.Point(i, j)
        r = w And RGB(255, 0, 0)
        g = Int((w And RGB(0, 255, 0)) / 256)
        b = Int((Int((w And RGB(0, 0, 255)) / 256) / 256))
        xg = Int((r + g + b) / 3)
        yg = Int(256 * c(xg) / 128 / 128)
        h2(yg) = h2(yg) + 1
        Picture2.PSet (i, j), RGB(yg, yg, yg)
    Next j
Next i

For i = 0 To 255
    MSChart1.Row = i + 1
    MSChart1.Data = h(i)
    MSChart1.RowLabel = Trim(Str(i))
    MSChart2.Row = i + 1
    MSChart2.Data = h2(i)
    MSChart2.RowLabel = Trim(Str(i))
Next i
```

# Program
dan berikut adalah program yang saya gunakan
```
  uploaded = files.upload()

import cv2
import numpy as np
import matplotlib.pyplot as plt

# Membaca gambar dari file yang diunggah
image = cv2.imread(next(iter(uploaded.keys())), cv2.IMREAD_GRAYSCALE)

# Mendapatkan ukuran gambar
height, width = image.shape

# Membuat histogram
hist = np.zeros(256)
for i in range(height):
    for j in range(width):
        pixel_value = image[i, j]
        hist[pixel_value] += 1

# Normalisasi histogram
hist = hist / (height * width)

# Histogram Cumulative Distribution Function (CDF)
cdf = np.zeros(256)
cdf[0] = hist[0]
for i in range(1, 256):
    cdf[i] = cdf[i - 1] + hist[i]

# Mapping untuk histogram equalization
equalized_image = np.zeros_like(image)
for i in range(height):
    for j in range(width):
        pixel_value = image[i, j]
        equalized_image[i, j] = int(cdf[pixel_value] * 255)

# Menampilkan hasil
plt.figure(figsize=(12, 6))
plt.subplot(1, 2, 1)
plt.title("Original Image")
plt.imshow(image, cmap='gray')
plt.subplot(1, 2, 2)
plt.title("Equalized Image")
plt.imshow(equalized_image, cmap='gray')
plt.show()

```

# Output
Untuk hasilnya berikut adalah foto yang saya gunakan
![Gambar WhatsApp 2024-11-15 pukul 22 52 41_9633d3a7](https://github.com/user-attachments/assets/cb656e17-5a80-4828-a1f7-3ff30a1dc19b)

dan untuk hasilnya setelah dimasukkan ke program adalah sebagai berikut

![image](https://github.com/user-attachments/assets/1cdbf10a-62c0-4220-8189-29243023db07)
