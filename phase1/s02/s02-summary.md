# Fullstack Revenge Program — Course Tracker

Personal 21-week program modeled on the RevoU Full Stack SE syllabus (4 phases, 84 live sessions).
Mentor role: recruiter + senior fullstack engineer. Language: Indonesian, technical terms in English.

## Schedule
- Mon–Thu 19.00–21.00 WIB live class (S01 = Mon 21 Sep 2026) · Fri assignment day · Sat 13.00–15.30 review + HackerRank + Career+ task
- Student starts each class with "Mulai Sxx" (may start earlier when free). Student will report manually how many sessions are done; do not reschedule on my own.

## Phases
| Phase | Sessions | Dates | Gate |
|---|---|---|---|
| 1 Algorithm & Programming (Python) | S01–S12 | 21 Sep – 8 Oct 2026 | HackerRank Problem Solving (Basic) + Job Insight CLI mini project |
| 2 Backend (Flask, PostgreSQL, pytest, Locust, Docker, AWS) | S13–S40 | 12 Oct – 26 Nov 2026 | Python/SQL (Basic) certs + ApplyTrack backend live |
| 3 Frontend (Next.js, TS, Tailwind, Playwright) | S41–S68 | 30 Nov 2026 – 14 Jan 2027 | JS/React (Basic) certs + Project #1 live |
| 4 AI-Driven (Kiro spec mode, steering, analytics/S3/email/AI) | S69–S84 | 18 Jan – 11 Feb 2027 | Problem Solving (Intermediate) + Project #2 live |

## Projects
- Project #1 ApplyTrack: internship/job application tracker (Flask + Postgres + Next.js)
- Project #2 ApplyTrack AI: analytics, S3 CV upload, email reminders, CV↔JD matcher, built via spec-driven AI workflow

## Deliverables so far (in fullstack-study/course/ on Aca's computer)
- 00_Master_Plan_Fullstack_Revenge.docx: recruiter brief, rules, 84-session calendar, HackerRank gates, Career+ track, rubric
- 01_Phase1_Materi_Algorithm_Programming.docx: full materials S01–S12
- 02_Phase1_Assignments_HackerRank.docx: W1–W3 assignments, mini project, Gate 1
- jobs.csv: synthetic dataset (90 rows, 3 deliberately broken rows)

## Student setup
- Repo: https://github.com/Acask8rawK/fullstack-revenge (local: Documents/fullstack-study/fullstack-revenge)
- Windows, Git Bash + PowerShell, Python 3.11.9, Git 2.52, VS Code 1.138; diagrams in draw.io/Miro

---

# Progress Log
Legend: ✅ correct · ◐ partially correct · ❌ wrong · ❓ "tidak tahu" / no answer

## S01 — Cara Program Berpikir + Arsitektur Web App
Done Mon 21 Sep 2026 (morning, ahead of the 19.00 slot).

### A. Warm-up diagnostic (score 3.5/5)

**Q1. Apa itu algoritma? (kata-kata sendiri)** ◐
- Jawaban Aca: "Algoritma adalah sebuah langkah atau bisa dikatakan resep untuk seorang programmer agar bisa membuat suatu aplikasi / membuat sebuah solusi dari suatu masalah."
- Koreksi: Algoritma tidak khusus untuk programmer (resep masak, prosedur ATM juga algoritma). Yang kurang: 4 ciri algoritma yang baik: (1) input jelas, (2) setiap langkah tidak ambigu, (3) pasti berhenti/finite, (4) output benar untuk semua input valid.

**Q2. Apa yang terjadi saat buka https://tokopedia.com lalu Enter?** ◐
- Jawaban Aca: DNS lookup (domain → IP) → koneksi ke server + HTTPS handshake terenkripsi → HTTP request method GET → server routing ke fungsi, validasi, ambil data, susun response → HTTP response dengan status code 2xx/4xx/5xx → browser render (HTML parsing, CSS, JavaScript) dan menampilkan website.
- Koreksi: Urutan benar, tapi hampir kata per kata sama dengan materi (hafalan). Diuji lebih dalam lewat pertanyaan pendalaman (lihat bagian C). Interview menuntut penjelasan, bukan hafalan.

**Q3. Beda Git dan GitHub?** ✅
- Jawaban Aca: "Git adalah version control system / alat untuk menyimpan snapshot project, sedangkan GitHub adalah platform untuk menyimpan repository suatu project melalui git."
- Tambahan: Git bekerja lokal & offline; GitHub hanyalah salah satu remote (ada juga GitLab, Bitbucket).

**Q4. Arti 404 dan 500, siapa yang salah?** ◐
- Jawaban Aca: "404 berarti sistem tidak ditemukan...? kalau 500 artinya internal server error (masalah di server)"
- Koreksi: 500 ✅. 404 = resource not found: server-nya jalan, tapi yang diminta tidak ada (URL salah / data dihapus). Aturan: 4xx = kesalahan client, 5xx = kesalahan server.

