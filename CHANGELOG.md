# Changelog

All notable changes to the **EventCaps** project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [1.0.0] - 2026-09-09

### Added
- **Dedicated TV Slideshow Tab**: Launched TV Slideshow in a new browser tab (`_blank`) with fullscreen presentation mode, allowing hosts to keep their moderation dashboard and active session open without interruptions or logouts.
- **Supabase Cloud Storage Integration**:
  - Direct-to-cloud photo uploads from attendee mobile devices directly to Supabase Storage buckets.
  - Global edge CDN delivery for live memories walls and big-screen TV presentations.
  - Built-in `🧪 Test Connection` utility in the host storage modal to verify bucket connectivity.
  - Environment-based secure credential management for project endpoints, API keys, and storage buckets.
- **Real-Time Moderation Queue**:
  - Live incoming capture queue displaying thumbnail previews, guest attribution, and timestamps.
  - 1-Click **Auto-Approve** toggle (`⚡ Auto-Approve: ON` / `🛡️ Auto-Approve: OFF`) with prompt to approve all pending items upon activation.
  - Individual and bulk `Approve` / `Reject` actions.
  - `↩️ Revert to Pending` and `🗑️ Delete` actions synchronized instantly across all screens.
- **Frictionless Smartphone Guest Experience**:
  - Instant joining via dynamic QR code scanning (zero app downloads required).
  - Client-side image processing engine: automatic resizing (2048px), lightweight thumbnail generation (360px), EXIF camera orientation correction, and GPS coordinate stripping for attendee privacy.
  - Real-time batch upload widget with animated progress bar, percentage tracker, and sequential counters (`Uploading Photos 2 of 5`).
  - Real-time Live Memories Wall with personal "My Shared Photos" feed and upload quota indicators.
- **Host Security & Profile Controls**:
  - SHA-256 hashed Admin PIN authentication and session management.
  - Profile customization modal to update Host Display Name, Role, and Admin PIN directly from the header.
- **Real-Time Analytics Dashboard**:
  - Live KPI cards: Total Uploads, Approved Photos, Active Attendees, and Disk Footprint (MB).
  - Ranked Leaderboard recognizing top contributing attendees.
  - Hourly activity timeline bar graph displaying photo submissions chronologically.
- **Presentation & TV Slideshow Mode**:
  - Fullscreen carousel presentation view (`F` to toggle fullscreen, `Space` to pause/resume, arrow keys to navigate).
  - Configurable slide intervals (3s, 5s, 10s), transition effects (fade, slide, zoom), and photographer credit overlays.
  - Live corner QR code watermark for late attendees.
- **Data Export & Cloud Backup**:
  - In-memory instant `.zip` full-album exporter using `JSZip`.
  - 1-Click Google Drive integration for direct cloud backup into organized folder hierarchies.
- **Offline PWA Support**:
  - Service worker with network-first caching and offline photo queueing.
  - Dedicated Privacy Policy (`#/privacy`) and Terms of Service (`#/terms`) pages.
- **CI/CD & Deployment**:
  - Automated GitHub Actions deployment pipeline targeting GitHub Pages (`https://deidi.github.io/event-caps/#/`).

### Changed
- Streamlined settings modal to hide project secrets and storage bucket names from the host UI.
- Upgraded frontend framework to Svelte 5 and Vite 6 with pure client-side reactive state runes (`$state`).
- Modernized architecture from peer-to-peer WebRTC mesh to high-reliability MQTT WebSockets signaling and Supabase CDN delivery.

### Fixed
- Resolved black placeholder image rendering by utilizing native browser decoding and CDN URL fallbacks.
- Fixed photo deletion synchronization to immediately remove retracted or deleted captures from all connected live walls and slideshows.
- Fixed retained gallery synchronization ensuring newly joined attendees instantly load the complete historical approved gallery.

---

[1.0.0]: https://github.com/deidi/event-caps/releases/tag/v1.0.0
