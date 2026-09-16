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
├── README.md
├── requirements.txt
└── visual_report.py
```

## Setup

```bash
git clone https://github.com/USERNAME/environmental-issue-monitoring.git
cd environmental-issue-monitoring
pip install -r requirements.txt
```

### Catatan penting

Script ini bergantung pada library internal `great` (klasifikasi isu, resolver lokasi, normalisasi slang) milik institusi tempat project ini dikembangkan. Library tersebut **privat, tidak disertakan di repo ini**. Untuk menjalankan pipeline secara utuh, kamu perlu:

1. Implementasi sendiri fungsi setara: `classify_issue(text)`, `resolve_frame(df, location_col, text_cols)`, `normalize_slang(text)`, plus dictionary `PROVINCE_FIX`, `GEO_FIX`, `PULAU_MAP`
2. Atau gunakan script ini sebagai referensi arsitektur pipeline (cleaning → klasifikasi → visualisasi)

Fungsi `prepare_data()` juga perlu diisi sesuai kebutuhan (umumnya: hitung `start_date`/`end_date` dari kolom `Date` di dataset).

## Cara Pakai

1. Buka `visual_report.py`, isi variabel `SOURCE` dengan link Google Sheets/Drive (akses "Anyone with the link") atau path file `.xlsx` lokal
2. Pastikan kolom data punya: `No`, `Headline`, `Mentions`, `Date`, `Link`, `Sentiment`, `Author`
3. Jalankan script:
   ```bash
   python visual_report.py
   ```
4. Output: dashboard peta + bar chart (ditampilkan via matplotlib), plus tabel top isu per pulau & media sosial (dicetak ke console)

## Contoh Output

<img width="2965" height="1297" alt="image" src="https://github.com/user-attachments/assets/3093eb5a-aa76-433b-a90b-b6bb3b0892c4" />


## Latar Belakang

Dibangun sebagai bagian dari kerja monitoring media untuk isu lingkungan di Indonesia — mengolah ratusan hingga ribuan mention berita/media sosial per periode menjadi ringkasan visual yang mudah dibaca untuk kebutuhan riset dan pelaporan.