**Q5. "Masak nasi sampai matang, lalu sajikan secukupnya": algoritma baik atau buruk?** ✅
- Jawaban Aca: "Buruk. Nasi matang itu tahu dari mana? Masak berapa lama? Secukupnya itu sebenarnya sebanyak apa?"
- Koreksi: Sempurna. Menemukan pelanggaran ciri "tidak ambigu" dan "pasti berhenti".

### B. Latihan A — Tulis ulang resep nasi sebagai algoritma (6/10)
- Jawaban Aca: INPUT: Beras · OUTPUT: Nasi yang matang · LANGKAH: 1) Masukkan 3 cup nasi ke rice cooker, 2) Tuangkan air 3 gelas, 3) Masak nasi selama 10 menit hingga matang, 4) Sajikan nasi yang sudah matang 5 sendok makan di piring.
- Koreksi (4 bug):
  1. State salah: "3 cup **nasi**": yang dimasukkan masih **beras** (setara salah menamai variabel).
  2. Masih ambigu: "10 menit **hingga matang**": kalau 10 menit belum matang, lalu apa?
  3. Asumsi salah: rice cooker butuh ±25–35 menit, bukan 10.
  4. Input tidak lengkap: air, rice cooker, listrik juga input.
- Versi benar: kondisi berhenti berbasis sensor, yaitu pola `while`: "SELAMA indikator masih COOK: tunggu; setelah pindah ke WARM, diamkan 10 menit".

### C. Latihan B — Pertanyaan pendalaman interview

**B1. Sebelum tanya DNS server, browser cari IP di mana dulu?** ❓
- Jawaban Aca: "tidak tahu"
- Jawaban: browser cache → OS cache + file hosts (C:\Windows\System32\drivers\etc\hosts) → router → DNS resolver (ISP / 8.8.8.8 / 1.1.1.1) → jika belum tahu, resolver bertanya berantai: root server → TLD (.com) → authoritative nameserver. Jawaban disimpan selama TTL (penyebab "DNS propagation").

**B2. Saat HTTPS handshake, apa yang dikirim server supaya browser yakin itu tokopedia asli?** ❌/❓
- Jawaban Aca: "sebuah term namanya ack tapi saya kurang paham"
- Koreksi: ACK milik **TCP handshake** (SYN → SYN-ACK → ACK), yang terjadi sebelum TLS. Jawaban yang benar: server mengirim **sertifikat (certificate)** berisi nama domain + public key + tanda tangan digital CA (Certificate Authority). Browser memverifikasi tanda tangan CA, kecocokan domain, dan masa berlaku → sepakati session key → semua data dienkripsi.

**B3. Buka tokopedia.com = berapa request? Satu atau banyak?** ❓
- Jawaban Aca: "kurang paham"
- Jawaban: banyak. HTML dulu → browser menemukan CSS/JS/gambar/font (request masing-masing) → JS memanggil API (fetch/XHR) untuk data produk dalam JSON.
- Praktik DevTools: Aca mengukur **191 request**. Hal yang mengejutkan menurut Aca: "ada banyak sekali request 150+". Penjelasan: gambar, JS chunks, API, tracking/analytics, CSS/font. Banyak request ≠ lambat berkat HTTP/2 (multiplexing), cache, lazy loading.
- Data API Tokopedia (URL/method/status + alasan GraphQL pakai POST): **dilewati**, belum dijawab. Pertanyaan pemantik yang masih terbuka: "Kenapa request ambil data bisa pakai POST?" (jawaban: GraphQL mengirim query di body request).

### D. Cek pemahaman — Konsep 2 (Three-tier)

**D1. Tombol "Beli" abu-abu (disabled) saat stok habis, apakah cukup mencegah pembelian?** ❌
- Jawaban Aca: "Cukup, karena dengan mengubah warna label mengindikasikan stok habis dan barang tidak bisa dibeli / tidak bisa di klik. Lebih detail: di database terdeteksi produk X tidak ada, lalu server mengirim response ke client bahwa stok habis, baru browser menampilkan label abu-abu dan tidak bisa diklik."
- Koreksi: TIDAK cukup. Tombol disabled = UX, bukan keamanan. Bisa ditembus dengan: (1) Inspect Element, hapus atribut `disabled`; (2) memanggil API langsung via Postman/curl; (3) race condition (2 pembeli, stok 1, klik bersamaan). Server wajib mengecek ulang stok saat request pembelian masuk, dalam satu transaksi atomik (dibahas di S24).
- Aturan emas: validasi client = UX, validasi server = keamanan. Selalu keduanya.

