# Kuis Pintar

Aplikasi latihan pengetahuan umum dengan tutor AI.
Proyek Besar Praktikum Algoritma dan Struktur Data, Kelompok KOCAK,
Fakultas Teknologi Informasi, Universitas Kristen Duta Wacana.

| Anggota | NIM |
|---|---|
| Brillyan Herlambang Anugerah Seleng | 71251202 |
| Raffiel Gideon Nyolo Nyolo | 71251214 |
| Elgin Brav Ekazatia | 71251234 |

## Tentang aplikasi

Latihan pengetahuan umum sering tidak terarah: soal tidak dijelaskan, bidang yang lemah
tidak ketahuan, dan bank soal gratis berbahasa Inggris. Kuis Pintar membantu pengguna:

- memilih kategori, tingkat kesulitan, dan jumlah soal, lalu mengerjakan soal satu per satu;
- melihat akurasi per kategori dan progres antar-sesi dalam grafik;
- mendapat terjemahan soal, penjelasan jawaban yang salah, dan rencana latihan dari Gemini;
- mengunduh laporan (Excel/JSON) dan mengunggah riwayat JSON untuk melanjutkan progres.

> Status: dalam pengerjaan. Fitur ditambahkan bertahap sesuai jadwal tim.

## Sumber data

Soal diambil dari [Open Trivia Database](https://opentdb.com/api_config.php)
(gratis, tanpa API key, lisensi CC BY-SA 4.0). Soal berbahasa Inggris.

| Endpoint | Dipakai untuk |
|---|---|
| `GET /api_category.php` | Daftar 24 kategori soal |
| `GET /api_count.php?category={id}` | Jumlah soal tersedia per kategori dan kesulitan |
| `GET /api_token.php?command=request` | Token sesi agar soal tidak berulang |
| `GET /api.php?amount=..&category=..&difficulty=..&type=..&token=..` | Mengambil soal (maksimal 50 per permintaan) |

Batas pemakaian: satu permintaan per 5 detik per alamat IP.

## Teknologi

Python, Streamlit, Pandas, Requests, Altair, OpenPyXL, Google GenAI SDK (Gemini), Pytest.

## Struktur data dan algoritma

| Kebutuhan | Struktur data / algoritma |
|---|---|
| Menyimpan soal dari API | List dan dictionary |
| Menyajikan soal satu per satu | Queue (`collections.deque`) |
| Mencegah soal berulang | Set |
| Cache API dan jawaban AI | Dictionary (hash table) |
| Riwayat sesi (undo/redo) | Stack |
| Statistik per kategori | Counter |
| Mengacak pilihan jawaban | Fisher-Yates shuffle |
| Peringkat kategori dan sesi | Merge sort |
| Mencari soal di riwayat | Linear search |

## Cara menjalankan

```
git clone https://github.com/elginbrav123170/kuis-pintar.git
cd kuis-pintar
python -m venv .venv
.venv\Scripts\activate        # Windows
source .venv/bin/activate     # Mac/Linux
pip install -r requirements.txt
streamlit run app.py
```

API key Gemini: salin `.streamlit/secrets.toml.example` menjadi `.streamlit/secrets.toml`,
lalu isi key-nya. File `secrets.toml` tidak ikut di-commit.

Menjalankan tes:

```
pytest
```

## Pembagian file

| File | Pemilik |
|---|---|
| `app.py`, `data.py`, `ui_kuis.py` | Brilly |
| `cache.py`, `antrean.py`, `history.py`, `statistik.py`, `sorting.py`, `search.py`, `tests/` | Raffiel |
| `charts.py`, `export.py`, `ai_tutor.py`, `ui_hasil.py`, `ui_tutor.py`, `ui_ekspor.py`, `data_contoh.py` | Elgin |

## Alur kerja Git

Tidak ada yang push langsung ke `main`. Setiap fitur dikerjakan di branch
`nama/fitur` (misalnya `raffiel/antrean-soal`), lalu digabung lewat pull request
yang di-review minimal satu anggota lain.
