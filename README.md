# 📸 EventCaps — Zero-Backend Real-Time Event Photo Hub

[![Release](https://img.shields.io/github/v/release/deidi/event-caps?color=blue&label=Release)](https://github.com/deidi/event-caps/releases/tag/v1.0.0)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![Frontend](https://img.shields.io/badge/Frontend-Svelte%205%20%2B%20Vite%206-orange)](https://svelte.dev/)
[![Storage](https://img.shields.io/badge/Storage-Supabase%20Cloud%20CDN-3ECF8E?logo=supabase)](https://supabase.com/)
[![PWA](https://img.shields.io/badge/PWA-Offline%20Ready-blueviolet)](https://web.dev/progressive-web-apps/)
[![Status](https://img.shields.io/badge/Deploy-GitHub%20Pages-success?logo=github)](https://deidi.github.io/event-caps/#/)

> **EventCaps** is a zero-backend, cloud-first real-time event photo sharing platform. Built entirely in modern web standards as a client-side Single Page Application (SPA) powered by managed BaaS (Supabase Cloud Storage), EventCaps requires **no custom server infrastructure to build or maintain**, incurs **zero dedicated hosting fees**, and delivers **direct-to-cloud photo uploads & global CDN delivery**, sub-second **real-time moderation**, and high-impact **live TV presentation slideshows** for 100+ attendees.

---

## 🚀 Live Demo & Quick Links

- **🌐 Live Production Web App**: [https://deidi.github.io/event-caps/#/](https://deidi.github.io/event-caps/#/)
- **📦 Official v1.0.0 Release**: [GitHub Release Notes](https://github.com/deidi/event-caps/releases/tag/v1.0.0)
- **📝 Project Changelog**: [CHANGELOG.md](CHANGELOG.md)

---

## 🌟 Key Features

### ⚡ 1. Zero-Backend & Pure Client SPA Architecture
- **Zero Custom Backend Maintenance**: Runs entirely inside host and guest web browsers without building, managing, or paying for custom backend servers (no Node.js/Express, Python, or Docker containers). All storage and media delivery are offloaded directly to managed Supabase Cloud Storage.
- **Static Cloud Deployment**: Optimized for GitHub Pages, Cloudflare Pages, Vercel, or Netlify with built-in SPA 404 fallback routing.

### ☁️ 2. Direct-to-Cloud Supabase Storage & CDN
- **Direct Mobile Uploads**: Smartphone captures bypass host bandwidth limits by streaming directly from guest mobile devices into Supabase Storage buckets.
- **Global Edge CDN**: Instant sub-second photo delivery to live moderation queues, attendee walls, and big-screen TV slideshows.
- **Environment-Secured Credentials**: Supabase project endpoint, API keys, and bucket names (`eventcaps-photos`) are securely managed via environment variables and settings.

### 📺 3. Independent Multi-Tab TV Slideshow (`_blank`)
- **Preserved Host Sessions**: Launching the TV Slideshow opens in a separate browser tab, allowing the host's moderation dashboard to stay active and logged in on their laptop while presenting on a secondary TV/projector.
- **Real-Time Presentation Stream**: Loops approved photos and immediately injects incoming approved captures without requiring page reloads.
- **Presentation Shortcuts**: `F` (Fullscreen), `Space` (Pause/Resume carousel), and `←`/`→` (Manual slide navigation).
- **Customizable Overlays**: Configurable transition intervals (`3s`, `5s`, `10s`), animation effects (`fade`, `slide`, `zoom`), photographer credit badges, and live corner QR code watermark for late arrivals.

### 🛡️ 4. Real-Time Moderation Queue & 1-Click Auto-Approve
- **Instant Photo Review**: Moderation feed with thumbnail previews, guest attribution, and upload timestamps.
- **1-Click Auto-Approve Toggle**: Switch seamlessly between **`⚡ Auto-Approve: ON`** (hands-free live stream) and **`🛡️ Auto-Approve: OFF`** (manual review mode) with one-click approval of pending batches.
- **Reversible Moderation**: Revert approved photos back to pending or permanently delete them with real-time removal across all connected screens.

### 📱 5. Frictionless Guest Smartphone Experience
- **Zero App Downloads**: Guests simply scan a dynamic QR code from any standard camera app to join in seconds.
- **In-Browser Image Engine**: Automatic client-side resizing (2048px), thumbnail generation (360px), EXIF orientation correction, and GPS coordinate stripping via HTML5 Canvas and `exifr`.
- **Live Upload Feedback**: Animated progress bar, sequential photo counters (`Uploading Photos 2 of 5`), and delivery confirmation.

### 📊 6. Real-Time Analytics Dashboard
- **Live Metrics**: Total photo submissions, approved count, active attendee count, and disk storage utilized (MB).
- **🏆 Contributor Leaderboard**: Ranked table recognizing top guest photographers.
- **⏱️ Activity Timeline**: Scaled chronological bar chart showing submission peaks throughout the gathering.

### 📦 7. Data Ownership, Backup & Export
- **In-Memory ZIP Exporter**: Download the complete event album with original photos and `metadata.json` in under 2 seconds using `JSZip`.
- **Google Drive Cloud Backup**: 1-Click Google OAuth integration to back up event media directly into organized `/EventCaps Events/<Event Name>/` folder hierarchies.
- **Offline PWA Resilience**: Service Worker with network-first caching and IndexedDB offline queues ensuring photos taken during intermittent connectivity are not lost.

---

## 🏗️ System Architecture

```
                                 ┌──────────────────────────────────────────────┐
                                 │     📱 Guest Smartphones (100+ Attendees)    │
                                 │  - Zero App Install: Instant QR Code Scan    │
                                 │  - In-Browser Resize (2048px) & EXIF Strip   │
                                 │  - Live Memories Wall & Upload Progress      │
                                 └──────┬───────────────────────────────▲───────┘
                                        │                               │
                1. Signaling & Approval │                               │ 3. Approved Media Stream
                    (MQTT / WebSockets) │                               │    (Supabase CDN / Web)
                                        ▼                               │
┌─────────────────────────────────────────────────────────┐             │
│              💻 Host Dashboard (Browser SPA)            │             │
│  - Event Spaces, SHA-256 PIN Security & Host Profile    │             │
│  - Real-Time Moderation Queue (Auto-Approve Toggle)     ├─────────────┼────────────────────────┐
│  - Local DB (IndexedDB) & Supabase Storage Manager      │             │                        │
└───────────────────────────┬─────────────────────────────┘             │                        │
                            │                                           │                        │
                            │ 2. Direct-to-Cloud Uploads                │                        │
                            ▼                                           ▼                        ▼
              ┌───────────────────────────┐               ┌──────────────────────────┐ ┌───────────────────┐
              │ ⚡ Supabase Cloud Storage │               │ 📺 TV / Projector Screen │ │ ☁️ Google Drive   │
              │  - Global Edge Photo CDN  │               │ - Dedicated New Tab View │ │    & ZIP Archive  │
              │  - Bucket: eventcaps-photos               │ - Fullscreen Presentation│ │ - In-Memory Export│
              └───────────────────────────┘               └──────────────────────────┘ └───────────────────┘
```

---

## 🛠️ Technology Stack

| Layer | Technologies / Libraries | Purpose |
| :--- | :--- | :--- |
| **Frontend Framework** | [Svelte 5](https://svelte.dev/) | High-performance reactive UI with modern runes (`$state`) |
| **Build Tool & Bundler** | [Vite 6](https://vitejs.dev/) | Fast HMR dev server and optimized production bundling |
| **Cloud Storage** | [@supabase/supabase-js](https://supabase.com/) | Direct client-to-cloud photo uploads and global CDN delivery |
| **Client Database** | [Dexie.js](https://dexie.org/) | Offline-first IndexedDB storage for events, photos, and host settings |
| **Real-Time Signaling** | [MQTT.js](https://github.com/mqttjs/MQTT.js) | Sub-second WebSocket messaging for cross-device synchronization |
| **Image Processing** | `HTML5 OffscreenCanvas` + [exifr](https://github.com/MikeKovarik/exifr) | In-browser resizing, thumbnail generation, and EXIF privacy stripping |
| **QR Code Engine** | [qrcode](https://github.com/soldair/node-qrcode) | Dynamic in-browser generation of event join QR codes |
| **Archive Exporter** | [JSZip](https://stuk.github.io/jszip/) | In-browser generation of full `.zip` albums and `metadata.json` |
| **PWA & Offline** | Service Worker (`sw.js`) + Web App Manifest | Native installability on mobile and network-first cache resilience |

---

## 📁 Repository Structure

```
event-caps/
├── .github/
│   └── workflows/
│       └── deploy.yml          # Automated GitHub Pages CI/CD workflow
├── client/                     # Frontend client application
│   ├── public/
│   │   ├── 404.html            # SPA fallback for deep links on GitHub Pages
│   │   ├── manifest.json       # PWA progressive web app configuration
│   │   ├── sw.js               # Network-first Service Worker
│   │   └── .nojekyll           # Disables Jekyll processing on GitHub Pages
│   ├── src/
│   │   ├── lib/
│   │   │   ├── api.js          # Unified API bridging DB, storage & realtime
│   │   │   ├── archive.js      # In-memory JSZip event archive creator
│   │   │   ├── db.js           # Dexie.js IndexedDB schema and operations
│   │   │   ├── gdrive.js       # Google Drive OAuth 2.0 integration
│   │   │   ├── offline-queue.js# Offline upload queue for unstable connections
│   │   │   ├── photo-engine.js # Client-side image resizer & EXIF orientation
│   │   │   ├── realtime.js     # MQTT over WebSockets live signaling
│   │   │   └── storage.js      # Supabase Cloud Storage client & CDN handlers
│   │   ├── App.svelte          # Main reactive SPA component
│   │   ├── app.css             # Design tokens, typography & animations
│   │   └── main.js             # Svelte 5 application entry point
│   ├── .env.example            # Environment variables template
│   ├── index.html              # HTML shell
│   ├── package.json            # Client dependencies & scripts
│   └── vite.config.js          # Vite config with relative base path ('./')
├── CHANGELOG.md                # Release history and version tracking
├── README.md                   # Comprehensive project documentation
└── package.json                # Root convenience scripts (npm run dev/build)
```

---

## 💻 Local Development Setup

### Prerequisites
- [Node.js](https://nodejs.org/) (v18 or higher recommended)
- [npm](https://www.npmjs.com/)

### 1. Clone the Repository
```bash
git clone https://github.com/deidi/event-caps.git
cd event-caps
```

### 2. Install Dependencies
```bash
# Install dependencies in client
npm --prefix client install
```

### 3. Environment Variables (Optional)
EventCaps has pre-configured production defaults. If you wish to use your own Supabase project:
```bash
cd client
cp .env.example .env
```
Edit `.env`:
```env
VITE_SUPABASE_URL=https://your-project-id.supabase.co
VITE_SUPABASE_ANON_KEY=your-supabase-anon-public-key
VITE_SUPABASE_BUCKET=eventcaps-photos
```

### 4. Run Development Server
```bash
# From root
npm run dev

# Or directly in client directory
cd client
npm run dev
```
Open `http://localhost:5173` in your browser.

### 5. Build for Production
```bash
# From root
npm run build

# Preview production build locally
npm run preview
```
The compiled static assets are generated in `client/dist/`.

---

## 📖 Event Day Runbook

### For Hosts & Event Organizers

1. **Initial Setup**:
   - Open **[https://deidi.github.io/event-caps/#/](https://deidi.github.io/event-caps/#/)**.
   - Create your **Host Display Name** and **4-Digit Admin PIN** on first setup.
   - Verify cloud storage status via the **`⚡ Supabase Cloud Storage: Active`** indicator.
2. **Create the Event**:
   - Click **`+ Create New Event`**.
   - Enter the Event Name, Date, Tagline, and per-guest upload limits.
   - Choose moderation preference: Enable manual moderation or toggle Auto-Approve.
3. **Display & Share QR Code**:
   - Click **`📱 QR Code`** on the event card.
   - Use **`📺 Full-Screen TV Mode`** to project the join QR code at venue entrances, or **`💾 Download PNG`** to print on table cards.
4. **Launch TV Slideshow**:
   - Click **`📺 Launch TV Slideshow`** — it opens in a separate browser tab (`_blank`).
   - Drag this tab to your venue TV screen or projector and press **`F`** for fullscreen.
   - Your host dashboard remains intact on your laptop for real-time moderation!
5. **Moderate & Export**:
   - Approve, reject, or auto-approve photos in real time.
   - After the event, click **`📦 Export Full Archive`** to download all original photos and metadata in a single `.zip` file.

### For Attendees & Guests

1. **Join**:
   - Scan the event QR code with any smartphone camera.
   - Type your name (e.g. `Emma`) and tap **Join Event**.
2. **Capture & Upload**:
   - Tap **📸 Camera** to capture live photos or **🖼️ Camera Roll** to select existing ones.
   - Watch the upload progress bar and delivery feedback.
3. **Live Memories**:
   - View approved memories on the live event stream in real time.
   - Delete any of your own photos at any time to free up quota.

---

## 🌐 Deploying to GitHub Pages

EventCaps includes an automated GitHub Actions workflow in `.github/workflows/deploy.yml`:

1. **Enable GitHub Pages**:
   - Go to your repository on GitHub: **Settings → Pages**.
   - Under **Build and deployment → Source**, select **GitHub Actions**.
2. **Push Changes**:
   - Every push to the `main` branch triggers an automated build and deployment.
   - The workflow compiles the Svelte 5 SPA, generates `404.html` for SPA hash routing, and publishes to GitHub Pages.

---

## 📄 License & Credits

Developed with ❤️ by **deidi** and the Open Source Community.  
Released under the **[MIT License](LICENSE)**.