**D2. Di tier mana password dicek?** ◐ (menjawab "kenapa", bukan "di mana")
- Jawaban Aca: "Password harus dicek pertama kali untuk menandakan apakah user ini valid, cek authorization dll. Kenapa bukan di tier lain? Karena kalau password tidak dicek di awal akan merusak reputasi aplikasi... orang tidak berwenang bisa menggunakan akun siapa saja, duit siapa saja dan mengeksploitasi."
- Koreksi: Jawaban = **Server/API (Flask)**. Client: kode bisa dimodifikasi (`if (true) login()`). Database: hanya menyimpan hash, dan client tidak boleh konek langsung ke DB. Server: satu-satunya tempat yang dikontrol penuh (ambil hash, bandingkan dengan bcrypt/argon2, rate limit, keluarkan token).
- Koreksi istilah: password = **Authentication** ("kamu siapa?" → 401), bukan Authorization ("kamu boleh apa?" → 403).

### E. Lab — Diagram arsitektur/sequence
- v1 (`phase1/s01/architecture.png`) — 2/4: berupa daftar 7 langkah linear, bukan diagram arsitektur. Masalah: tidak ada komponen (Browser/DNS/Flask/PostgreSQL), panah tanpa arah antar-komponen, label tidak spesifik, jalur error tidak ada, "DNS lookup dari halaman lowongan" keliru (DNS menerjemahkan domain, bukan halaman/path).
  - Bug konsep di step 6 Aca: "404 jika data lowongan tidak ditemukan" → salah untuk pencarian. Hasil pencarian kosong = `200 OK` + `[]`. Tabel: `GET /jobs?city=bandung` kosong → 200 []; `GET /jobs/999` tidak ada → 404; parameter invalid → 400; DB mati → 500/503.
- v2 (`phase1/SequenceDiagram-ApplyTrack.drawio.png`, kini dipindah ke `phase1/s01/`) — konten 3/4, tapi **export PNG rusak** (panah & teks tidak terlihat: warna default di tema gelap + background transparan). Konten diekstrak dari XML yang tertanam di PNG.
  - Bagus: User actor terpisah, happy path + error path, pesan error ramah & tidak bocor detail teknis, query SQL spesifik.
  - Perbaikan: tambah lifeline DNS; tulis `GET /jobs?city=jakarta`; pecah step 6 jadi self-arrow validasi + panah SQL ke PostgreSQL; routing ke **fungsi/handler** bukan "file"; server **mengembalikan** 500 + JSON, browser yang **menampilkan**; error path harus menunjukkan **penyebab** (DB mati / connection refused), bukan "cari Aceh → 500" (kota tanpa lowongan = 200 []).
  - **Status: file sudah dipindah ke phase1/s01/, tapi PNG masih versi lama (export rusak) dan konten belum diperbaiki; .drawio belum di-commit.**

### F. Exit ticket

**F1. Beda client, server, database (≤5 kalimat) + kenapa validasi di server** — 3/4 ✅
- Jawaban Aca: "Client adalah komponen website yang bertugas menangkap interaksi user langsung dan membuat request atau menangkap response dari server, lalu server adalah komponen website yang tugasnya menghandle request dari client dan melakukan proses di balik layar seperti pencarian fungsi, komunikasi dengan database dan validasi (validasi berada di server karena fungsi-fungsi validasi harus bekerja di balik layar supaya user tidak bisa mengubah/mengutak-atik JSON contohnya dari client langsung), sedangkan database adalah komponen yang bertugas menyimpan, mengolah, dan me-maintain data milik website tersebut."
- Koreksi: Alasan validasi di server bukan "di balik layar", tapi karena server satu-satunya tempat yang dikontrol penuh; kode client bisa dibaca/diubah/dilewati. Client bukan hanya website (mobile app, script, Postman juga client). Validasi client tetap berguna untuk UX.

**F2. Arti status code 200, 301, 400, 401, 403, 404, 500** — 2/4 ◐
| Code | Jawaban Aca | Status | Jawaban benar |
|---|---|---|---|
| 200 | "berhasil (ok)" | ✅ | OK |
| 301 | "saya lupa" | ❓ | Moved Permanently: resource pindah permanen ke URL baru (mis. http → https) |
| 400 | "error di sisi client" | ◐ | Bad Request: input/format request tidak valid (itu arti keluarga 4xx secara umum) |
| 401 | (tidak dijawab) | ❓ | Unauthorized: belum login / token tidak valid ("kamu siapa?") |
| 403 | "tidak tahu" | ❓ | Forbidden: sudah login tapi tidak punya izin ("kamu tidak boleh") |
| 404 | "data yang dicari tidak ditemukan oleh sistem" | ✅ | Not Found: resource tidak ada |
| 500 | "internal server error, seperti koneksi DB dengan backend terputus" | ✅ | Internal Server Error |
- Catatan: 401/403 sudah diajarkan ±1 jam sebelumnya (D2) tapi tidak teringat → spaced repetition. Analogi: 401 = satpam minta ID card; 403 = ID valid tapi dilarang masuk ruang direktur.

