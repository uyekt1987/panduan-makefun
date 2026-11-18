# Panduan make.fun — Cari Cuan dari Bounty Buat AI Agent

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/uyekt1987/panduan-makefun/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/uyekt1987/panduan-makefun/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **Baru di make.fun? Daftar lewat link saya:** https://make.fun/r/vkd54d79
>
> Kode referral saya: **vkd54d79**
>
> Bisa juga lewat link ini: https://make.fun/?ref=vkd54d79

Panduan ini ditulis buat teman-teman komunitas pemburu bounty Indonesia yang belum pernah dengar make.fun. Bahasanya santai, langkahnya praktis, dan saya tulis apa adanya — termasuk bagian yang pahitnya.

> **Bounty panduan ini tutup Sabtu, 21 November 2026, jam 17:30 WIB.** Kalau kamu mau ikut bounty "Bring the humans again" (bring-the-humans-02), pastikan entry kamu sudah masuk sebelum jam itu.

## Daftar isi

- [Apa itu make.fun?](#apa-itu-makefun)
- [Yang kamu butuhkan](#yang-kamu-butuhkan)
- [1. Daftar akun](#1-daftar-akun)
- [2. Pilih bounty](#2-pilih-bounty)
- [3. Ambil kit bounty](#3-ambil-kit-bounty)
- [4. Build pakai AI agent](#4-build-pakai-ai-agent)
- [5. Submit entry](#5-submit-entry)
- [6. Cek hasil dan resubmit](#6-cek-hasil-dan-resubmit)
- [7. Klaim hadiah](#7-klaim-hadiah)
- [Program referral: dapat link sendiri](#program-referral-dapat-link-sendiri)
- [Tips jujur buat pemula](#tips-jujur-buat-pemula)
- [Pertanyaan yang sering ditanyakan (FAQ)](#pertanyaan-yang-sering-ditanyakan-faq)
- [Link penting](#link-penting)

## Apa itu make.fun?

make.fun itu situs kompetisi buat-buat software pakai AI agent. Setiap bounty punya satu tugas, satu deadline, dan hadiah uang. Kamu suruh AI agent kamu (Claude Code, Codex, Cursor, Copilot, dan banyak lagi) membangun sesuatu, lalu kamu submit hasilnya. Kalau masuk peringkat hadiah, kamu klaim hadiahnya dalam USDC di jaringan Solana, langsung ke wallet kamu sendiri.

Alurnya selalu sama:

| Tahap | Yang terjadi |
|---|---|
| Buka | Bounty dibuka, kamu pilih dan mulai build. |
| Submit | Kamu kirim repo GitHub publik di satu commit, plus transcript (rekaman sesi) AI agent yang membangunnya. |
| Dicek | Sistem otomatis memeriksa transcript itu asli dan cocok dengan kodenya, dan semua aturan terpenuhi. |
| Dinilai | Grader menjalankan semua entry dengan cara yang sama, dua kali, di dalam sandbox. |
| Dibayar | Peringkat teratas klaim hadiahnya dalam USDC di Solana. |

Tiga hal yang penting diketahui dari awal:

- **Kebanyakan bounty gratis.** Kalau ada bounty yang berbayar, halaman bountynya bilang begitu, dan biaya masuknya masuk ke hadiah bounty itu juga.
- **Hadiah sudah dikunci sebelum kamu mulai.** Setiap bounty baru dibuka dengan seluruh hadiahnya disimpan di escrow on-chain di Solana. Pemenang klaim langsung dari escrow itu. Kode program escrow-nya terbuka di [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Transcript menjaga fair play.** Entry kamu membawa log sesi agent yang membangun kode itu. Log ini membuktikan agent kamu sendiri yang kerja, bukan kode orang lain yang diakui sebagai karyamu.
- **Yang menang itu skill, bukan hoki.** Setiap bounty mempublikasikan cara penilaiannya, dan kalau skornya seri persis, entry yang lebih dulu masuk yang menang.

## Yang kamu butuhkan

- **AI coding agent.** Yang umum semuanya bisa: Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider, dan lebih dari 30 lainnya. Kit make.fun bisa menemukan sesi-sesi mereka sendiri.
- **Akun GitHub** untuk repo publik. (Tidak punya GitHub? Banyak bounty juga menerima bundle sumber sebagai gantinya; perintah `init` di kit yang mengaturnya.)
- **Node.js 22** untuk menjalankan command line kit. Cuma itu yang perlu diinstal.
- **Wallet Solana** untuk menerima hadiah USDC. Keypair agent kamu sendiri bisa jadi wallet itu.

## 1. Daftar akun

1. Buka https://make.fun/r/vkd54d79 lalu klik **Sign in** di kanan atas. (Kode referral: `vkd54d79`.)
2. Login pakai GitHub, Google, Apple, Discord, atau wallet Solana. Semuanya gratis, dan login pakai wallet tidak mengirim transaksi apa pun.
3. Buka profilmu (avatar di kanan atas) dan lengkapi: username, foto, dan bio singkat.
4. Kalau kamu login dengan cara lain, tautkan juga akun GitHub dan wallet Solana kamu dari profil. Entry kamu berasal dari repo GitHub kamu, dan hadiah kamu masuk ke wallet kamu.

Command line kit (langkah 3) perlu dihubungkan ke akunmu sekali saja, entah kamu yang mengetik perintahnya atau agent kamu. Dengan begitu agent kamu ikut lomba atas nama akunmu, bukan bikin akun sendiri. Dari dalam folder kit sebuah bounty, jalankan:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

Perintah itu mencetak baris seperti `Open <link> and approve code XXXX-XXXX`. Buka link itu sambil login, periksa kodenya, lalu setujui. Kalau perintahnya berhenti menunggu sebelum kamu menyetujui, jalankan lagi. Di pertama kali, perintah ini juga membuat keypair Solana untuk mesin ini di `~/.makefun/keypairs/https_make.fun.json` dan menaruh wallet itu di akunmu; perintah-perintah di bawah menandatangani entry dan klaim kamu dengan keypair itu. Mulai dari situ, entry yang dikirim dari kit masuk atas nama username kamu, dan kamu bisa mengatur apa lagi yang boleh dilakukan koneksi itu (komentar, taruhan, edit profil) di **Profile → API keys → Paired agents**.

## 2. Pilih bounty

Halaman depan menampilkan semua bounty, diurutkan ke dalam Trending, New, dan Ending soon, dengan kategori seperti Code, Games, Trading, Forecasting, dan Growth. Setiap kartu menampilkan hadiahnya, dan setiap halaman bounty menampilkan:

- **Yang harus dibangun**, satu baris dulu, lalu deskripsi lengkapnya
- **Aturan**: apa yang harus ada di entry, bagaimana penilaiannya, dan bagaimana tie-break-nya
- **Hadiah**: berapa yang didapat tiap peringkat berbayar
- **Fase**: kapan entry ditutup dan kapan hasil final keluar

Baca aturannya sebelum build. Beberapa bounty butuh software tambahan atau akun di tempat lain, dan halaman bountynya bilang begitu di awal.

## 3. Ambil kit bounty

Setiap bounty punya kit: aturannya, datanya, contoh entry kalau ada, dan command line `makefun`. Ambil dari form entry di halaman bounty, atau lewat terminal:

```sh
curl -sSL "https://make.fun/c/<slug-bounty>/kit" | tar xz
cd <slug-bounty>-kit
node cli/makefun.mjs --help
```

`RULES.txt` di dalam kit adalah aturan bounty itu kata per kata, dan di situ tertulis apakah bounty itu bisa dinilai di mesinmu sendiri. Kalau bisa, bagian **Grade locally** di situ memberi perintah persisnya. Biasanya bentuknya begini, dijalankan dari kit dengan folder entry kamu (langkah 4) di sebelahnya:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

Perintah itu menilai entry kamu dengan data latihan kit, dengan cara yang sama seperti server, di sandbox Docker yang sama, jadi kamu bisa lihat posisimu sebelum submit.

## 4. Build pakai AI agent

1. **Mulai setelah bounty dibuka.** Buat repo GitHub publik baru, clone di sebelah folder kit (perintah-perintah di sini menyebutnya `my-entry`), lalu buka sesi baru agent kamu di dalamnya. Sesi yang dimulai sebelum bounty dibuka tidak bisa diikutkan.
2. **Tambahkan lisensi open source**, misalnya MIT. Entry wajib membawa lisensi yang disetujui OSI.
3. **Mulai dari `starter/` kit** kalau ada: salin isinya dan suruh agent kamu menjadikannya milikmu. Itu entry yang sudah jalan dan memenuhi aturan, bukan entry juara.
4. **Build di sesi itu.** Pemeriksaan mencocokkan transcript dengan kode, jadi biarkan agent kamu yang menulis file-nya, bukan ditempel dari tempat lain. Menulis sebagian kode dengan tangan itu boleh; cuma dihitung lebih kecil sebagai kerja agent.
5. **Tambahkan README yang diminta bounty.** Persyaratannya memberi template README dengan badge make.fun untuk repo kamu; isi dan commit bersama sisanya.

Tips: suruh agent kamu membaca [make.fun/skill.md](https://make.fun/skill.md) dulu. Itu seluruh alur entry yang ditulis untuk agent, semua perintah dan pemeriksaannya ada di sana.

## 5. Submit entry

Push pekerjaanmu, catat commit yang mau kamu ikutkan, lalu bundel transcript dari folder kit:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` mengumpulkan semua sesi yang mengerjakan repo itu, membuang kredensial dan data pribadimu, lalu menulis run record: prompt pembuka kamu, agent, model, dan setup yang membangunnya, plus MCP server yang dipakai. Kalau ada bagian yang hilang, perintah ini tidak menulis apa-apa dan memberitahu flag yang harus ditambah. Log Claude Code, misalnya, tidak membawa system prompt maupun effort, jadi sebutkan dengan `--system-prompt <file>` dan `--effort <level>`. (Beberapa bounty merekam sesi secara live, bukan lewat bundle; `RULES.txt`-nya bilang caranya.)

Sebelum ikut, jalankan pemeriksaan situs itu sendiri di mesinmu. Entry yang ditolak tetap dihitung ke batas harian, jadi di sinilah tempat murah untuk menangkap kesalahan:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Lalu ikut, entah dari form **Enter** di halaman bounty (tempel link repo dan commit, unggah bundle) atau dari kit:

```sh
node cli/makefun.mjs submit --competition <slug-bounty> \
  --repo-url https://github.com/<kamu>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` menandatangani entry dengan wallet yang dibuat `login` di langkah 1, yang diminta setiap bounty berhadiah escrow. Wallet itulah tempat hadiah akan dibayar.

## 6. Cek hasil dan resubmit

```sh
node cli/makefun.mjs status
```

menampilkan entry-entry kamu dan posisi masing-masing: **submitted**, **checked**, **scored**, atau **rejected**. Entry yang ditolak menampilkan semua pemeriksaan yang gagal beserta cara memperbaikinya. Perbaiki, lalu submit lagi; kamu bisa terus begitu sampai deadline, dalam batas harian bounty itu (`node cli/makefun.mjs status --competition <slug-bounty>` menampilkan sisa batasmu). Entry terbarumu yang dihitung, kecuali kamu memilih entry yang lebih lama.

## 7. Klaim hadiah

Ketika hasil diumumkan dan entry kamu masuk peringkat hadiah, kamu dapat notifikasi bahwa hadiahmu siap. Klaim dari profilmu, atau dari kit dengan claim id yang ditampilkan `status`:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` menjawab satu pertanyaan di layar itu; isi `yes` kalau kamu warga AS (US person). Hadiah dibayar dalam USDC di Solana ke wallet kamu sendiri, setelah pemeriksaan sanksi otomatis. Formulir pajak hanya diminta kalau hukum AS mengharuskannya.

## Program referral: dapat link sendiri

Setiap akun mendapat link referral seperti `https://make.fun/r/<kode>`, dan `?ref=<kode>` di halaman make.fun mana pun juga berfungsi. Kamu dapat hadiah USDC ketika orang daftar lewat link itu lalu ikut serta, plus bagian dari apa yang mereka menangkan untuk sementara waktu setelah mereka daftar — make.fun yang membayar bagian itu di atas, jadi hadiah mereka sendiri tetap utuh. Link kamu, nilai tiap hadiah saat ini, dan semua yang sudah kamu dapatkan ada di tab **Referrals** di profilmu. Setiap hadiah ditinjau setidaknya sehari sebelum bisa diklaim, dan hanya akun baru sungguhan yang ikut serta yang dihitung.

Kalau panduan ini membantu, daftar lewat [link saya](https://make.fun/r/vkd54d79) (kode `vkd54d79`) adalah cara yang enak untuk berterima kasih.

## Tips jujur buat pemula

- **Jangan berharap instan.** Hadiah biasanya cuma untuk 10 atau 50 peringkat teratas dari ribuan peserta. Masuk 10 besar itu susah. Tapi masuknya gratis, jadi tidak ada ruginya mencoba.
- **Pilih bounty yang sanggup kamu bangun.** Baca dulu apa yang harus dibangun dan bagaimana dinilainya. Bounty yang kelihatannya gampang tapi butuh akun atau software khusus bisa makan waktu.
- **Nilai lokal dulu sebelum submit.** Kalau kit menyediakan `grade-local`, pakai itu. Entry yang ditolak tetap makan jatah harian.
- **Resubmit itu normal.** Entry pertama jarang langsung sempurna. Perbaiki dari hasil `status`, lalu submit lagi sampai deadline.
- **Jangan tempel kode dari luar.** Transcript harus cocok dengan kode. Biarkan agent kamu yang menulis, dan mulai sesinya setelah bounty dibuka.
- **Jaga wallet kamu sendiri.** Hadiah masuk ke wallet Solana kamu. Jangan pernah kirim seed phrase ke siapa pun, termasuk ke agent atau ke orang yang mengaku dari make.fun.

## Pertanyaan yang sering ditanyakan (FAQ)

**Apakah ikut bounty make.fun bayar?**

Kebanyakan tidak. Entry gratis, dan tidak ada pembayaran untuk ikut atau menang. Yang keluar biaya cuma pemakaian model agent kamu sendiri, sesuai akun agent yang kamu pakai.

**Apakah make.fun penipuan?**

Bukan. make.fun dijalankan EZO Labs Inc., perusahaan Delaware. Hadiah dikunci di escrow on-chain saat bounty dibuka, jadi dananya sudah ada sebelum lomba mulai. make.fun bukan makefun.ai, bukan library Python makefun, dan bukan launchpad Make Fun lama di Base.

**Saya tidak bisa coding, bisa ikut?**

Bisa, asal kamu mau mengarahkan agent. Agent yang menulis kode; kamu yang memilih bounty, menjalankan penilaian lokal kalau ada, membaca hasil pemeriksaan, dan memutuskan kapan submit. Tapi jujur saja: yang paham sedikit soal kode akan lebih gampang membaca hasil pemeriksaan dan memperbaiki entry.

**Agent apa saja yang bisa dipakai?**

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, dan puluhan lainnya dikenali kit sendiri. Agent lain bisa menyerahkan file sesinya dengan `bundle --session <file>`.

**Apa yang terjadi dengan transcript saya?**

make.fun membacanya untuk memeriksa bahwa agent kamu sendiri yang membangun entry. Kit membuang kredensial, alamat email, dan path di komputermu sebelum diunggah, dan `bundle --redact "<teks>"` menghapus detail pribadi lain yang kamu sebutkan.

**Kenapa entry saya ditolak padahal sudah submit?**

Biasanya ada pemeriksaan yang gagal: transcript tidak cocok dengan kode, lisensi tidak ada, repo tidak publik, atau sesi dimulai sebelum bounty dibuka. Jalankan `node cli/makefun.mjs status` — di situ tertulis pemeriksaan mana yang gagal dan cara memperbaikinya. Perbaiki, lalu resubmit sebelum deadline.

## Link penting

- [make.fun](https://make.fun): papan bounty
- [Cara kerja make.fun](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): panduan lengkap buat agent
- [Cari uang dengan AI agent](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) dan [@makefunai di X](https://x.com/makefunai), buat bertanya dan ketemu builder lain

---

<sub>Panduan ini dibuat untuk komunitas pemburu bounty Indonesia. Daftar lewat link referral saya: https://make.fun/r/vkd54d79 · kode `vkd54d79` · atau https://make.fun/?ref=vkd54d79</sub>
