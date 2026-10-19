# Visual Sudoku Solving Using Constraint Satisfaction Problem (CSP)

## Tentang Program

Program ini menyelesaikan Sudoku dari gambar. CNN (LeNet atau ResNet18) membaca 81 sel dan menghasilkan probabilitas angka di tiap sel. Setelah itu, solver Constraint Programming (CPMpy + OR-Tools CP-SAT) memilih bacaan yang paling mungkin dan tetap memenuhi aturan Sudoku (*joint inference*). Dengan cara ini, salah baca CNN dan isian tulisan tangan yang salah bisa dikoreksi.

Isi notebook `csp_visual_sudoku.ipynb`:

1. Setup dan load data (OpenSky, MNIST Visual Sudoku, Sudoku Assistant)
2. Preprocessing
3. Training CNN
4. Kalibrasi probabilitas
5. Model CP dan solver (Baseline, Hybrid, Higher-order, Style-aware, Wildcard)
6. Eksperimen tiga skenario
7. Demo web Gradio: upload foto Sudoku (kotak dideteksi otomatis dengan OpenCV), lalu program menampilkan solusi dan posisi sel yang salah (baris dan kolom)

## Referensi

Mulamba, M., Mandi, J., Mahmutoğulları, A. İ., & Guns, T. (2024). Perception-based constraint solving for sudoku images. *Constraints*, 29, 112–151. https://doi.org/10.1007/s10601-024-09372-9

Dataset: KU Leuven RDR, https://doi.org/10.48804/3SUHHR

## Cara Menjalankan

### Lokal

Butuh Python 3.12.

```bash
uv venv --python 3.12
source .venv/bin/activate
uv pip install torch torchvision cpmpy ortools numpy pandas matplotlib gradio opencv-python-headless certifi ipykernel
```

Buka `csp_visual_sudoku.ipynb` di VS Code atau Jupyter, pilih kernel `.venv`, lalu jalankan semua sel (Run All).

- Dataset diunduh otomatis ke `data/` saat pertama kali dijalankan (sekitar 700 MB).
- `TRAIN = False` (default) memakai bobot yang sudah ada di `weights/`. Ubah ke `True` untuk melatih CNN dari awal.
- Sel terakhir membuka demo web di `http://127.0.0.1:7860`.

### Google Colab

1. Upload notebook ke Colab dan pilih runtime GPU.
2. Upload folder `weights/` ke `/content/weights` (atau pakai Google Drive, lihat komentar di sel Konfigurasi).
3. Jalankan semua sel. Dependensi terpasang otomatis, dan demo web mendapat link publik `*.gradio.live`.
