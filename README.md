Saya akan buatkan **README.md** yang lengkap untuk bot Discord Lexy kamu, mencakup semua variabel, sintaks, tabel type status, rotasi status, dan panduan lengkap. ASCII art

---

# 📘 **README.md - Discord Bot Lexy**

```markdown
# 🤖 Lexy Discord Bot

Bot Discord lengkap dengan fitur moderasi, anti-spam soundboard, auto-response, dan berbagai command interaktif.

## 📋 Daftar Isi
- [Fitur Utama](#-fitur-utama)
- [Persyaratan](#-persyaratan)
- [Instalasi](#-instalasi)
- [Konfigurasi Variabel](#-konfigurasi-variabel)
- [Prefix & Command](#-prefix--command)
- [Status Bot (Presence)](#-status-bot-presence)
- [Rotasi Status Otomatis](#-rotasi-status-otomatis)
- [Permission yang Dibutuhkan](#-permission-yang-dibutuhkan)
- [Struktur Folder](#-struktur-folder)
- [Cara Menjalankan](#-cara-menjalankan)
- [Troubleshooting](#-troubleshooting)

---

## 🎯 Fitur Utama

| Fitur | Deskripsi |
|-------|-----------|
| ✅ Anti-Spam Soundboard | Timeout 1 menit jika 3x soundboard dalam 5 detik |
| ✅ Sambutan Member Baru | Auto-role "Member" + pesan selamat datang |
| ✅ Log Pesan | Mencatat pesan yang dihapus ke channel #log |
| ✅ Moderasi | Kick, Ban, Clear, Slowmode, Timeout |
| ✅ Informasi | Userinfo, Serverinfo, Avatar, Membercount |
| ✅ Utility | Say, Embed, Poll (dapat ditambahkan) |
| ✅ Fun Commands | 8ball, Roll, Quote, Meme (dapat ditambahkan) |

---

## 📦 Persyaratan

- Node.js **v16.9.0** atau lebih tinggi
- NPM (biasanya sudah termasuk Node.js)
- Discord Bot Token ([Dapatkan di sini](https://discord.com/developers/applications))

---

## 🚀 Instalasi

### 1. Clone atau Buat Folder Project
```bash
mkdir lexy-bot
cd lexy-bot
```

### 2. Inisialisasi NPM
```bash
npm init -y
```

### 3. Install Dependencies
```bash
npm install discord.js dotenv
```

### 4. Buat File `.env`
```env
TOKEN=masukkan_token_bot_anda_di_sini
```

### 5. Buat File `index.js`
Copy seluruh kode bot ke dalam file `index.js`

---

## ⚙️ Konfigurasi Variabel

### Variabel Dasar

| Variable | Tipe | Default | Deskripsi |
|----------|------|---------|-----------|
| `PREFIX` | String | `'lyxy'` | Awalan command bot |
| `TOKEN` | String | (dari .env) | Token autentikasi bot |
| `soundboardHistory` | Map | `new Map()` | Menyimpan timestamp soundboard per user |

### Konstanta Waktu

| Variable | Nilai | Deskripsi |
|----------|-------|-----------|
| `SOUNDBOARD_WINDOW_MS` | `5000` | Jendela waktu deteksi spam (5 detik) |
| `SOUNDBOARD_LIMIT` | `3` | Batas maksimal soundboard dalam window |
| `TIMEOUT_DURATION_MS` | `60000` | Durasi timeout (1 menit) |
| `CLEANUP_INTERVAL_MS` | `60000` | Interval bersihkan history (1 menit) |

### Channel yang Digunakan

| Channel Name | Fungsi |
|--------------|--------|
| `#welcome` | Pesan selamat datang member baru |
| `#log` | Log pesan yang dihapus & aktivitas spam |
| `#rules` | (Opsional) Tempat aturan server |

### Role yang Digunakan

| Role Name | Fungsi |
|-----------|--------|
| `Member` | Diberikan otomatis ke member baru |

---

## 🔧 Prefix & Command

### Prefix: `lyxy`

| Command | Syntax | Contoh | Izin |
|---------|--------|--------|------|
| `ping` | `lyxy ping` | `lyxy ping` | Semua |
| `help` | `lyxy help` | `lyxy help` | Semua |
| `clear` | `lyxy clear <1-100>` | `lyxy clear 10` | Manage Messages |
| `userinfo` | `lyxy userinfo [@user]` | `lyxy userinfo @Lexy` | Semua |
| `serverinfo` | `lyxy serverinfo` | `lyxy serverinfo` | Semua |
| `kick` | `lyxy kick @user [alasan]` | `lyxy kick @spammer` | Kick Members |
| `ban` | `lyxy ban @user [alasan]` | `lyxy ban @spammer` | Ban Members |
| `say` | `lyxy say <pesan>` | `lyxy say Hello!` | Manage Messages |
| `embed` | `lyxy embed <judul> \| <deskripsi>` | `lyxy embed Info \| Hallo semua` | Manage Messages |
| `avatar` | `lyxy avatar [@user]` | `lyxy avatar @Lexy` | Semua |
| `membercount` | `lyxy membercount` | `lyxy membercount` | Semua |
| `slowmode` | `lyxy slowmode <detik>` | `lyxy slowmode 5` | Manage Channels |
| `soundboardstatus` | `lyxy soundboardstatus` | `lyxy soundboardstatus` | Administrator |