**F3. `GET /jobs/42`, lowongan ID 42 sudah dihapus → status code & tampilan frontend?** ❌
- Jawaban Aca: "Tetap 200 OK dengan isi JSON yang kosong [], yang sebaiknya ditampilkan di layar user adalah 'Lowongan yang anda cari sudah tidak tersedia'"
- Koreksi: Overgeneralization dari aturan pencarian. `/jobs/42` = single resource → **404 Not Found** (bonus: 410 Gone lebih akurat, tapi 404 lebih umum). `200 []` hanya untuk collection/pencarian kosong. Pesan untuk user ✅ tepat; tambahkan tombol "Lihat lowongan lain".

### G. Git issues yang dialami & pelajarannya
1. `git add readme.md` tidak menambahkan apa-apa: pathspec Git case-sensitive (`README.md`). Pelajaran: selalu `git status` sebelum commit.
2. Warning `LF will be replaced by CRLF`: bukan error; tambahkan `.gitattributes` berisi `* text=auto eol=lf` (sudah dilakukan ✅).
3. `Repository not found` saat push: `git remote add` hanya mencatat alamat, repo harus dibuat dulu di github.com (sudah diperbaiki ✅).
4. Commit message "Chore: init class Repo": conventional commits pakai huruf kecil (`chore: init class repo`). Amend hanya sebelum push.
5. Folder kosong tidak ter-commit: Git melacak file, bukan folder → `.gitkeep` (sudah dilakukan ✅).

### H. Ringkasan skor S01
| Aspek | Hasil |
|---|---|
| Warm-up diagnostic | 3.5/5 |
| Latihan resep | 6/10 |
| Pendalaman interview (B1–B3) | 0/3 (semua "tidak tahu"/keliru; sudah diajarkan) |
| Cek pemahaman (D1–D2) | D1 ❌ · D2 ◐ |
| Lab diagram | 2/4 → 3/4 (pending fix export + DNS + error cause) |
| Exit ticket | F1 3/4 · F2 2/4 · F3 ❌ |

---

## S02 — Problem Decomposition, Flowchart & Pseudocode
Done Tue 22 Sep 2026. Aca read the S02 material beforehand.

### A. Warm-up: Review Bank R1–R6 (score 5.5/6) 📈

**R1. Arti 301 + contoh** ✅
- Jawaban Aca: "301 artinya resource sudah pindah / permanently moved, contoh: memindahkan site secara keseluruhan ke domain yang baru."

**R2. 401 vs 403 + authentication vs authorization** ✅
- Jawaban Aca: "401 itu error di sisi client tepatnya pada masalah authentication seperti belum login / token yang invalid, sedangkan 403 di sisi client juga tapi masalah authorization seperti user login tapi tidak punya izin untuk melakukan suatu interaksi / tidak punya izin mengakses suatu fitur."

**R3. 400 vs keluarga 4xx** ✅
- Jawaban Aca: "400 artinya dari sisi client terdapat error yaitu bad request seperti input / format tidak valid, 4xx itu secara umum error pada sisi client."

**R4. (a) `GET /jobs?city=papua` kosong, (b) `GET /jobs/77` tidak ada** ✅
- Jawaban Aca: "a = 200 OK tapi JSON kosong []. b = 404 (data tidak ditemukan oleh sistem), bisa 410 (gone)."

**R5. 3 cara menembus tombol disabled + solusi server** ◐
- Jawaban Aca: "1) mengubah tombol disabled menjadi bisa diklik melalui devtools. 2) bypass API melalui Postman. Solusinya bukan hanya validasi client (UX) tapi juga panggilan API ke server/Flask untuk double validasi (client + server): client memvalidasi ke server, server cek ke DB dan merespons untuk memastikan stok benar habis dan tidak melakukan transaksi."
- Koreksi: cara ke-3 terlewat: **race condition**. Solusi "cek dulu lalu beli" masih punya celah **TOCTOU (Time-Of-Check to Time-Of-Use)**: dua user sama-sama lolos cek stok = 1, lalu dua-duanya membeli → stok -1. Solusi benar: pengecekan stok terjadi **di dalam request pembelian** dan dilakukan **atomik**, mis. `UPDATE products SET stock = stock - 1 WHERE id = 42 AND stock > 0;` → 0 baris ter-update = habis → tolak (409 Conflict). Dibahas di S24.

**R6. Tier pengecekan password + kenapa bukan client/DB** ✅
- Jawaban Aca: "1) server / Flask, 2) client bisa dibypass karena seluruh code client bisa di-inspect / diubah, lalu bukan di database karena di database seharusnya password hanya berbentuk hash yang tersimpan di table."
- Catatan: kali ini menjawab persis yang ditanya (kemarin menjawab "kenapa" saat ditanya "di mana").

