# Fullstack Revenge Program — Course Tracker

Personal 21-week program modeled on the RevoU Full Stack SE syllabus (4 phases, 84 live sessions).
Mentor role: recruiter + senior fullstack engineer. Language: Indonesian, technical terms in English.

## Schedule
- Mon–Thu 19.00–21.00 WIB live class (S01 = Mon 21 Sep 2026) · Fri assignment day · Sat 13.00–15.30 review + HackerRank + Career+ task
- Student starts each class with "Mulai Sxx" (may start earlier when free)

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

## S01 — Cara Program Berpikir + Arsitektur Web App
Done Mon 21 Sep 2026 (morning, ahead of the 19.00 slot).
Legend: ✅ correct · ◐ partially correct · ❌ wrong · ❓ "tidak tahu" / no answer

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

**Q5. "Masak nasi sampai matang, lalu sajikan secukupnya" — algoritma baik atau buruk?** ✅
- Jawaban Aca: "Buruk. Nasi matang itu tahu dari mana? Masak berapa lama? Secukupnya itu sebenarnya sebanyak apa?"
- Koreksi: Sempurna. Menemukan pelanggaran ciri "tidak ambigu" dan "pasti berhenti".

### B. Latihan A — Tulis ulang resep nasi sebagai algoritma (6/10)
- Jawaban Aca: INPUT: Beras · OUTPUT: Nasi yang matang · LANGKAH: 1) Masukkan 3 cup nasi ke rice cooker, 2) Tuangkan air 3 gelas, 3) Masak nasi selama 10 menit hingga matang, 4) Sajikan nasi yang sudah matang 5 sendok makan di piring.
- Koreksi (4 bug):
  1. State salah: "3 cup **nasi**" — yang dimasukkan masih **beras** (setara salah menamai variabel).
  2. Masih ambigu: "10 menit **hingga matang**" — kalau 10 menit belum matang, lalu apa?
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
- v2 (`phase1/SequenceDiagram-ApplyTrack.drawio.png`) — konten 3/4, tapi **export PNG rusak** (panah & teks tidak terlihat: warna default di tema gelap + background transparan). Konten diekstrak dari XML yang tertanam di PNG.
  - Bagus: User actor terpisah, happy path + error path, pesan error ramah & tidak bocor detail teknis, query SQL spesifik.
  - Perbaikan: tambah lifeline DNS; tulis `GET /jobs?city=jakarta`; pecah step 6 jadi self-arrow validasi + panah SQL ke PostgreSQL; routing ke **fungsi/handler** bukan "file"; server **mengembalikan** 500 + JSON, browser yang **menampilkan**; error path harus menunjukkan **penyebab** (DB mati / connection refused), bukan "cari Aceh → 500" (kota tanpa lowongan = 200 []).
  - Repo: pindahkan ke `phase1/s01/sequence-diagram.png` via `git mv`, commit juga file sumber `.drawio`.
  - **Status: menunggu perbaikan.**

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

# Review Bank — pertanyaan yang harus dites ulang (spaced repetition)
Semua item ❓/❌ dari sesi sebelumnya. Muncul lagi di warm-up sesi berikutnya sampai dijawab benar 2x berturut-turut.

| # | Pertanyaan | Asal | Benar berturut-turut |
|---|---|---|---|
| R1 | Arti 301 | S01-F2 | 0/2 |
| R2 | Arti 401 vs 403 (+ authentication vs authorization) | S01-F2, D2 | 0/2 |
| R3 | Arti 400 vs keluarga 4xx | S01-F2 | 0/2 |
| R4 | Collection kosong (200 []) vs single resource tidak ada (404) | S01-F3, Lab | 0/2 |
| R5 | Kenapa tombol disabled tidak cukup (3 cara menembus) | S01-D1 | 0/2 |
| R6 | Di tier mana password dicek & kenapa bukan tier lain | S01-D2 | 0/2 |
| R7 | Urutan DNS resolution (cache → hosts → resolver → root → TLD → authoritative) | S01-B1 | 0/2 |
| R8 | TCP handshake vs TLS handshake; isi sertifikat & peran CA | S01-B2 | 0/2 |
| R9 | Kenapa 1 halaman = banyak request; HTTP/2, cache, lazy load | S01-B3 | 0/2 |
| R10 | 4 ciri algoritma yang baik | S01-A1 | 0/2 |
| R11 | Kenapa GraphQL "ambil data" pakai POST | S01-B3 (belum dijawab) | 0/2 |

# Weakness tracker
- Hafalan jangka pendek: materi yang diajarkan dalam sesi yang sama bisa hilang (401/403) → review bank + flashcards.
- Security mindset belum refleks: "never trust the client".
- Menjawab "kenapa" saat ditanya "di mana" → latih menjawab pertanyaan persis.
- Overgeneralization aturan baru (collection vs single resource).
- Menjawab dengan hafalan materi, belum dengan pemahaman (Q2 warm-up).
- Kekuatan: peka ambiguitas, cepat merevisi setelah feedback, insting UX pesan error bagus, inisiatif (User actor di sequence diagram).

# Next up
- PR sebelum S02: perbaiki diagram (tema terang, DNS, error cause, pindah ke phase1/s01, commit .drawio); buat `notes/http-status-codes.md` dengan kata-kata sendiri + contoh; baca materi S02.
- Masih menunggu post-mortem penolakan internship.
- S02 (Flowchart & Pseudocode) Tue 22 Sep 19.00; warm-up = Review Bank R1–R6.
- Tulis materi Phase 2 per minggu (W4 = S13–S16) sebelum Mon 12 Oct 2026.