---

## 🎮 Status Bot (Presence)

### Syntax Dasar
```javascript
client.user.setPresence({
    activities: [{ name: 'teks', type: angka }],
    status: 'online'
});
```

### Tabel Type Status

| Type | Angka | Nama | Ikon | Contoh Tampilan |
|------|-------|------|------|-----------------|
| Playing | `0` | Playing | 🎮 | 🎮 **Playing** Minecraft |
| Streaming | `1` | Streaming | 🔴 | 🔴 **Streaming** on Twitch |
| Listening | `2` | Listening to | 🎧 | 🎧 **Listening to** Lofi Girl |
| Watching | `3` | Watching | 👁️ | 👁️ **Watching** Server Activity |
| Custom | `4` | Custom | 💬 | 💬 **Custom Status** |
| Competing | `5` | Competing in | 🏆 | 🏆 **Competing in** Valorant |

### Tabel Status Online

| Status | Kode | Warna | Ikon |
|--------|------|-------|------|
| Online | `'online'` | Hijau | 🟢 |
| Idle | `'idle'` | Kuning | 🟠 |
| Do Not Disturb | `'dnd'` | Merah | 🔴 |
| Invisible | `'invisible'` | Abu-abu | ⚫ |

### Contoh Implementasi

```javascript
// Listening to (🎧)
client.user.setPresence({
    activities: [{ name: 'lyxy help', type: 2 }],
    status: 'online'
});

// Watching (👁️)
client.user.setPresence({
    activities: [{ name: 'Server Lexy', type: 3 }],
    status: 'online'
});

// Playing (🎮)
client.user.setPresence({
    activities: [{ name: 'with code', type: 0 }],
    status: 'online'
});

// Competing (🏆)
client.user.setPresence({
    activities: [{ name: 'Best Bot', type: 5 }],
    status: 'online'
});
```

---

## 🔄 Rotasi Status Otomatis

### Kode Rotasi Sederhana
```javascript
// Daftar status yang akan dirotasi
const statusList = [
    { name: 'lyxy help', type: 2 },      // Listening to
    { name: 'Server Lexy', type: 3 },    // Watching
    { name: 'with code', type: 0 },      // Playing
    { name: 'Anti Spam Aktif', type: 2 }, // Listening to
    { name: `${PREFIX}help`, type: 2 }    // Listening to
];

let index = 0;
setInterval(() => {
    client.user.setPresence({
        activities: [statusList[index]],
        status: 'online'
    });
    index = (index + 1) % statusList.length;
}, 30000); // Ganti setiap 30 detik
```

### Rotasi dengan Waktu Berbeda per Status
```javascript
const statusList = [
    { name: 'lyxy help', type: 2, duration: 20000 },     // 20 detik
    { name: 'Server Aktif', type: 3, duration: 15000 },  // 15 detik
    { name: 'Anti Spam ON', type: 2, duration: 10000 }   // 10 detik
];

let index = 0;
function rotateStatus() {
    const current = statusList[index];
    client.user.setPresence({
        activities: [{ name: current.name, type: current.type }],
        status: 'online'
    });
    index = (index + 1) % statusList.length;
    setTimeout(rotateStatus, current.duration);
}
rotateStatus();
```

### Rotasi dengan Status Online Berbeda
```javascript
const statusList = [
    { name: 'lyxy help', type: 2, status: 'online' },   // 🟢
    { name: 'Maintenance', type: 0, status: 'dnd' },    // 🔴
    { name: 'AFK Mode', type: 3, status: 'idle' }       // 🟠
];

let index = 0;
setInterval(() => {
    client.user.setPresence({
        activities: [{ name: statusList[index].name, type: statusList[index].type }],
        status: statusList[index].status
    });
    index = (index + 1) % statusList.length;
}, 30000);
```

---

## 🔑 Permission yang Dibutuhkan

### Permission Value: `268823630`

### Daftar Permission Lengkap

| Permission | Nilai | Kegunaan |
|------------|-------|----------|
| Kick Members | `2` | Command `kick` |
| Ban Members | `4` | Command `ban` |
| Manage Channels | `16` | Command `slowmode` |
| Add Reactions | `64` | Fitur reaction (poll) |
| Read Messages | `1024` | Membaca pesan |
| Send Messages | `2048` | Mengirim pesan |
| Embed Links | `16384` | Mengirim embed |
| Attach Files | `32768` | Mengirim file/gambar |
| Read Message History | `65536` | Log pesan dihapus |
| Manage Messages | `8192` | Command `clear` & log |
| Manage Roles | `268435456` | Auto-role member baru |
| Moderate Members | `68719476736` | **Timeout (anti-spam soundboard)** |