### B. Latihan Understand — "Label status deadline lamaran" (5/10)
- Jawaban Aca:
  - INPUT: tanggal, jam, Data
  - OUTPUT: label kategori (Terlambat / Hari ini / Mendesak / Aman)
  - Batas: Terlambat (≥1 menit setelah waktu pengumpulan), Hari ini (kapanpun asalkan sebelum deadline), Mendesak (Hari H deadline), Aman (H-7 dari deadline)
  - Contoh (deadline 22/09/2026 23.59): [22/09 23:59, valid] → terkumpul + mendesak; [10/09 23:59, valid] → terkumpul + aman; [20/09 10:00, valid] → terkumpul + hari ini; [23/09 00:00, valid] → terkumpul + terlambat; [10/09 23:59, invalid] → tidak terkumpul
  - Klarifikasi: (1) label untuk job poster atau job seeker? (2) kalau job poster, apakah label diganti "Baru di-post"? (3) kalau job seeker, apakah label Aman tidak diperlukan? (4) data invalid saat submit diterima atau ditolak dengan 400?
- Bagus: klarifikasi #1 (siapa user-nya) = pemikiran level product; edge case 23:59 vs 00:00 (boundary); memikirkan data invalid.
- Koreksi:
  - **Menyelesaikan soal yang berbeda**: soalnya = seberapa dekat deadline dari **waktu sekarang**; Aca mengartikan = kapan lamaran **dikumpulkan**. Pertanyaan klarifikasi terpenting yang terlewat: "label dihitung relatif terhadap waktu apa?"
  - Aturan label **tumpang tindih & ada celah**: "Hari ini" mencakup semua waktu sebelum deadline; "Mendesak" dan "Hari ini" tertukar; "Aman" = tepat H-7 → H-6..H-1 tidak terdefinisi. Contoh #3 tidak konsisten dengan aturan sendiri. Aturan emas: **MECE** (mutually exclusive, collectively exhaustive).
  - Jawaban model: INPUT deadline + now (now dijadikan input supaya pure/testable); aturan: deadline < now → Terlambat; sisa_hari = 0 → Hari ini; 1–3 → Mendesak; >3 → Aman. Edge: deadline 22/09 09:59 dengan now 22/09 10:00 → Terlambat (hari sama, jam lewat); tepat 3 hari; 26/09 00:00 → Aman; deadline kosong. Klarifikasi: ambang Mendesak, hitung per tanggal vs per 24 jam, zona waktu, lamaran tanpa deadline, lamaran yang sudah dikirim.

### C. Latihan Pseudocode LabelDeadline (percobaan 1: 2/10)
- Jawaban Aca:
  ```
  Terlambat ← deadline < now
  Hari ini ← sisa_hari == 0
  Mendesak ← 1 <= sisa_hari <= 3
  Aman ← sisa_hari > 3
  untuk setiap hasil status lamaran
      cek apakah status ← deadline < now || sisa_hari == 0 || 1 <= sisa_hari <= 3 || sisa_hari > 3
  Jika sisa_hari tidak sama dengan 0 maka
     kembalikan sisa_hari
  kembalikan status
  ```
- Koreksi (6 masalah): (1) label dijadikan nama variabel boolean, padahal label = data yang dikembalikan; (2) semua kondisi di-OR-kan → selalu true, tidak tahu label mana; (3) mengembalikan `sisa_hari` (angka), bukan label; (4) `sisa_hari` tidak pernah dihitung (NameError); (5) loop "untuk setiap lamaran" tidak perlu, karena satu fungsi = satu lamaran; (6) deadline kosong & dry-run tidak dikerjakan.
- Akar masalah: sudah bisa menyebut kondisi, tapi belum paham **mekanisme rantai JIKA / JIKA TIDAK, JIKA** (if/elif/else): dicek atas → bawah, berhenti di yang pertama benar.
- Versi benar: guard `deadline KOSONG → "Tanpa deadline"`; `deadline < now → "Terlambat"`; hitung `sisa_hari`; `= 0 → "Hari ini"`; `≤ 3 → "Mendesak"`; `JIKA TIDAK → "Aman"`. Cabang Mendesak cukup `≤ 3` karena kasus ≤ 0 sudah tersaring di atas.

### D. Latihan ulang (A dry-run 1/3 · B ◐ · C ◐)
**A. Dry-run (now = 22/09 10:00)**
| deadline | Jawaban Aca | Benar |
|---|---|---|
| 22/09 09:59 | deadline<now: no · sisa 0 · "Hari ini" · cabang 3 ❌ | **Ya** (09:59 < 10:00) → **Terlambat**, cabang 2, sisa_hari tidak dihitung |
| 25/09 23:59 | no · 3 · "Aman" · cabang 5 ◐ | no · 3 · **Mendesak** (3 ≤ 3) · cabang 4 |
| KOSONG | no · 0 · "Tanpa deadline" · cabang 1 ◐ | "Tanpa deadline", cabang 1 ✅; kolom lain **"— tidak dieksekusi"** |
- Pelajaran: baris 1 adalah edge case yang sudah ditandai sebelumnya ("hari sama, jam lewat"), terlewat karena membaca sekilas. Trace table = rekaman eksekusi nyata; yang tidak dieksekusi tidak punya nilai.

