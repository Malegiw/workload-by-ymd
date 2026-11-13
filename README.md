# Workload by YMD

Aplikasi web untuk menganalisis beban kerja tim engineering per disiplin (Lead Project, Process, Mechanical, Piping, Civil/Structure, Electrical, Instrument, DocCon) di fase pekerjaan Inisiasi, Pre-FEED, FEED, dan DED.

Aplikasinya hanya satu file `index.html`, jadi tidak perlu proses build. Cukup buka file itu di browser, atau hosting lewat GitHub Pages.

## Rumus

```
Beban     = Bobot fase × Faktor peran × Faktor kompleksitas × Alokasi × (1 − Progres)
Utilisasi = Σ Beban ÷ Kapasitas personel
```

Bobot fase default: DED 1,00 · FEED 0,70 · Pre-FEED 0,40 · Inisiasi 0,20. Semua bobot bisa diubah di halaman **Pengaturan**.

Status utilisasi: di bawah 70% **Tersedia**, 70–100% **Optimal**, di atas 100% **Overload**.

## Halaman

| Halaman | Isi |
|---|---|
| Dashboard | KPI, proyek per fase, utilisasi per disiplin, kapasitas tim, proyek dengan beban tertinggi, heatmap 12 minggu |
| Proyek | Daftar proyek, ganti fase langsung dari tabel, panel detail tim |
| Personel | Kartu utilisasi per orang, bisa difilter per disiplin |
| Penugasan | Form penugasan dengan pratinjau utilisasi dan peringatan overload |
| Analisis disiplin | Beban per fase, komposisi beban, tren bulanan, struktur Disiplin → Personel → Proyek |
| Pengaturan | Bobot dan faktor, ekspor/impor Excel, reset ke data contoh |

## Data dan sinkronisasi antar perangkat

- Saat pertama dibuka, aplikasi berisi **data contoh**.
- Tanpa sinkronisasi, perubahan hanya tersimpan di browser perangkat itu.
- Dengan **Sinkronisasi GitHub** (Pengaturan), data disimpan sebagai `data.json` di sebuah repo **Private** terpisah, jadi HP, iPad, dan laptop memakai data yang sama.
  - Perubahan dikirim otomatis 2,5 detik setelah Anda berhenti mengedit, dan setiap pengiriman menjadi satu commit (riwayat perubahan ikut tersimpan).
  - Perangkat lain memeriksa pembaruan tiap 30 detik dan saat aplikasi dibuka kembali.
  - Jika dua perangkat mengubah data bersamaan, aplikasi meminta Anda memilih versi mana yang dipakai. Tidak ada data yang tertimpa diam-diam.
  - Jika offline, perubahan tetap di perangkat dan dikirim saat online.
- Token GitHub hanya disimpan di browser tiap perangkat. Jangan membagikannya.
- Impor Excel: unduh `Template-Workload.xlsx` (Pengaturan → Unduh template Excel), isi sheet `Proyek`, `Personel`, `Penugasan`, lalu impor lewat tombol Impor Excel. Ada pratinjau sebelum data berubah, mode Gabung atau Ganti semua, dan daftar baris bermasalah. Hasil ekspor memakai format yang sama sehingga bisa diedit di Excel lalu diimpor kembali. `Bobot Fase`, `Faktor Peran`, `Kompleksitas` bersifat opsional.

## Menjalankan di komputer

Klik dua kali `index.html`, atau jalankan server lokal:

```bash
python -m http.server 8000
# lalu buka http://localhost:8000
```

## Komponen pihak ketiga

Logo (Particles), Context meter, Card swap, dan Upload dropzone diadaptasi dari [Bencho](https://bencho.dev) (lisensi MIT). Detailnya ada di `THIRD_PARTY_NOTICES.md`. Template, ekspor, dan impor Excel memakai [ExcelJS](https://github.com/exceljs/exceljs) (MIT) dari CDN.