### Link Invite dengan Permission Lengkap
```
https://discord.com/api/oauth2/authorize?client_id=YOUR_CLIENT_ID&permissions=268823630&scope=bot
```
**Ganti `YOUR_CLIENT_ID` dengan ID bot Anda**

### Privileged Gateway Intents (Aktifkan di Developer Portal)

| Intent | Kode | Kegunaan |
|--------|------|----------|
| Server Members Intent | `1 << 0` | Deteksi member baru, userinfo |
| Message Content Intent | `1 << 1` | Membaca isi pesan (SEMUA COMMAND) |

**Cara aktivasi:**
1. Buka [Discord Developer Portal](https://discord.com/developers/applications)
2. Pilih aplikasi bot Anda
3. Klik tab **Bot**
4. Scroll ke **Privileged Gateway Intents**
5. ✅ Centang kedua intent di atas

---

## 📁 Struktur Folder

```
lexy-bot/
│
├── index.js          # Kode utama bot
├── .env              # Token bot (JANGAN DI-SHARE!)
├── package.json      # Dependencies
├── package-lock.json # Lock file
└── README.md         # Dokumentasi ini
```

---

## 🏃 Cara Menjalankan

### Development (Local)
```bash
node index.js
```

### Dengan Nodemon (Auto-restart saat ada perubahan)
```bash
npm install -g nodemon
nodemon index.js
```

### Production (dengan PM2)
```bash
npm install -g pm2
pm2 start index.js --name lexy-bot
pm2 save
pm2 startup
```

---

## ⚠️ Troubleshooting

### Error: `An invalid token was provided`
**Solusi:** Token di file `.env` salah atau expired. Reset token di Discord Developer Portal.

### Error: `Missing Access`
**Solusi:** Bot tidak memiliki permission yang cukup. Gunakan link invite dengan permission `268823630`.

### Error: `Privileged intent is disabled`
**Solusi:** Aktifkan `MESSAGE CONTENT INTENT` dan `SERVER MEMBERS INTENT` di Discord Developer Portal.

### Error: `Cannot find module 'discord.js'`
**Solusi:** Jalankan `npm install discord.js dotenv`

### Soundboard tidak terdeteksi
**Solusi:** 
- Pastikan bot punya permission `Read Messages` dan `Read Message History`
- Coba gunakan deteksi alternatif dengan menyesuaikan fungsi `isSoundboardMessage()`

### Bot tidak bisa timeout member
**Solusi:** 
- Pastikan bot punya permission `Moderate Members`
- Pastikan role bot lebih tinggi dari role target

---

## 📝 Variabel yang Dapat Disesuaikan

### Di bagian atas file `index.js`:

```javascript
// ========== KONFIGURASI YANG DAPAT DIUBAH ==========

const PREFIX = 'lyxy';              // Ganti prefix sesuai keinginan

// Konfigurasi Anti-Spam Soundboard
const SOUNDBOARD_WINDOW_MS = 5000;  // Window waktu deteksi (ms)
const SOUNDBOARD_LIMIT = 3;         // Batas maksimal dalam window
const TIMEOUT_DURATION_MS = 60000;  // Durasi timeout (ms)

// Channel & Role Names
const WELCOME_CHANNEL = 'welcome';  // Nama channel sambutan
const LOG_CHANNEL = 'log';          // Nama channel log
const DEFAULT_ROLE = 'Member';      // Nama role untuk member baru

// Status Bot
const BOT_STATUS = 'online';        // online, idle, dnd, invisible
const BOT_ACTIVITY_TYPE = 2;        // 0=Playing,1=Streaming,2=Listening,3=Watching,4=Custom,5=Competing
const BOT_ACTIVITY_NAME = 'lyxy help'; // Teks status
```

---

## 📞 Dukungan

Jika mengalami masalah atau ingin menambahkan fitur:
- **Discord Server:** [Link Invite Server]
- **Developer:** Lexy

---

## 📄 Lisensi

MIT License - Bebas digunakan dan dimodifikasi.

---

**Dibuat dengan ❤️ oleh Lexy**
```

---

## 💾 **CARA MENYIMPAN FILE README**

1. Di folder project bot kamu (`lexy-bot/`), buat file baru bernama `README.md`
2. Copy semua kode markdown di atas
3. Paste ke file `README.md`
4. Simpan (Ctrl + S)

---

## 📖 **FILE `README.md` MENCERMINKAN:**

| Section | Isi |
|---------|-----|
| Fitur Utama | Tabel semua fitur bot |
| Konfigurasi Variabel | Semua variabel yang bisa diubah |
| Tabel Type Status | Lengkap dengan angka dan contoh |
| Rotasi Status | 3 metode berbeda dengan kode contoh |
| Permission | Daftar lengkap + link invite |
| Troubleshooting | Solusi error umum |

---

Mau ditambahkan section lain? Misalnya:
- **Cara menambahkan command baru**
- **Contoh kode untuk fitur tambahan** (music, leveling, ticket system)
- **Cara hosting 24/7** (Railway, Render, VPS)

Beri tahu saya!