**B. Tambah label "Minggu ini" (4–7 hari), Aman > 7** ◐
- Jawaban Aca: `= 0 → Hari ini`; `≤ 3 → Mendesak`; `>= 4 → Minggu ini`; `> 7 → Aman`.
- Koreksi: **dead code**: `>= 4` menangkap semua angka > 7 sehingga "Aman" tidak pernah tercapai. Benar: `≤ 7 → Minggu ini` (batas atas), lalu `JIKA TIDAK → Aman`.

**C. Kalau "Mendesak (≤3)" dicek sebelum "Terlambat"?** ◐
- Jawaban Aca: "cabang jika-jika tidak jadi salah dan salah satu label akan error, contoh: sisa hari tidak bisa diproses dan error karena sisa hari dipakai sebelum dihitung."
- Koreksi: poin dependensi urutan valid, tapi bukan inti. Inti: deadline sudah lewat → sisa_hari negatif (mis. -2) → -2 ≤ 3 → salah dapat "Mendesak". "Terlambat" harus dicek paling awal untuk menyaring angka negatif.

### E. Drill ketelitian (6/6) ✅
- Jawaban Aca: 1) `10:00 < 10:00` tidak ✅ 2) `3 ≤ 3` ya ✅ 3) `-2 ≤ 3` ya ✅ 4) `22/09 09:59 < 22/09 10:00` ya ✅ 5) `8 ≤ 7` tidak ✅ 6) sisa 7 → "Minggu ini", cabang 3 ✅
- Kesimpulan: masalahnya kecepatan/ketelitian membaca, bukan pemahaman.

### F. Lab flowchart (`phase1/s02/`)
PNG sekarang terbaca (pelajaran export S01 diterapkan ✅). File `.drawio` sumber belum di-commit.

**Soal 1 · LabelDeadline flowchart** — 2.5/4
- Bagus: urutan benar, sisa_hari dihitung setelah cek Terlambat, semua decision berlabel Ya/Tidak.
- Koreksi: (1) semua cabang "Ya" masuk ke **satu** kotak output berisi semua label di-OR-kan (miskonsepsi yang sama dengan pseudocode C), harus satu kotak output per label; (2) diamond ke-6 `sisa hari > 7` = dead code, dan cabang "Tidak"-nya kembali ke atas = potensi **infinite loop**; cukup `JIKA TIDAK → "Aman"`; typo "tabggal".

**Soal 2 · ATM** — 2/4
- (a) Understand, jawaban Aca: INPUT: PIN, NOMINAL (kelipatan 50.000) · OUTPUT: SISA_SALDO, UANG (integer) · contoh: (1) PIN valid 1x, 100.000 → uang + sisa saldo; (2) PIN salah 2x lalu valid, nominal > saldo → "Saldo tidak cukup"; (3) PIN salah 3x → kartu terblokir + "Hubungi bank"; (4) PIN valid, 59.000 → "Masukkan nominal yang valid"; (5) PIN valid, 1.000.000 → uang + sisa saldo.
  - Koreksi: **SALDO tidak ada di INPUT**; pesan (blokir/saldo tidak cukup/nominal invalid) juga output; edge case terlewat: nominal = saldo, nominal 0/negatif. Contoh #4 (59.000) bagus.
- (b) Flowchart: 🐛 `SISA_SALDO = Nominal − saldo` **terbalik** (benar: `saldo ← saldo − nominal`); 🐛 loop nominal "Tidak" kembali ke decision yang sama tanpa input baru = **infinite loop** (harus kembali ke input + tampilkan pesan); ⚠️ PIN di-unroll jadi 3 diamond dan PIN hanya diinput sekali, seharusnya loop dengan counter `percobaan`.
- (c) Pseudocode, jawaban Aca:
  ```
  JIKA PIN 3X invalid MAKA Kembalikan "Kartu diblokir"
  SISA SALDO <- NOMINAL(input) - SALDO(saldo akhir)
  JIKA NOMINAL > SALDO MAKA Kembalikan "Saldo Anda Tidak Cukup"
  JIKA TIDAK, JIKA NOMINAL kelipatan 50.000 MAKA Kembalikan SISA_SALDO, UANG
  JIKA TIDAK Kembalikan "Masukkan Kembali Nominal yang Valid"
  ```
  - Koreksi: tidak ada loop/counter PIN; rumus saldo terbalik; cek saldo **sebelum** cek kelipatan (aturan: validasi format input dulu, baru aturan bisnis); "masukkan kembali" butuh loop, bukan KEMBALIKAN.
