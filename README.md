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

## Data

- Saat pertama dibuka, aplikasi berisi **data contoh**.
- Di GitHub Pages, perubahan disimpan di browser masing-masing pengguna (localStorage).
- Untuk memindahkan atau membagikan data, gunakan **Ekspor Excel**. Impor menerima format yang sama: sheet `Proyek`, `Personel`, dan `Penugasan`, dengan sheet `Bobot Fase` dan `Faktor Peran` sebagai opsi.

## Menjalankan di komputer

Klik dua kali `index.html`, atau jalankan server lokal:

```bash
python -m http.server 8000
# lalu buka http://localhost:8000
```

## Komponen pihak ketiga

Logo (Particles), Context meter, Card swap, dan Upload dropzone diadaptasi dari [Bencho](https://bencho.dev) (lisensi MIT). Detailnya ada di `THIRD_PARTY_NOTICES.md`. Pembacaan Excel memakai [SheetJS](https://sheetjs.com) dari CDN.
