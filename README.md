# Pertemuan 13 Debugging dan Testing Python

## Identitas

Nama: Ismaya Catur Dewi Azzahra
NIM: 2225250018
Kelas: 3A

## Tujuan

Tujuan dari tugas ini adalah mempelajari cara menemukan dan memperbaiki bug pada program Python menggunakan tracing, debugger VS Code, dan test case, serta membuktikan bahwa perbaikan berhasil melalui pengujian ulang.

## Cara Menjalankan Program

Program dijalankan melalui VS Code menggunakan Python.

Langkah-langkah:

1. Buka folder `pertemuan-13-debugging-2225250018` di VS Code.
2. Buka terminal dan pastikan posisi terminal berada di folder utama proyek.
3. Jalankan program dan test case dengan perintah berikut.

```bash
python3 praktik/praktik_4_debugging.py
python3 praktik/test_praktik_4.py
```

4. Bandingkan hasil aktual dengan hasil yang diharapkan.

## Algoritma Debugging Praktik 4

1. Jalankan program awal tanpa mengubah kode dan catat output aktual.
2. Susun test case untuk setiap fungsi, termasuk nilai batas dan list kosong.
3. Jalankan test case dan catat test yang FAIL.
4. Lakukan tracing atau gunakan breakpoint untuk mencari letak kesalahan.
5. Tentukan akar penyebab setiap bug.
6. Perbaiki kode dengan perubahan sesedikit mungkin.
7. Jalankan ulang seluruh test case.
8. Catat hasil retest dan pastikan tidak ada regresi.

## Pengujian Awal

| Test Case | Target | Input | Hasil yang Diharapkan | Hasil Aktual | Status |
| --- | --- | --- | --- | --- | --- |
| T1 | rata-rata | `[80, 60, 90, 70]` | 75.0 | 60.0 | FAIL |
| T2 | rata-rata | `[100, 80]` | 90.0 | 36.0 | FAIL |
| T3 | status | `60` | Lulus | Tidak lulus | FAIL |
| T4 | status | `59` | Tidak lulus | Tidak lulus | PASS |
| T5 | tertinggi | `[80, 60, 90, 70]` | 90 | 0 | FAIL |
| T6 | tertinggi | `[]` | `None` | 0 | FAIL |

## Bug Report

| Bug | Test Case | Lokasi | Akar Penyebab | Perbaikan |
| --- | --- | --- | --- | --- |
| B01 | T1, T2 | `hitung_rata_rata` | Pembagi ditulis tetap 5, tidak sesuai jumlah data | Memakai `len(nilai)` dan menangani list kosong |
| B02 | T3 | `status` | Operator `>` tidak memasukkan nilai 60 | Mengganti menjadi `>=` |
| B03 | T5, T6 | `nilai_tertinggi` | Operator terbalik (`<`) dan nilai awal 0 | Nilai awal `nilai[0]`, operator `>`, dan `None` untuk list kosong |

## Pengujian Ulang

| Test Case | Hasil yang Diharapkan | Hasil Aktual | Status |
| --- | --- | --- | --- |
| T1 | 75.0 | 75.0 | PASS |
| T2 | 90.0 | 90.0 | PASS |
| T3 | Lulus | Lulus | PASS |
| T4 | Tidak lulus | Tidak lulus | PASS |
| T5 | 90 | 90 | PASS |
| T6 | `None` | `None` | PASS |

Semua test case berstatus PASS dan T4 yang sebelumnya benar tetap PASS, sehingga tidak ada regresi.

## Riwayat Commit

| Commit | Keterangan |
| --- | --- |
| `chore: menambahkan kasus debugging awal` | Kode awal yang masih bermasalah |
| `test: menambahkan test case dan bug report` | Test case dan bug report |
| `fix: memperbaiki bug rata-rata status dan nilai tertinggi` | Perbaikan B01, B02, dan B03 |
| `docs: menambahkan hasil retest dan refleksi` | Hasil retest dan refleksi |

## Refleksi

Teknik debugging yang paling membantu adalah membuat test case nilai batas, karena bug `nilai > 60` tidak menimbulkan error tetapi membuat nilai 60 salah dinyatakan tidak lulus. Selain itu, perbaikan harus diikuti pengujian ulang seluruh test case agar tidak ada bagian lain yang rusak.