- (d) Dry-run (saldo 200rb, PIN salah 1x lalu benar, nominal 75rb lalu 150rb), jawaban Aca: `1 | 2 (benar) | 150rb | 200rb | UANG, SISA_SALDO(50rb)` · `2 | 3 (benar) | 75rb | 200rb | nominal tidak valid` · `3 | 3 (salah) | x | 200rb | kartu diblokir` ❌
  - Koreksi: urutan terbalik, percobaan PIN salah hitung, baris "kartu diblokir" karangan. Benar: (1) PIN salah → "PIN salah"; (2) PIN benar; (3) 75.000 → "Nominal harus kelipatan 50.000"; (4) 150.000 → uang 150.000, saldo 200.000 → 50.000. Catatan: angka sisa 50rb di kepala benar, tapi rumus tertulis terbalik (pola ketelitian).

**Soal 3 · CV Screening (stretch)** — flowchart ✅ logika benar, pseudocode 🐛
- Pseudocode Aca: `JIKA IPK >= 3.0 || 2 Project live DAN JIKA SKILL python || js MAKA "Lolos" JIKA TIDAK "Tidak Lolos"`
- Aca meminta mentor yang menguji 4 kondisi. Hasil uji mentor: kasus IPK 3.5 + 0 project + Go → flowchart "Tidak Lolos" ✅, pseudocode "Lolos" ❌.
- Koreksi: **operator precedence**: AND dievaluasi sebelum OR, jadi terbaca `IPK>=3 || (project AND python) || js`. Selalu pakai kurung: `(IPK >= 3.0 OR project_live >= 2) AND ("Python" IN skills OR "JavaScript" IN skills)`. Diamond "2 Project Live?" harus `project_live >= 2?` (kalau "tepat 2", 3 project gagal). Kotak proses `Lolos = ...` di atas flowchart redundan & bertentangan dengan diamond; hapus.

### G. Exit ticket S02
**G1. Tulis 4 test case CV screening tanpa melihat review** — 2.5/4
- Jawaban Aca: menulis ulang pseudocode dengan kurung ✅, lalu tabel 6 baris. Baris 1–4 **disalin dari tabel review mentor** (termasuk catatan "⚠️ tergantung (lihat bawah)"), melanggar instruksi "tanpa melihat review". Baris milik Aca sendiri:
  - #5: IPK 3.0 · project 2 · Rust → Tidak Lolos ✅ (boundary + IPK tinggi tapi gagal)
  - #6: IPK 3.0 · project 2 · JS → Lolos ✅ (boundary)
- Koreksi: kasus #5 & #6 bagus (tepat di batas). Tapi keduanya menguji kombinasi yang sama (IPK dan project sama-sama di batas), jadi tidak mengisolasi batas IPK saja (mis. IPK 3.0, project 0) atau project saja (IPK 2.0, project 2). Baris #3 dibiarkan "tergantung" padahal dengan `>= 2` jawabannya Lolos. Merancang test case = skill yang dinilai di interview; tidak boleh didelegasikan.

**G2. `True OR False AND False` = ?** ◐
- Jawaban Aca: "TRUE"
- Koreksi: hasil benar, tapi urutan evaluasi tidak dijelaskan (diminta). AND dulu: `False AND False = False` → `True OR False = True`.

**G3. Kapan loop jadi infinite loop + 2 tempat di lab** ◐
- Jawaban Aca: "infinite loop terjadi jika ada suatu kondisi yang tidak membutuhkan suatu decision / decision tambahan, akhirnya dari decision yang tidak diperlukan itu bisa menyebabkan percabangan tanpa henti, atau bisa juga karena menggunakan fungsi yang salah, misalkan seharusnya menggunakan counter, saya malah menggunakan decision yes or no. Saya hampir membuatnya di diamond ke-6 di flowchart soal 1, dan di diamond ke-2 (nominal masukkan = kelipatan 50.000? di panah tidaknya)."
- Koreksi: dua lokasi ✅ tepat. Definisi kurang tepat. Definisi benar: **loop jadi infinite ketika tidak ada yang berubah di dalam loop yang bisa membuat kondisi berhentinya terpenuhi** (state yang dicek kondisi tidak pernah diperbarui). Aturan: setiap loop wajib (1) mengubah sesuatu setiap iterasi (input baru / counter +1) dan (2) perubahan itu bergerak menuju kondisi keluar.

### H. Ringkasan skor S02
| Aspek | Hasil |
|---|---|
| Warm-up review bank | 5.5/6 📈 (S01: 3.5/5) |
| Understand deadline | 5/10 |
| Pseudocode percobaan 1 | 2/10 |
| Latihan ulang | A 1/3 · B ◐ · C ◐ |
| Drill ketelitian | 6/6 ✅ |
| Lab: Soal 1 / Soal 2 / Soal 3 | 2.5/4 · 2/4 · flowchart ✅ pseudocode 🐛 |
| Exit ticket | G1 2.5/4 · G2 ◐ · G3 ◐ |

