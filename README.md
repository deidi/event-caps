# 📸 EventCaps — Serverless Real-Time Event Photo Hub

[![Release](https://img.shields.io/github/v/release/deidi/event-caps?color=blue&label=Release)](https://github.com/deidi/event-caps/releases/tag/v1.0.0)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![Frontend](https://img.shields.io/badge/Frontend-Svelte%205%20%2B%20Vite-orange)](https://svelte.dev/)
[![Storage](https://img.shields.io/badge/Cloud%20Storage-Supabase%20CDN-3ECF8E?logo=supabase)](https://supabase.com/)

> **EventCaps** is a 100% serverless, cloud-first event photo sharing hub. It runs **entirely in modern web browsers** with zero dedicated backend servers, zero database hosting costs, direct **Supabase Cloud Storage & CDN delivery**, real-time live moderation, multi-screen TV slideshows, and Google Drive cloud backup for 100+ attendees.

---

## 🌟 Key Features

- ⚡ **Zero Backend Servers**: Pure client-side Single Page Application (SPA) built with Svelte 5 and Vite — zero Node.js servers, Python backends, or local CLI processes needed during live events.
- 🌐 **Static Cloud Deployment**: Optimized for **GitHub Pages** (`https://deidi.github.io/event-caps/#/`) or any static hosting provider (Cloudflare Pages, Vercel, Netlify).
- ☁️ **Direct-to-Cloud Supabase Storage**: Guests upload high-resolution photos directly to Supabase Storage buckets with sub-second global CDN distribution.
- 📺 **Independent Multi-Tab TV Slideshow**: "Launch TV Slideshow" opens in a dedicated tab (`_blank`) with fullscreen presentation mode, custom transitions, and live QR watermark — ensuring the host dashboard and moderation queue stay active without interruption or session logout.
- 🛡️ **Real-Time Moderation Queue & 1-Click Auto-Approve**: Instant photo review with guest attribution, individual and bulk approve/reject actions, and a 1-click **Auto-Approve** toggle for hands-free live events.
- 📡 **Universal Real-Time Sync**: Instant photo streaming and status synchronization across host screens, guest phones, and TV walls via WebSockets and MQTT brokers.
- ☁️ **Google Drive Backup**: 1-click cloud sync into organized event folder hierarchies (`/EventCaps Events/<Event Name>/originals` and `/thumbnails`).
- 👤 **Host Security & PIN Authentication**: SHA-256 encrypted host PIN security, session tokens, and instant profile management.
- 📊 **Real-Time Analytics & Leaderboard**: Track total submissions, approved photos, active attendee counts, disk storage used (MB), top contributor rankings, and hourly activity timeline graphs.
- 🖼️ **Client-Side Image Optimization**: In-browser resizing (2048px), thumbnail generation (360px), EXIF orientation correction, and GPS coordinate stripping for privacy via HTML5 `OffscreenCanvas` and `exifr`.
- 📦 **In-Memory ZIP Exporter**: Instant download of complete event archives containing original photos and `metadata.json` in under 2 seconds via `JSZip`.
- 📴 **Offline PWA Resilience**: Full Service Worker and PWA manifest with offline queueing and `no-store` network-first updates.
- 📜 **Compliance & Privacy**: Built-in Privacy Policy (`#/privacy`) and Terms of Service (`#/terms`) pages.

---

## 🏗️ Architecture Overview

```
                                 ┌──────────────────────────────────────────────┐
                                 │     📱 Guest Smartphones (100+ Attendees)    │
                                 │  - Zero App Install: Instant QR Code Scan    │
                                 │  - In-Browser Resize (2048px) & EXIF Strip   │
                                 │  - Real-Time Live Memories Wall              │
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
              │  - High-Speed Photo CDN   │               │ - Dedicated New Tab View │ │    & ZIP Archive  │
              │  - Bucket: eventcaps-photos               │ - Fullscreen Presentation│ │ - In-Memory Export│
              └───────────────────────────┘               └──────────────────────────┘ └───────────────────┘
```

---

## 🚀 Live Demo & Getting Started

### 🌐 Access Live App
- **Live Host & Guest App**: [https://deidi.github.io/event-caps/#/](https://deidi.github.io/event-caps/#/)
- **Latest Release**: [EventCaps v1.0.0](https://github.com/deidi/event-caps/releases/tag/v1.0.0)

### 💻 Local Development Setup

```bash
# 1. Clone the repository
git clone https://github.com/deidi/event-caps.git
cd event-caps/client

# 2. Install dependencies
npm install

# 3. (Optional) Configure environment variables
# Copy .env.example or create .env with your Supabase credentials:
# VITE_SUPABASE_URL=https://your-project.supabase.co
# VITE_SUPABASE_ANON_KEY=your-anon-public-key
# VITE_SUPABASE_BUCKET=eventcaps-photos

# 4. Start local development server
npm run dev

# 5. Build for production
npm run build
```

---

## ➕ How to Create and Host an Event

Creating an event space takes less than 30 seconds:

1. **Access the Host Dashboard**:
   - Open **[https://deidi.github.io/event-caps/#/](https://deidi.github.io/event-caps/#/)**.
   - Set up your **Host Name & 4-Digit PIN** on initial launch (or enter your PIN to unlock).

2. **Click `+ Create New Event`**:
   - Click the primary **`+ Create New Event`** button on your dashboard.

3. **Configure Your Event Space**:
   - **Event Name**: E.g., `Annual Gala 2026`, `Emma & David's Wedding`, `Tech Conference`.
   - **Date**: Scheduled event date.
   - **Tagline / Message** *(Optional)*: Welcome message displayed on guest capture screens and the live slideshow.
   - **Per-Guest Upload Limit**: Limit uploads per attendee (e.g., `5`, `10`, `25`, or unlimited).
   - **Photo Moderation Queue**:
     - *Enabled (Recommended)*: Photos require host approval in the moderation queue before appearing on live screens.
     - *Disabled / Auto-Approve*: Photos appear on the live wall and TV slideshow immediately.
   - **Strip EXIF Metadata**: Automatically strips GPS coordinates and device metadata for attendee privacy.

4. **Launch & Display**:
   - In the event view, click **`📱 QR Code`** to show or print the event join code.
   - Click **`📺 Launch TV Slideshow`** to open the live presentation view in a separate tab or on a secondary display.

---

## 📱 How to Use During an Event

| Role / Device | URL Route | Instructions |
| :--- | :--- | :--- |
| **💻 Host Dashboard** | `https://deidi.github.io/event-caps/#/` | 1. Log in with your Admin PIN.<br>2. Click **`+ Create New Event`**.<br>3. Click **`📱 QR Code`** to project or print for guests.<br>4. Click **`📺 Launch TV Slideshow`** to open the presentation in a new tab.<br>5. Moderate guest uploads in real time or view **📊 Analytics**. |
| **📱 Guests (Smartphones)** | `https://deidi.github.io/event-caps/#/event/<slug>` | 1. Scan the host's QR code (no app download needed).<br>2. Enter their name (e.g. `Sarah`) and tap **Join Event**.<br>3. Snap photos with their phone camera or camera roll.<br>4. Watch approved photos appear on the **Live Memories Wall**! |
| **📺 TV / Projector Mode** | `https://deidi.github.io/event-caps/#/event/<slug>/slideshow` | 1. Opens in a separate browser tab.<br>2. Move to TV/projector screen and press **`F`** for fullscreen.<br>3. Real-time dynamic carousel streams photos automatically. |

---

## 📺 Live TV & Projector Slideshow Mode

The slideshow view is specifically crafted for big-screen presentation during live events:
- **Dedicated Tab Behavior**: Launched via `window.open(..., '_blank')` so the host's moderation dashboard and active session remain uninterrupted on their laptop.
- **Dynamic Stream**: Automatically loops approved photos and smoothly injects newly approved captures in real time.
- **Keyboard Controls**:
  - **`F`**: Toggle Fullscreen mode.
  - **`Space`**: Pause / Resume slide carousel.
  - **`←` / `→`**: Manually advance or revisit slides.
- **Customizable Presentation Settings**:
  - Slide interval speed (`3s`, `5s`, `10s`).
  - Transition animations (`fade`, `slide`, `zoom`).
  - Toggle photographer credit badge on/off.
  - Toggle live corner QR watermark so late attendees can join anytime.

---

## ☁️ Cloud Storage & Backup Architecture

### ⚡ Supabase Cloud Storage
- **Direct-to-Cloud Uploads**: Photos upload straight from attendee devices to your Supabase Storage bucket, avoiding host bandwidth bottlenecks.
- **High-Speed CDN Delivery**: Photos stream across global Edge CDNs for fast rendering on high-resolution TV displays and guest devices.
- **Secure Configuration**: Project URL, anon API key, and bucket name (`eventcaps-photos`) are securely managed via environment variables and settings.
- **Connection Test Tool**: Built-in `🧪 Test Connection` utility in the host settings modal to verify storage connectivity in one click.

### ☁️ Google Drive Cloud Backup
- **1-Click Google Authorization**: Connect your Google account to sync event albums directly into Google Drive folder structures.
- **Resumable Upload Sessions**: Robust background transfer with live progress tracking.

### 📦 In-Memory ZIP Archiver
- Export complete event archives (`.zip`) containing full-resolution original photos and `metadata.json` directly from the browser in seconds using `JSZip`.

---

## 🛡️ Real-Time Moderation Queue

- **Live Review Feed**: Real-time incoming queue displaying thumbnail previews, author names, and timestamps.
- **1-Click Moderation Actions**:
  - **`Approve`** / **`Reject`**: Moderate individual captures.
  - **`Approve All`** / **`Reject All`**: Handle high-traffic upload bursts in one click.
- **⚡ 1-Click Auto-Approve Toggle**:
  - Easily toggle between **`⚡ Auto-Approve: ON`** (hands-free live stream) and **`🛡️ Auto-Approve: OFF`** (strict curation).
  - Offers a quick prompt to instantly approve all currently waiting photos when toggled on.
- **Live Gallery Management**:
  - **`↩️ Revert to Pending`**: Instantly removes an already approved photo from live screens back into the moderation queue.
  - **`🗑️ Delete`**: Permanently purges a photo across host and all attendee screens.
  - **Full-Screen Lightbox**: High-res inspection with download capabilities.

---

## 📊 Analytics Dashboard

Click **📊 Analytics** inside any event to inspect real-time metrics:
- **Total Uploads**: Cumulative photo count received.
- **Approved & Live**: Count of photos actively displayed.
- **Active Guests**: Number of unique contributing attendees.
- **Disk Storage Used**: Total footprint of event photos in MB.
- **🏆 Top Guest Contributors**: Live leaderboard recognizing top attendee photographers.
- **⏱️ Activity Timeline by Hour**: Interactive bar chart displaying submission volume chronologically throughout the event.

---

## 📴 Offline PWA & Device Resilience

- **Offline Upload Queue**: Captures taken during intermittent connectivity are queued in local IndexedDB and automatically flush when connectivity resumes.
- **Mobile PWA Support**: Installable directly from mobile browser menus onto iOS and Android home screens.
- **Network-First Service Worker**: Uses `no-store` cache policies so hotfixes and app updates deploy instantly without stale browser caches.

---

## 📄 License & Credits

Developed with ❤️ by **deidi** and the Open Source Community.  
Released under the **[MIT License](LICENSE)**.
