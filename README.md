# 💜 Ellie Dashboard

Mobile-first dashboard untuk monitoring OpenClaw agent. Desain dalam Bahasa Indonesia, optimized untukHP, dan gampang dibaca.

![Dashboard Preview](docs/preview.png)

## ✨ Fitur

| Fitur | Deskripsi |
|-------|-----------|
| 🏠 **Beranda** | Overview agent aktif, pengeluaran harian, kesehatan sistem |
| 💬 **Sesi** | Lihat semua agent sessions (aktif/off) |
| ⏰ **Cron** | Kelola cron jobs dengan toggle on/off |
| 📋 **Log** | System logs real-time dengan color-coded errors |
| 📁 **File** | Browse workspace files |
| 📊 **Biaya** | Statistik token usage (hari/minggu/bulan) |
| ⚙️ **Setelan** | Pengaturan dashboard |

## 🚀 Quick Start

### Prerequisites

- Node.js v18+
- OpenClaw (optional, untuk fitur lengkap)
- Cloudflare account (untuk tunnel)

### Installation

```bash
# Clone repo
git clone https://github.com/mail-eth/ellie-dashboard.git
cd ellie-dashboard

# Install dependencies (jika ada)
npm install

# Start dashboard
node server-simple.js
```

### Akses

Buka browser ke: `http://localhost:7001`

## 🌐 Deployment dengan Cloudflare Tunnel

### 为什么 pakai Cloudflare Tunnel?

- ✅ Gratis
- ✅ Permanent URL (tidak expire)
- ✅ SSL otomatis
- ✅ Tidak perlu buka port

### Setup

1. **Buat Cloudflare Zero Trust account** (gratis)
2. **Create tunnel baru**:
   - Pergi ke https://dash.cloudflare.com/networks/tunnels
   - Klik "Create a tunnel"
   - Pilih "Cloudflared"
   - Beri nama: `ellie-dashboard`
   - Copy token yang diberikan

3. **Konfigurasi DNS**:
   - Add public hostname: `dashboard.tedomain.com` atau `elliedash.trycloudflare.com`
   - Service: `http://localhost:7001`

4. **Jalankan tunnel**:
   ```bash
   # Jalankan langsung
   cloudflared tunnel run --token <YOUR_TOKEN>
   
   # Atau install sebagai service (auto-startup)
   sudo cloudflared service install <YOUR_TOKEN>
   ```

5. **Akses**:
   ```
   https://elliedash.trycloudflare.com
   ```

## ⚙️ Konfigurasi

### Environment Variables (Optional)

Buat file `dashboard.env` di root folder:

```env
# Port untuk dashboard (default: 7001)
PORT=7001

# OpenClaw workspace path (default: /root/.openclaw)
WORKSPACE_DIR=/root/.openclaw

# Refresh interval dalam ms (default: 30000 = 30 detik)
REFRESH_INTERVAL=30000
```

### API Endpoints

| Endpoint | Method | Deskripsi |
|----------|--------|-----------|
| `/api/system/stats` | GET | CPU, RAM, Disk, Uptime |
| `/api/sessions` | GET | List agent sessions |
| `/api/crons` | GET | List cron jobs |
| `/api/logs` | GET | System logs |
| `/api/files` | GET | Workspace files |
| `/api/costs` | GET | Token usage & spending |
| `/api/backup` | POST | Trigger backup |
| `/api/restart` | POST | Restart gateway |

## 📱 Mobile-First Design

Dashboard ini dirancang khusus untuk mobile:

- **Portrait orientation** - Layout vertical yang gampang di-scroll
- **Touch-friendly** - Button minimal 44x44px
- **Dark mode** - Mudah dilihat di kondisi cahaya minim
- **Bahasa Indonesia** - Semua label dalam Bahasa Indonesia

## 🔧 Development

### Struktur Project

```
ellie-dashboard/
├── server-simple.js    # Node.js server + API routes
├── dashboard-mobile.html # Frontend (HTML/CSS/JS)
├── .gitignore         # Git ignore rules
├── README.md          # Dokumentasi
└── docs/              # Preview images
```

### Customization

#### Mengganti Nama/Emoji

Edit `dashboard-mobile.html`:

```javascript
// Ganti header
<h1>💜 Ellie Dashboard</h1>

// Ganti greeting
<span>Terhubung</span>
```

#### Menambah Fitur Baru

1. Tambah API endpoint di `server-simple.js`:
```javascript
if (url.pathname === '/api/new-feature') {
  res.writeHead(200, { 'Content-Type': 'application/json' });
  res.end(JSON.stringify({ data: 'value' }));
  return;
}
```

2. Tambah UI di `dashboard-mobile.html`:
```html
<div class="action-btn" onclick="doAction('new-feature')">
  <div class="action-icon">✨</div>
  <div class="action-label">Fitur Baru</div>
</div>
```

## 🛡️ Security

- ❌ Tidak menyimpan credentials di repo
- ✅ .env files di-gitignore
- ✅ Sensitive data (API keys) tidak di-commit
- ✅ Cloudflare tunnel menggunakan HTTPS

## 📝 Lisensi

MIT License - Bebas digunakan dan dimodifikasi.

## 🤝 Kontribusi

1. Fork repo
2. Buat feature branch (`git checkout -b fitur-baru`)
3. Commit (`git commit -m 'Menambah fitur baru'`)
4. Push (`git push origin fitur-baru`)
5. Buat Pull Request

---

💜 Dibuat dengan love oleh Ellie AI Assistant