---

# Review Bank — pertanyaan yang harus dites ulang (spaced repetition)
Muncul lagi di warm-up sesi berikutnya sampai dijawab benar 2x berturut-turut.

| # | Pertanyaan | Asal | Benar berturut-turut |
|---|---|---|---|
| R1 | Arti 301 | S01-F2 | 1/2 |
| R2 | Arti 401 vs 403 (+ authentication vs authorization) | S01-F2, D2 | 1/2 |
| R3 | Arti 400 vs keluarga 4xx | S01-F2 | 1/2 |
| R4 | Collection kosong (200 []) vs single resource tidak ada (404) | S01-F3, Lab | 1/2 |
| R5 | 3 cara menembus tombol disabled (termasuk race condition) + solusi atomik / TOCTOU | S01-D1, S02-A | 0/2 |
| R6 | Di tier mana password dicek & kenapa bukan tier lain | S01-D2 | 1/2 |
| R7 | Urutan DNS resolution (cache → hosts → resolver → root → TLD → authoritative) | S01-B1 | 0/2 |
| R8 | TCP handshake vs TLS handshake; isi sertifikat & peran CA | S01-B2 | 0/2 |
| R9 | Kenapa 1 halaman = banyak request; HTTP/2, cache, lazy load | S01-B3 | 0/2 |
| R10 | 4 ciri algoritma yang baik | S01-A1 | 0/2 |
| R11 | Kenapa GraphQL "ambil data" pakai POST | S01-B3 (belum dijawab) | 0/2 |
| R12 | MECE: aturan kategori tidak tumpang tindih & tanpa celah | S02-B | 0/2 |
| R13 | Mekanisme rantai JIKA/JIKA TIDAK: atas → bawah, berhenti di yang pertama benar; kenapa urutan penting (Terlambat dulu) | S02-C, D | 0/2 |
| R14 | Dead code: kapan sebuah cabang tidak pernah tercapai (`>= 4` sebelum `> 7`) | S02-D-B, Lab Soal 1 | 0/2 |
| R15 | Operator precedence AND vs OR + selalu pakai kurung | S02-Lab Soal 3, G2 | 0/2 |
| R16 | Definisi infinite loop + 2 syarat loop yang benar | S02-G3 | 0/2 |
| R17 | Trace table = rekaman eksekusi nyata (yang tidak dieksekusi = "—") | S02-D-A, Lab Soal 2d | 0/2 |
| R18 | Urutan validasi: format input dulu, baru aturan bisnis | S02-Lab Soal 2c | 0/2 |

# Weakness tracker
- **Membaca kondisi sekilas** (09:59 vs 10:00, `≤` dibaca `<`, rumus saldo terbalik padahal hitungan mental benar) → selalu baca karakter per karakter saat dry-run. Drill membuktikan bisa 6/6 kalau pelan.
- **Belum paham mekanisme if/elif/else** (label jadi variabel, OR semua kondisi, satu kotak output gabungan) → S03–S04 wajib banyak latihan rantai kondisi.
- **Salah memahami soal** (Understand deadline) → selalu tulis ulang soal dengan kata sendiri + tanya "relatif terhadap apa?" sebelum mengerjakan.
- **Loop belum dikuasai** (PIN di-unroll, loop tanpa input baru) → fokus S05.
- **Mendelegasikan/menyalin bagian latihan** (minta mentor menguji; menyalin tabel review ke exit ticket) → integritas latihan; test design harus dikerjakan sendiri.
- Hafalan jangka pendek: membaik (warm-up 5.5/6), lanjutkan review bank.
- Security mindset: membaik (2/3 cara), belum paham race condition.
- Kekuatan: pertanyaan klarifikasi level product (siapa user-nya), insting boundary (23:59 vs 00:00, IPK tepat 3.0), jujur mengidentifikasi letak kesalahan sendiri (G3), cepat merespons feedback, export diagram sudah benar.

# Next up
- Revisi S02 (prioritas): ATM (rumus saldo, loop nominal ke input, PIN counter loop, saldo di input, urutan validasi); Soal 1 (satu output per label, hapus diamond ke-6); Soal 3 (kurung, `>= 2`, hapus kotak proses); commit file `.drawio` + `atm.md` & `cv-screening.md`.
- Revisi S01 masih tertunda: sequence diagram (export ulang, DNS, error cause) + `notes/http-status-codes.md`.
- Masih menunggu post-mortem penolakan internship.
- S03 (Variabel, Tipe Data, Operator, I/O): warm-up = R5, R12–R16 + R1–R4/R6 (untuk mencapai 2/2).
- Tulis materi Phase 2 per minggu (W4 = S13–S16) sebelum Mon 12 Oct 2026.