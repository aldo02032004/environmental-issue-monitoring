# Environmental Issue Monitoring — Visualization Pipeline

Pipeline Python untuk memantau isu lingkungan di Indonesia dari data media (berita + media sosial). Mengubah data mentah hasil monitoring jadi klasifikasi isu, deteksi lokasi, dan dashboard visual (peta choropleth + bar chart).

## Fitur

- **Ingest fleksibel**: baca data dari Google Sheets, Google Drive, atau file `.xlsx` lokal
- **Cleaning teks**: hapus boilerplate berita, URL, hashtag, mention; deduplikasi konten yang di-syndicate ulang
- **Klasifikasi isu**: kategorisasi otomatis isu lingkungan dari teks
- **Deteksi lokasi**: ekstraksi provinsi & pulau dari teks bebas, termasuk distribusi proporsional untuk lokasi ambigu (cuma nama pulau disebut, provinsi tidak spesifik)
- **Dashboard visual**: peta choropleth Indonesia + bar chart distribusi nasional & per pulau
- **Tabel ringkasan**: top isu per pulau (berita) dan top isu media sosial, lengkap dengan link sumber

## Tech Stack

| Kategori | Tools |
|---|---|
| Data processing | pandas, geopandas |
| Visualisasi | matplotlib |
| HTTP/ingest | requests |
| Progress tracking | tqdm |

## Struktur Project

```
environmental-issue-monitoring/
├── environmental-issue-monitoring.ipynb   # seluruh pipeline, 7 cell
├── requirements.txt
└── README.md
```

## Cara Pakai (Google Colab)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/aldo02032004/environmental-issue-monitoring/blob/main/environmental-issue-monitoring.ipynb)

1. Buka notebook lewat tombol di atas.
2. Di **CELL 2**, isi variabel `SOURCE` dengan link Google Sheets/Drive (akses *Anyone with the link*) atau path file `.xlsx`.
3. Pastikan data punya kolom: `No`, `Headline`, `Mentions`, `Date`, `Link`, `Sentiment`, `Author`.
4. `Runtime → Run all`. Hasilnya dashboard peta + bar chart, tabel top isu per pulau & media sosial, dan laporan kata yang belum tercakup klasifikasi.

Tidak perlu token atau API key. Klasifikasi isu, resolver lokasi (`resolve_frame`), dan normalisasi slang berasal dari library [GREAT-Tools](https://github.com/azmkto/GREAT-Tools) yang publik dan di-install otomatis di CELL 1.

Untuk dijalankan di luar Colab: `pip install -r requirements.txt`, lalu buka notebook di Jupyter.

## Contoh Output

<img width="2965" height="1297" alt="image" src="https://github.com/user-attachments/assets/3093eb5a-aa76-433b-a90b-b6bb3b0892c4" />


## Latar Belakang

Dibangun sebagai bagian dari kerja monitoring media untuk isu lingkungan di Indonesia — mengolah ratusan hingga ribuan mention berita/media sosial per periode menjadi ringkasan visual yang mudah dibaca untuk kebutuhan riset dan pelaporan.
