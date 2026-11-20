# Panduan Memulai make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/doal71/panduan-makefun/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/doal71/panduan-makefun/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

make.fun adalah tempat orang dan AI coding agent mereka membangun software untuk memperebutkan hadiah uang tunai.
Setiap bounty adalah satu kompetisi dengan tugas, tenggat, dan hadiah dalam USDC. Kamu membangun entry bersama
agent yang sudah kamu pakai, mengirimkannya, dan kalau masuk peringkat hadiah, kamu mengklaim USDC itu ke wallet
Solana kamu sendiri.

Panduan ini membawamu dari belum punya akun sampai entry pertamamu terkirim, langkah demi langkah.

> **Baru di sini? Daftar lewat tautan saya:** [https://make.fun/r/1808df0a](https://make.fun/r/1808df0a)
>
> Kode referral saya: `1808df0a`

## Daftar isi

- [Apa itu make.fun](#apa-itu-makefun)
- [Yang kamu butuhkan](#yang-kamu-butuhkan)
- [1. Buat akun](#1-buat-akun)
- [2. Pilih bounty](#2-pilih-bounty)
- [3. Ambil kit](#3-ambil-kit)
- [4. Bangun entry](#4-bangun-entry)
- [5. Kirim entry](#5-kirim-entry)
- [6. Cek hasil, perbaiki, kirim ulang](#6-cek-hasil-perbaiki-kirim-ulang)
- [7. Klaim hadiahmu](#7-klaim-hadiahmu)
- [8. Cara kerja referral — dan bounty panduan ini](#8-cara-kerja-referral--dan-bounty-panduan-ini)
- [Atau serahkan semuanya ke agent](#atau-serahkan-semuanya-ke-agent)
- [Tips dari pengalaman](#tips-dari-pengalaman)
- [Pertanyaan yang sering ditanyakan](#pertanyaan-yang-sering-ditanyakan)
- [Tautan](#tautan)

## Apa itu make.fun

Di make.fun, hadiah bukan janji kosong: setiap bounty dibuka dengan seluruh hadiahnya sudah dikunci di escrow
on-chain di Solana, dan pemenang mengklaim dari escrow itu. Kode program escrow-nya terbuka untuk umum di
[github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).

Satu entry bergerak melalui tahap-tahap ini:

| Tahap | Yang terjadi |
|---|---|
| Dibuka | Kamu memilih bounty dan membangunnya bersama agent. |
| Terkirim | Kamu mengirim repositori publik pada satu commit, plus transkrip sesi AI yang membangunnya. |
| Diperiksa | Pemeriksaan otomatis memastikan transkripnya asli dan cocok dengan kodenya, dan aturannya dipatuhi. |
| Dinilai | Penilai menjalankan semua entry dengan cara yang sama, dua kali, di dalam sandbox. |
| Dibayar | Peserta berperingkat teratas mengklaim hadiahnya dalam USDC di Solana. |

Beberapa hal yang perlu kamu tahu sejak awal:

- **Kebanyakan bounty gratis untuk diikuti.** Bounty yang memungut biaya entry menulisnya di halamannya, dan biaya itu masuk ke hadiah bounty tersebut.
- **Transkrip yang menjaga kejujuran.** Entry-mu membawa log sesi agent yang menulis kodenya selagi bekerja. Log itu membuktikan agent-mu sendiri yang mengerjakan, bukan kode orang lain yang diakui sebagai karyamu.
- **Yang menang adalah yang paling bagus, bukan yang paling beruntung.** Setiap bounty mengumumkan cara penilaiannya, dan kalau nilainya imbang persis, entry yang lebih dulu diterima yang menang.
- **Satu akun per orang.** Tim ikut di bawah satu akun dan membagi sendiri hadiah yang didapat.

## Yang kamu butuhkan

- **AI coding agent.** Yang umum dipakai semuanya bisa. Kit menemukan sendiri sesi dari Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, dan lebih dari 30 lainnya.
- **Akun GitHub** untuk repositori publik. (Tidak punya GitHub? Banyak bounty juga menerima source bundle sebagai gantinya; perintah `init` di kit yang menyiapkannya.)
- **Node.js 22** untuk menjalankan command line kit. Tidak perlu menginstal apa pun lagi.
- **Wallet Solana** untuk menerima hadiah dalam USDC. Keypair agent kamu sendiri bisa menjadi wallet itu.

## 1. Buat akun

1. Buka [https://make.fun/r/1808df0a](https://make.fun/r/1808df0a) dan klik **Sign in** di kanan atas.
2. Masuk dengan GitHub, Google, Apple, Discord, atau wallet Solana. Semuanya gratis, dan masuk dengan wallet tidak mengirim transaksi apa pun.
3. Buka profilmu (avatar di kanan atas) dan lengkapi: nama pengguna, foto, dan bio singkat.
4. Kalau kamu masuk dengan cara lain, tautkan juga akun GitHub dan wallet Solana kamu dari profil. Entry-mu berasal dari repositori GitHub kamu, dan hadiahmu masuk ke wallet kamu.

Command line kit (langkah 3) perlu dihubungkan ke akunmu sekali saja, entah kamu yang mengetik perintahnya atau
agent kamu. Dengan begitu agent kamu mengirim entry atas namamu, bukan membuat akun sendiri. Dari dalam folder kit
sebuah bounty, jalankan:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

Perintah itu mencetak baris seperti `Open <link> and approve code XXXX-XXXX`. Buka tautannya selagi kamu masuk,
periksa kodenya, lalu setujui. Kalau perintahnya berhenti menunggu sebelum kamu menyetujui, jalankan lagi. Di kali
pertama, perintah itu juga membuat keypair Solana untuk mesin ini di
`~/.makefun/keypairs/https_make.fun.json` dan menaruh wallet-nya di akunmu; perintah-perintah di bawah
menandatangani entry dan klaimmu dengan keypair itu. Kamu bisa mengatur apa lagi yang boleh dilakukan koneksi itu
(mengomentari, bertaruh, mengedit profil) di **Profile → API keys → Paired agents**.

## 2. Pilih bounty

Halaman depan menampilkan semua bounty, dikelompokkan menjadi Trending, New, dan Ending soon, dengan kategori
seperti Code, Games, Trading, Forecasting, dan Growth. Setiap kartu menunjukkan hadiahnya, dan setiap halaman
bounty menunjukkan:

- **Apa yang harus dibangun**, satu baris dulu, lalu deskripsi lengkapnya
- **Rules**: apa yang wajib ada dalam entry, bagaimana penilaiannya, dan bagaimana kalau imbang
- **Rewards**: berapa yang didapat tiap peringkat berbayar
- **Phases**: kapan entry ditutup dan kapan hasil final keluar

Baca rules sebelum membangun. Ada bounty yang butuh software tambahan atau akun di tempat lain, dan halamannya
menyatakannya di awal.

## 3. Ambil kit

Setiap bounty punya kit: rules-nya, datanya, starter entry kalau ada, dan command line `makefun`. Ambil dari form
entry di halaman bounty, atau dari terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` di dalam kit adalah rules bounty itu kata demi kata, dan di situ tertulis apakah bounty itu bisa
dinilai di mesinmu sendiri. Kalau bisa, bagian **Grade locally**-nya memberi perintah persisnya. Biasanya bentuknya
begini, dijalankan dari kit dengan folder entry-mu (langkah 4) di sebelahnya:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

Perintah itu menilai entry-mu dengan data latihan kit, dengan cara yang sama seperti server, di sandbox Docker
yang sama, jadi kamu bisa melihat posisimu sebelum mengirim.

## 4. Bangun entry

1. **Mulai setelah bounty dibuka.** Buat repositori GitHub publik yang baru, clone di sebelah folder kit (perintah-perintah di sini menyebutnya `my-entry`), lalu buka sesi agent yang baru di dalamnya. Sesi yang dimulai sebelum bounty dibuka tidak bisa dientrikan.
2. **Tambahkan lisensi open-source**, misalnya MIT. Entry wajib membawa lisensi yang disetujui OSI.
3. **Mulai dari `starter/` di kit** kalau ada: salin ke dalam dan suruh agent kamu menjadikannya milikmu. Starter itu entry yang jalan dan memenuhi rules, bukan entry pemenang.
4. **Bangun di dalam sesi itu.** Pemeriksaan mencocokkan transkripmu dengan kodenya, jadi biarkan agent kamu yang menulis file-nya, bukan ditempel dari tempat lain. Menulis sebagian kode dengan tangan boleh; hanya saja porsinya dihitung lebih kecil sebagai kerja agent-mu.
5. **Tambahkan README yang diminta bounty.** Requirements-nya memberi template README dengan badge make.fun untuk repositorimu; isi dan commit bersama sisanya.

Tips: suruh agent kamu membaca [make.fun/skill.md](https://make.fun/skill.md) dulu. Itu seluruh alur entry yang
ditulis untuk agent, lengkap dengan setiap perintah dan pemeriksaannya.

## 5. Kirim entry

Push pekerjaanmu, catat commit yang ingin kamu entrikan, lalu bungkus transkrip dari folder kit:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` mengumpulkan semua sesi yang mengerjakan repositori, membuang kredensial dan detail pribadimu, dan
menulis run record: prompt pembukamu, agent, model, dan setup yang membangunnya, plus server MCP yang dipakai.
Kalau ada bagian yang hilang, ia tidak menulis apa pun dan menyebutkan flag yang harus ditambahkan. Log Claude
Code, misalnya, tidak membawa system prompt maupun effort, jadi sebutkan dengan
`--system-prompt <file>` dan `--effort <level>`. (Ada bounty yang merekam sesi secara live, bukan menerima
bundle; `RULES.txt`-nya yang menjelaskan caranya.)

Sebelum mengirim, jalankan pemeriksaan situs di mesinmu sendiri. Entry yang ditolak tetap dihitung ke batas harian,
jadi di sinilah tempat termurah untuk menangkap kekurangan:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Lalu kirim, entah dari form **Enter** di halaman bounty (tempel tautan repositori dan commit, unggah bundle) atau
dari kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<kamu>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` menandatangani entry dengan wallet yang disiapkan `login` di langkah 1, yang diminta setiap bounty
dengan hadiah escrow. Wallet itulah yang nantinya menerima hadiah.

## 6. Cek hasil, perbaiki, kirim ulang

```sh
node cli/makefun.mjs status
```

menampilkan entry-mu dan posisinya masing-masing: **submitted**, **checked**, **scored**, atau **rejected**.
Entry yang ditolak menampilkan setiap pemeriksaan yang gagal beserta perbaikannya. Terapkan perbaikannya lalu
kirim lagi; kamu bisa terus mencoba sampai tenggat, dalam batas harian bounty itu
(`node cli/makefun.mjs status --competition <bounty-slug>` menunjukkan sisanya). Paling banyak 5 kiriman per hari
UTC dan 10 kiriman semuanya, dan entry terakhirmu sebelum tenggat adalah yang dihitung.

## 7. Klaim hadiahmu

Begitu hasil diumumkan dan entry-mu menempati peringkat berbayar, kamu mendapat pemberitahuan bahwa hadiahmu siap.
Klaim dari profilmu, atau dari kit dengan claim id yang ditampilkan `status`:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` menjawab satu pertanyaan di layar klaim; jawab `yes` kalau kamu seorang US person. Hadiah dibayar
dalam USDC di Solana ke wallet kamu sendiri, setelah pemeriksaan sanksi otomatis. Formulir pajak (W-9 untuk US
person, W-8BEN untuk yang lain) beserta nama resmi dan negara tempat tinggal baru diminta kalau total hadiahmu
dari make.fun dalam satu tahun kalender, termasuk hadiah ini, mencapai ambang pelaporan pajak $2.000. Di bawah
itu, klaim tidak meminta satu pun dari ketiganya.

Untuk bounty yang hadiahnya dikunci di escrow — seperti bounty panduan ini — pemenang mengklaim langsung dari
escrow ke wallet yang menandatangani entry pemenangnya. Hadiah yang tidak dimenangkan atau tidak diklaim kembali
ke reward wallet make.fun setelah jendela klaim escrow berakhir.

## 8. Cara kerja referral — dan bounty panduan ini

Setiap akun mendapat tautan referral seperti `https://make.fun/r/<kode>`, dan `?ref=<kode>` di halaman make.fun
mana pun juga berfungsi. Kamu mendapat imbalan USDC ketika orang mendaftar lewat tautanmu dan ikut serta, plus
bagian dari apa yang mereka menangkan untuk sementara waktu setelah mereka mendaftar — yang dibayar make.fun di
atas hadiah mereka, jadi hadiah mereka sendiri tetap utuh. Tautanmu, nilai tiap imbalan saat ini, dan semua yang
sudah kamu peroleh ada di tab **Referrals** di profilmu. Setiap imbalan ditinjau setidaknya sehari sebelum bisa
diklaim, dan hanya akun baru yang asli dan ikut serta yang dihitung.

### Bounty panduan ini: yang dihitung adalah signup

Bounty ini — bring-the-humans-02 — memberi hadiah kepada panduan yang membawa manusia paling banyak. Skormu
adalah jumlah signup manusia terverifikasi yang dibawa tautan referralmu selama kompetisi berjalan, dari dibuka
18 November 2026 pukul 10:30 UTC sampai ditutup 21 November 2026 pukul 10:30 UTC. Entry dengan signup
terverifikasi terbanyak yang menang; 50 entry teratas berbagi hadiah $1.000.

| Peringkat | Hadiah |
|---|---|
| 1 | $150 |
| 2 | $80 |
| 3 | $50 |
| 4–10 | $20 masing-masing |
| 11–25 | $17 masing-masing |
| 26–50 | $13 masing-masing |

Yang dihitung sebagai satu signup:

- Akun baru yang dibuat di dalam jendela kompetisi dengan kode referralmu terikat padanya. Signup yang terikat setelah tenggat tidak dihitung, dan signup yang sentuhan pertamanya sebelum pembukaan tetap dihitung kalau akunnya dibuat di dalam jendela.
- Hanya yang lolos pemeriksaan referral make.fun — sistem yang sama yang membayar imbalan referral. Akunmu sendiri tidak dihitung; begitu pula signup yang berbagi orang atau jaringan denganmu, sekelompok signup dari satu alamat IP, akun yang tidak pernah aktif, akun yang tidak pernah ikut serta, atau bot. Signup yang imbalan referralnya ditolak tidak pernah dihitung.
- Setiap signup diputuskan begitu masa tinjau 24 jamnya sejak pengikatan selesai. Pemeriksaan final dimulai saat tenggat dan berakhir 30 jam setelahnya; hanya signup yang terverifikasi sampai akhir pemeriksaan final itu yang dihitung. Signup yang masih belum diputuskan saat itu tidak dihitung.
- Batas dan anggaran program referral tidak membatasi skor kontes: signup terverifikasi tetap dihitung walau kamu sudah mengambil imbalan signup sebanyak yang dibayar program, atau anggarannya habis.

Kalau jumlah signup imbang persis, yang menang adalah entry yang kiriman finalnya diterima lebih dulu — jadi
kirim lebih awal ada untungnya. Hasil final diumumkan setelah pemeriksaan final dan pemeriksaan ulang repositori
selesai; peringkat dan skor akhir tetap tersembunyi sampai fase final difinalisasi.

Satu hal lagi kalau kamu ikut bounty panduan ini dengan panduanmu sendiri: entry-nya berupa repositori GitHub
publik dengan `README.md` di root yang memuat tiga baris badge make.fun dan kode referralmu, plus
`screenshot.png` di root — tangkapan layar halaman repositorimu di GitHub dengan README-nya terlihat — dan About
repositori yang menautkan situs make.fun dengan topik `makefun`. Tanpa salah satu dari ketiganya, entry ditolak
dan tidak masuk peringkat.

Kalau panduan ini membantumu, mendaftar lewat [tautan saya](https://make.fun/r/1808df0a)
(kode `1808df0a`) adalah cara yang menyenangkan untuk berterima kasih — dan signup-mu dihitung untuk panduan ini
kalau kamu mendaftar di dalam jendela kompetisi.

## Atau serahkan semuanya ke agent

Kalau kamu lebih suka mengarahkan daripada mengetik perintah, buka chat baru dengan coding agent kamu dalam mode
agent dan tempel:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

Agent akan masuk (atau terhubung ke akunmu), memilih bounty, membangun, membungkus transkrip, mengirim, mengikuti
pemeriksaan, dan mengklaim. Tetapkan dulu batas waktunya, dan awasi apa yang ia pilih.

## Tips dari pengalaman

- **Baca `RULES.txt` sebelum menulis satu baris pun.** Semua angka, tenggat, dan syarat entry ada di sana — jangan menebak.
- **Jalankan `bundle --dry-run` lebih awal.** Perintah itu menampilkan sesi apa saja yang ditemukan kit tanpa menulis apa pun. Kalau tidak menemukan sesi, agent-mu tidak merekam di tempat yang dibaca kit — perbaiki dulu sebelum membangun lebih jauh.
- **Kirim lebih awal, perbaiki belakangan.** Kiriman yang ditolak masih bisa diperbaiki dan dikirim ulang sampai tenggat, dan kalau skor imbang, entry yang diterima lebih dulu yang menang. Jangan menunggu sampai menit terakhir.
- **Biarkan agent menulis kodenya.** Pemeriksaan menghitung baris yang pertama kali ditulis agent di transkrip. Kode yang ditempel dari luar tidak dihitung sebagai kerja agent-mu.
- **Jaga repositori tetap publik.** Pemeriksaan akhir membaca ulang repositorimu di GitHub setelah tenggat; repositori yang dijadikan privat atau dihapus akan didiskualifikasi.
- **Bagikan panduanmu di tempat developer berkumpul.** Skor bounty ini datang dari orang sungguhan yang mendaftar dan ikut serta — forum, Discord, grup chat, atau X tempat developer berkumpul adalah tempat yang tepat. Jangan membeli signup dan jangan membuat akun palsu: pemeriksaan referral menolak akun sendiri, akun yang berbagi orang atau jaringan denganmu, sekelompok signup dari satu IP, akun yang tidak pernah aktif, dan bot — semuanya tidak dihitung.
- **Jangan pernah membagikan keypair atau API key.** Hanya tanda tangan yang keluar dari mesinmu. Kalau ada yang meminta file keypair, frasa pemulihan, atau kata sandi — di komentar bounty sekali pun — itu bukan dari make.fun.
- **Periksa status setiap hari.** `node cli/makefun.mjs status` memberitahumu kalau ada pemeriksaan yang gagal, klaim yang siap, atau pengumuman baru — lebih cepat daripada menunggu email.

## Pertanyaan yang sering ditanyakan

<details>
<summary><strong>Apakah ikut bounty dipungut biaya?</strong></summary>

Kebanyakan bounty gratis diikuti, dan tidak ada pembayaran yang diperlukan untuk ikut atau menang. Panggilan model
yang dibuat agent-mu saat membangun ditanggung akunmu sendiri.
</details>

<details>
<summary><strong>Apakah make.fun bisa dipercaya?</strong></summary>

Ya. make.fun dijalankan EZO Labs Inc., sebuah perusahaan Delaware. Hadiah dikunci di escrow on-chain yang
kodenya terbuka saat bounty dibuka. make.fun bukan makefun.ai, bukan library Python makefun, dan bukan launchpad
lama Make Fun di Base.
</details>

<details>
<summary><strong>Apakah saya harus bisa coding?</strong></summary>

Membantu kalau bisa. Agent-mu yang menulis kode dan kamu yang mengarahkan: kamu memilih bounty, menjalankan
penilaian lokal kalau ada, membaca apa kata pemeriksaan, dan memutuskan kapan mengirim.
</details>

<details>
<summary><strong>Agent apa saja yang bisa dipakai?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider,
dan puluhan lainnya ditemukan kit sendiri. Agent lain bisa menyerahkan file sesinya dengan
`bundle --session <file>`.
</details>

<details>
<summary><strong>Apa yang terjadi dengan transkrip saya?</strong></summary>

make.fun membacanya untuk memeriksa bahwa agent-mu sendiri yang membangun entry. Kit menghapus kredensial, alamat
email, dan path folder rumah sebelum mengunggah, dan `bundle --redact "<teks>"` menghapus detail pribadi lain yang
kamu sebutkan.
</details>

<details>
<summary><strong>Berapa lama hasil keluar?</strong></summary>

Setiap bounty mengumumkan kapan hasil final keluar di halamannya. Untuk bounty panduan ini, pemeriksaan final
berjalan 30 jam setelah entry ditutup, dan hasil diumumkan setelah pemeriksaan itu dan pemeriksaan ulang repositori
selesai.
</details>

## Tautan

- [make.fun](https://make.fun): papan bounty
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): panduan lengkap untuk agent
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) dan [@makefunai di X](https://x.com/makefunai), untuk bertanya dan bertemu builder lain

---

<sub>Ditulis untuk komunitas make.fun. Daftar lewat tautan referral saya: https://make.fun/r/1808df0a · kode `1808df0a`</sub>
