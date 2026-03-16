# 📘 BMC Project Journal
### Bhatia Master Classes — Website & Platform

> **Maintained by:** Prabhakar (Solo Dev/Designer — current)
> **Last updated:** March 2026
> **Live URL:** https://prabhakarmdes12-cmyk.github.io/Bhatia-Master-Classes/
> **Client:** Bhatia Master Classes, Ujjain (JEE · NEET · Foundation Coaching)

---

## 🗂 Table of Contents

1. [Project Overview](#1-project-overview)
2. [Team & Department Guide](#2-team--department-guide)
3. [Tech Stack & Architecture](#3-tech-stack--architecture)
4. [File Structure & Page Map](#4-file-structure--page-map)
5. [Deployment & Hosting Guide](#5-deployment--hosting-guide)
6. [Current Progress & Changelog](#6-current-progress--changelog)
7. [Known Issues & Bugs](#7-known-issues--bugs)
8. [Roadmap — Upcoming Features](#8-roadmap--upcoming-features)
9. [Environment Variables & Secrets](#9-environment-variables--secrets)
10. [Design System Reference](#10-design-system-reference)

---

## 1. Project Overview

Bhatia Master Classes (BMC) is a JEE & NEET coaching institute based in Ujjain, Madhya Pradesh. This project is the institute's complete digital presence — a public-facing marketing website, a student portal, an admin dashboard, and a growing set of interactive tools.

**Core goals:**
- Establish BMC's online brand and drive student enquiries
- Provide enrolled students with a self-service portal (DPPs, tests, PYQs, notices)
- Generate leads through interactive engagement features (BMC Challenger, Crack These)
- Enable online teaching capabilities (live classes, doubt submission, video lectures)

**What the site currently does:**
- Full marketing site with 9 sections, responsive, SEO-tagged
- Student login portal (role-based: student / admin)
- Admin dashboard with leads tracking, student management, notices, uploads, fees
- BMC Challenger — weekly JEE question with OTP-gated solution + lead capture
- Crack These — 4 daily questions with solution modal + share cards
- DPP downloads (6 subjects), PYQ downloads (JEE Advanced 2023 packs)
- Video gallery section (3 reels, self-hosted MP4, 9:16 portrait)
- Doubt submission page with camera, file upload, canvas drawing, WhatsApp CTA
- Live Class page — YouTube live embed + Jitsi doubt sessions + countdown timer
- Branded share cards (Canvas-rendered), deep link sharing, social platform distribution
- Interactive login background — math symbol grid reacting to mouse movement

---

## 2. Team & Department Guide

> **If you're joining this project**, start here. Each department has its own section marked with a department tag throughout this document.

### 🎨 `[DESIGN]` — UI/UX Designer

**Your domain:** Visual design, component design, Figma files, brand consistency.

**Figma file:** `Bhatia_Master_Classes` — file key `r8vBpBQrqFQVEXbwAeKztP`
All major sections are named frames in Figma: Navigation, Hero, DPP, Test Series, PYQ, Admissions, Contact, Footer. The plugin **"HTML to Design"** was used to import the live site into Figma.

**Design system lives in:** `/10-design-system` in Figma (extracted component library)

**Key design decisions to preserve:**
- Color palette is defined in CSS variables — never hardcode hex values directly
- All new sections must use the dark navy (`#0F2245`) or light (`#F5F7FA`) alternating background pattern
- The accent gold (`#F4A825`) is used sparingly — only for CTAs, highlights, and active states
- Typography: `Barlow Condensed` for headings/display, `DM Sans` for body. No other fonts.
- Section structure: label pill → h2 title → divider bar → subtitle → content
- Cards always use `--radius-lg: 20px` and `--shadow-sm` at rest, `--shadow-md` on hover

**Workflow:** Design new section in Figma → share node link with developer → developer generates HTML

---

### 💻 `[FRONTEND]` — Frontend Developer

**Your domain:** HTML/CSS/JS, all `.html` files, component implementation, animations.

**No build system.** This is a pure static site — no React, no Webpack, no npm. Every page is a single `.html` file with all CSS and JS inlined. This is intentional for GitHub Pages compatibility.

**File naming convention:** All pages lowercase, hyphen-separated. e.g. `live-class.html`, `doubt.html`

**CSS convention:**
- All variables in `:root {}` at top of each file's `<style>` block
- Section-specific CSS grouped with a comment header: `/* ========== SECTION NAME ========== */`
- Never use `!important` unless overriding Bootstrap layout utilities
- Responsive breakpoints: `768px` (tablet), `991px` (nav collapse), `480px` (mobile)

**JS convention:**
- No frameworks. Vanilla JS only.
- All JS in a single `<script>` block at the bottom of `<body>`
- State that needs to persist across pages: use `localStorage`
- State that resets on tab close: use `sessionStorage`
- All modal IDs follow: `[section]Modal` — e.g. `challengerModal`, `solutionModal`
- All modal open functions: `openXModal()`, close: `closeModal('modalId')`

**Critical note on script order:** JS that queries DOM elements must be in a `<script>` block *after* the relevant HTML. `index.html` has two script blocks — the second one (after all modal HTML) is where modal-dependent JS lives. Do not move it.

---

### 🔧 `[BACKEND]` — Backend Developer *(Phase 2 — not yet active)*

**Your domain:** Server-side APIs, authentication, database, real-time features.

**This role doesn't exist yet.** The site is 100% static (Phase 1). When Phase 2 begins, the backend will handle:

- Real OTP delivery via Fast2SMS or MSG91 (Indian SMS gateway)
- Jitsi self-hosted on a DigitalOcean droplet (1-click installer available)
- Real user authentication replacing the hardcoded credentials in `login.html`
- Attendance tracking for live classes
- Student performance data storage
- Formspree replacement with a proper API endpoint

**Handoff checklist for Phase 2:**
- Replace `YOUR_FORM_ID` in `index.html` (admissions form) with real endpoint
- Replace `YOUR_DOUBT_FORM_ID` in `doubt.html` with real endpoint
- Replace hardcoded credentials in `login.html` CONFIG block with API calls
- Replace `CONFIG.isLive` flag in `live-class.html` with a database-driven status
- Replace `localStorage` lead storage in `admin.html` with a proper DB read

---

### 🚀 `[DEVOPS]` — Deployment & Infrastructure

**Your domain:** GitHub Pages, DNS, file management, performance, security.

**See Section 5 (Deployment Guide) for full details.**

**Quick facts:**
- Hosting: GitHub Pages (free tier)
- Repo: `https://github.com/prabhakarmdes12-cmyk/Bhatia-Master-Classes`
- Branch deployed: `main`
- Custom domain: Not yet configured (using GitHub subdomain)
- CI/CD: None (manual pushes to main trigger deployment)
- CDN: GitHub Pages has no CDN layer — static files served directly

**Phase 2 infrastructure needs:**
- DigitalOcean Droplet (₹800/month) for Jitsi + backend API
- TURN server for WebRTC NAT traversal
- SSL via Let's Encrypt (auto with DigitalOcean)
- Custom domain DNS configuration (currently on GoDaddy)

---

### ✍️ `[CONTENT]` — Content Editor

**Your domain:** Copy, SEO metadata, DPP/PYQ documents, notices, video scripts.

**Editable content locations:**

| Content | File | How to Update |
|---|---|---|
| Hero stats (3 batches, 90% success rate) | `index.html` line ~1037 | Edit `.stat-pill` values |
| Mentor bio | `index.html` line ~1116 | Edit `<p class="mentor-bio">` |
| DPP cards (title, description, download link) | `index.html` lines ~1235–1346 | Edit `.card-title`, `<p>`, `href` |
| PYQ cards | `index.html` lines ~1465–1598 | Edit card content |
| BMC Challenger question (weekly) | `index.html` line ~1305 | Edit `.challenger-question-text` |
| BMC Challenger solution | `index.html` line ~2404 | Edit `#challengerSolutionContent` |
| Video titles & captions | `index.html` lines ~1957–2055 | Edit `data-title`, `data-caption`, `.video-title`, `.video-caption` |
| Admissions features list | `index.html` lines ~1614–1641 | Edit `.admit-feature-text` |
| Contact details | `index.html` contact section | Update phone, address, maps link |
| Portal notices | `portal.html` notices section | Add/edit notice rows |
| Admin notice poster | `admin.html` | Use the "Post Notice" UI |
| SEO meta tags | `index.html` lines 6–46 | Edit `<title>`, `<meta name="description">` |

**Weekly BMC Challenger update checklist:**
1. Replace question text in `.challenger-question-text`
2. Replace solution in `#challengerSolutionContent`
3. Update `CHALLENGER_SHARE` object in JS (text field)
4. Update `shareChallenger()` text in JS
5. Update week dates in `.challenger-meta-strip`

---

## 3. Tech Stack & Architecture

### Frontend
```
HTML5 / CSS3 / Vanilla JavaScript (ES2020+)
Bootstrap 5.3.2          — grid, utilities, responsive layout
Bootstrap Icons 1.11.3   — icon set (bi-* classes)
Barlow Condensed         — Google Fonts (display/heading)
DM Sans                  — Google Fonts (body)
Canvas API               — branded share cards, login background animation
```

### Third-party Services
```
Formspree                — form submissions (admissions + doubt)
                           Status: PLACEHOLDER — needs real form IDs
                           Admissions form ID: YOUR_FORM_ID
                           Doubt form ID:      YOUR_DOUBT_FORM_ID

WhatsApp Business API    — wa.me redirects (no API key needed)
                           Number: +91 9516210209

Jitsi Meet (public)      — doubt video sessions (meet.jit.si)
                           Room format: BMC-Doubt-YYYY-MM-DD
                           Phase 2: self-hosted on DigitalOcean

YouTube Live (embed)     — live class streaming
                           Player: standard YouTube iframe embed
                           Video ID set manually per class in CONFIG block
```

### Data Storage (Client-side only, Phase 1)
```
localStorage:
  bmc_leads              — OTP-verified BMC Challenger leads
                           Schema: [{ name, phone, class, source, timestamp }]
                           Read by: admin.html → Question Leads tab

sessionStorage:
  bmc_live_session       — Live class login session
                           Schema: { valid: true, id: "BMC-2026-001" }
```

### No Build System
This project intentionally has no build pipeline. No npm, no Webpack, no Babel, no PostCSS. All CSS and JS is authored directly and inlined in each HTML file. Rationale: GitHub Pages serves static files; there is no build step in the deployment workflow. If a build system is added in Phase 2, this journal will be updated.

---

## 4. File Structure & Page Map

```
/
├── index.html            Public marketing site (main entry point)
├── login.html            Student + Admin login (role-based tabs)
├── portal.html           Student portal (gated — requires login)
├── admin.html            Admin dashboard (gated — admin credentials only)
├── doubt.html            Doubt submission (3-step: details → attach → send)
├── live-class.html       Live class page (gated — student login)
├── JOURNAL.md            This file
│
├── image/
│   ├── BMC_LOGO.svg      Primary logo (used in nav, footer, login)
│   └── shyam-bhatia.jpg  Mentor photo (used in mentor section)
│
├── assets/
│   ├── videos/
│   │   ├── video-1.mp4   Video gallery reel 1 (9:16 portrait)
│   │   ├── video-2.mp4   Video gallery reel 2
│   │   └── video-3.mp4   Video gallery reel 3
│   └── images/
│       ├── thumb-1.jpg   Thumbnail for video 1 (400×711px recommended)
│       ├── thumb-2.jpg   Thumbnail for video 2
│       └── thumb-3.jpg   Thumbnail for video 3
│
└── assets/pdfs/          DPP and PYQ downloadable files
    ├── DPP-Maths_Quadratic.docx
    ├── DPP_EMI-Physics.docx
    ├── DPP-Thermodynamics-Physics.docx
    ├── DPP-DPP_hydrocarben_chemistry.docx
    ├── Chemistry_DPP__Ionic_Equilirium.docx
    ├── DPP_Advance_Problem_in_physics.docx
    ├── jee_adv2023_1_English.pdf
    ├── jee_adv_2023_2_English.pdf
    ├── jee_adev_2023_1_Hindi.pdf
    ├── jeea_dv_2023_2_Hindi.pdf
    └── jeeadv2024_1_Hindi.pdf
```

### Page Relationships
```
index.html
  ├── → login.html          (Student Login / Admin Login nav button)
  ├── → doubt.html          (Ask a Doubt button — hero + navbar)
  └── → #video-gallery      (Videos nav link)

login.html
  ├── → portal.html         (on successful student login)
  └── → admin.html          (on successful admin login)

portal.html
  ├── → live-class.html     (Live Classes nav item + dashboard banner)
  └── → doubt.html          (Submit Doubt quick action)

live-class.html
  └── → portal.html         (back arrow)

doubt.html
  └── → index.html          (back arrow + success screen)

admin.html
  └── reads bmc_leads       (from localStorage — set by index.html challenger OTP flow)
```

---

## 5. Deployment & Hosting Guide

### `[DEVOPS]` Current Setup

**Platform:** GitHub Pages
**Repo:** `https://github.com/prabhakarmdes12-cmyk/Bhatia-Master-Classes`
**Branch:** `main` (auto-deploys on push)
**Live URL:** `https://prabhakarmdes12-cmyk.github.io/Bhatia-Master-Classes/`

### Deploying Changes

**Option A — GitHub Web Editor (quick single-file edits):**
1. Go to the repo on GitHub
2. Click the file to edit → pencil icon (✏️)
3. Make changes → scroll down → click **"Commit changes"**
4. GitHub Pages rebuilds automatically (takes ~30–60 seconds)

**Option B — Git CLI (recommended for multi-file changes):**
```bash
git clone https://github.com/prabhakarmdes12-cmyk/Bhatia-Master-Classes.git
cd Bhatia-Master-Classes

# Make your changes, then:
git add .
git commit -m "feat: describe what you changed"
git push origin main
```

**Option C — GoDaddy cPanel File Manager (secondary hosting):**
1. Log in to GoDaddy → cPanel → File Manager
2. Navigate to `public_html/`
3. Upload updated files directly
4. Changes are live immediately (no build step)

### `[DEVOPS]` Uploading Video Files

Video files are large — **do not commit them to git** (GitHub has a 100MB file limit; the repo will get bloated).

**Recommended workflow for videos:**
1. Upload MP4 files to GitHub via the web UI (drag & drop on the repo page)
2. Or use Git LFS (Large File Storage) — needs setup: `git lfs track "*.mp4"`
3. Or upload to the GoDaddy hosting `public_html/assets/videos/` via cPanel

**Video specs for optimal performance:**
- Format: MP4 (H.264)
- Aspect ratio: 9:16 (portrait, Instagram size)
- Resolution: 1080×1920px
- Max file size: 15MB per video (compress with HandBrake, CRF 28)
- Thumbnail: JPG, 400×711px, < 100KB

### `[DEVOPS]` Custom Domain Setup (when ready)

```
1. Buy/configure domain on GoDaddy (e.g. bhatiamc.in)
2. In GoDaddy DNS: Add CNAME record → www → prabhakarmdes12-cmyk.github.io
3. In GoDaddy DNS: Add A records for GitHub Pages IPs:
   185.199.108.153
   185.199.109.153
   185.199.110.153
   185.199.111.153
4. In GitHub repo Settings → Pages → Custom domain → enter domain
5. Check "Enforce HTTPS" (free SSL via Let's Encrypt — auto-provisioned)
6. DNS propagation: 24–48 hours
```

---

## 6. Current Progress & Changelog

### ✅ Completed (as of March 2026)

#### Phase 1 — Core Website
- [x] Full responsive marketing site — 9 sections (Hero, Mentor, BMC Challenger, DPP, Test Series, PYQ, Video Gallery, Admissions, Contact)
- [x] Sticky navbar with active-section highlighting on scroll
- [x] SEO meta tags, Open Graph tags, structured heading hierarchy
- [x] WhatsApp floating button

#### Phase 1 — Interactive Features
- [x] **BMC Challenger** — weekly JEE question, OTP verification flow (simulated), lead capture to localStorage
- [x] **Crack These** — 4 daily questions with gated solution modal (name + phone + class form)
- [x] **Branded share cards** — Canvas-rendered question cards with BMC branding
- [x] **Share sheet** — WhatsApp, Facebook, Instagram, Copy Link, Save Image
- [x] **Deep linking** — `#q-0` through `#q-3` and `#bmc-challenger` hash routes, smooth scroll + glow animation on landing
- [x] **OTP flow** — 6-box input, auto-advance, backspace nav, paste support, 30s resend timer, shake animation on wrong OTP

#### Phase 1 — Pages
- [x] `login.html` — Student + Admin tabs, animated math symbol background (Canvas, mouse-reactive)
- [x] `portal.html` — Student portal with 8 sections: Dashboard, Profile, DPP, Tests, PYQ, Performance, Timetable, Notices. Live Classes quick action + dashboard banner added.
- [x] `admin.html` — Admin dashboard with 9 sections including Question Leads tab (reads localStorage, export CSV, WhatsApp follow-up)
- [x] `doubt.html` — 3-step doubt submission: details form → attach (camera/upload/draw) → preview with rotate & crop → WhatsApp CTA
- [x] `live-class.html` — Live class page: login gate, YouTube live embed, countdown timer, LIVE NOW badge, Jitsi doubt sessions, teacher admin bar

#### Phase 1 — Content
- [x] 6 DPP sheets linked (Maths Quadratic, Physics EMI, Physics Thermodynamics, Chemistry Hydrocarbons, Chemistry Ionic Equilibrium, Physics Advanced)
- [x] 5 PYQ packs linked (JEE Advanced 2023 — P1/P2 English + Hindi, JEE Adv 2024 Hindi)
- [x] 3 video gallery slots configured (awaiting actual video files from client)

---

## 7. Known Issues & Bugs

> Format: **`[SEVERITY]` `[DEPARTMENT]`** Description — Root cause — Fix status

---

**`[HIGH]` `[FRONTEND]`** Formspree form IDs are placeholders
- `index.html` — admissions form: `YOUR_FORM_ID`
- `doubt.html` — doubt form: `YOUR_DOUBT_FORM_ID`
- **Impact:** Form submissions silently fail. The success UI still shows (by design — WhatsApp is primary channel) but data is not emailed to client.
- **Fix:** Client needs to create a free Formspree account at formspree.io, create two forms, and replace the placeholder IDs.

---

**`[HIGH]` `[FRONTEND]`** OTP is simulated — no real SMS sent
- `live-class.html` and `index.html` (BMC Challenger) both use client-side OTP generation.
- **Impact:** The OTP is visible in the dev-mode banner. Any user can see and use it. Not secure for production.
- **Fix (Phase 2):** Integrate Fast2SMS or MSG91 API via a backend endpoint. The frontend flow is already built — only the delivery mechanism needs to change.

---

**`[HIGH]` `[DEVOPS]`** Video files not yet uploaded
- `assets/videos/video-1.mp4`, `video-2.mp4`, `video-3.mp4` referenced in `index.html` but files don't exist yet.
- `assets/images/thumb-1.jpg`, `thumb-2.jpg`, `thumb-3.jpg` likewise missing.
- **Impact:** Video gallery shows broken/black cards.
- **Fix:** Client to provide videos → compress to spec → upload to repo or hosting.

---

**`[MEDIUM]` `[FRONTEND]`** Live class `isLive` flag is hardcoded
- `CONFIG.isLive = false` in `live-class.html`. Must be manually set to `true` before class and back to `false` after.
- **Impact:** Teacher must remember to push a code change before each live class.
- **Fix:** Short-term — teacher can use the in-page admin bar toggle (no code edit needed). Long-term (Phase 2) — backend flag in a database.

---

**`[MEDIUM]` `[CONTENT]`** BMC Challenger solution visible in dev-mode banner
- The simulated OTP and a yellow dev-mode banner showing the OTP code is visible to all users.
- **Impact:** Minor trust issue — students can see "Dev mode" messaging.
- **Fix:** Remove or hide the `otp-dev-hint` div once real SMS is integrated. Or conditionally show only when `CONFIG.isTeacher = true`.

---

**`[MEDIUM]` `[BACKEND]`** Login credentials are hardcoded
- `login.html`: `student: { id: 'BMC-2026-001', password: 'bmc2026' }` and `admin: { email: 'admin@bhatiamc.in', password: 'admin2026' }`
- **Impact:** Anyone who views source can log in. No multi-student support.
- **Fix (Phase 2):** Replace with a real auth API. This is acceptable for Phase 1 demo/MVP.

---

**`[LOW]` `[FRONTEND]`** `bmc_leads` localStorage cleared on browser data clear
- Admin leads are stored in the browser's localStorage on the client's device only.
- **Impact:** If the admin clears browser data, all leads are lost permanently.
- **Fix:** Before clearing, use the Export CSV button in admin.html → Question Leads tab. Phase 2 will move this to a proper database.

---

**`[LOW]` `[DESIGN]`** Mentor photo path is `image/shyam-bhatia.jpg`
- The mentor section references a local image that may not be in the repo.
- **Impact:** Mentor section shows broken image placeholder.
- **Fix:** Ensure `image/shyam-bhatia.jpg` is in the repo root's `image/` folder.

---

## 8. Roadmap — Upcoming Features

### 🟡 Phase 1.5 — Polish (No backend needed)

| Feature | Dept | Priority | Notes |
|---|---|---|---|
| Replace Formspree placeholders with real form IDs | `[FRONTEND]` `[CONTENT]` | 🔴 Critical | Client action required |
| Upload video files + thumbnails | `[DEVOPS]` `[CONTENT]` | 🔴 Critical | Client to provide videos |
| Upload mentor photo | `[DEVOPS]` | 🟠 High | `image/shyam-bhatia.jpg` |
| Remove OTP dev-mode banner from production | `[FRONTEND]` | 🟠 High | One line CSS change |
| Add Google Analytics tracking | `[DEVOPS]` `[CONTENT]` | 🟡 Medium | Client needs GA4 property |
| Add WhatsApp chat widget (Tawk.to or similar) | `[FRONTEND]` | 🟡 Medium | Free service |
| Add more DPP files (Biology, remaining Physics) | `[CONTENT]` | 🟡 Medium | Client to provide PDFs |
| JEE Mains PYQ packs | `[CONTENT]` | 🟡 Medium | Client to provide PDFs |
| NEET PYQ packs | `[CONTENT]` | 🟡 Medium | Client to provide PDFs |
| Custom domain setup (bhatiamc.in) | `[DEVOPS]` | 🟡 Medium | GoDaddy DNS config |

### 🔵 Phase 2 — Backend Integration

| Feature | Dept | Notes |
|---|---|---|
| Real SMS OTP (Fast2SMS / MSG91) | `[BACKEND]` `[FRONTEND]` | ₹0.15/SMS approx |
| Real multi-student authentication | `[BACKEND]` `[FRONTEND]` | Replace hardcoded credentials |
| Formspree → Custom API for form submissions | `[BACKEND]` | Email + DB storage |
| Leads DB (replace localStorage) | `[BACKEND]` `[DEVOPS]` | PostgreSQL or Firestore |
| Jitsi self-hosted (DigitalOcean) | `[BACKEND]` `[DEVOPS]` | ₹800/month, full host control |
| Live class — dynamic isLive flag | `[BACKEND]` `[FRONTEND]` | Teacher dashboard toggle |
| Attendance tracking | `[BACKEND]` | Log join/leave times |
| Class recording archive | `[DEVOPS]` `[CONTENT]` | YouTube unlisted links per session |

### 🟣 Phase 3 — Platform Expansion

| Feature | Dept | Notes |
|---|---|---|
| Student progress tracking (real data) | `[BACKEND]` `[DESIGN]` | Replace dummy stats in portal |
| Online test engine with timer + auto-grade | `[BACKEND]` `[FRONTEND]` | MCQ + integer type |
| Fee payment integration (Razorpay) | `[BACKEND]` | ₹2/transaction + 2% |
| Parent portal (read-only view) | `[DESIGN]` `[FRONTEND]` | Separate login role |
| Mobile app (React Native or PWA) | `[FRONTEND]` | PWA is lower effort |
| Push notifications for class reminders | `[BACKEND]` `[DEVOPS]` | Web Push API or FCM |

---

## 9. Environment Variables & Secrets

> `[BACKEND]` `[DEVOPS]` — This section tracks all credentials and service keys.
> **Never commit real secrets to git.** This table documents what keys exist and where they go.

| Key | Used In | Current Status | Where to Get |
|---|---|---|---|
| `FORMSPREE_ADMISSIONS_ID` | `index.html` | ❌ Placeholder (`YOUR_FORM_ID`) | formspree.io → create form |
| `FORMSPREE_DOUBT_ID` | `doubt.html` | ❌ Placeholder (`YOUR_DOUBT_FORM_ID`) | formspree.io → create form |
| `WHATSAPP_NUMBER` | `index.html`, `doubt.html`, `admin.html` | ✅ Set (`919516210209`) | Client confirmed |
| `STUDENT_ID` | `login.html`, `live-class.html` | ⚠️ Hardcoded (`BMC-2026-001`) | Phase 2: move to DB |
| `STUDENT_PASSWORD` | `login.html`, `live-class.html` | ⚠️ Hardcoded (`bmc2026`) | Phase 2: move to DB |
| `ADMIN_EMAIL` | `login.html` | ⚠️ Hardcoded (`admin@bhatiamc.in`) | Phase 2: move to DB |
| `ADMIN_PASSWORD` | `login.html` | ⚠️ Hardcoded (`admin2026`) | Phase 2: move to DB |
| `FAST2SMS_API_KEY` | Not yet integrated | ❌ Not set | fast2sms.com after Phase 2 |
| `YOUTUBE_LIVE_VIDEO_ID` | `live-class.html` CONFIG | ⚠️ Set per-class manually | YouTube Studio → Live → Copy ID |
| `JITSI_ROOM_NAME` | `live-class.html` CONFIG | ✅ Auto-generated (date-based) | No action needed |

---

## 10. Design System Reference

> `[DESIGN]` `[FRONTEND]` — Single source of truth for all visual tokens.

### Color Palette

| Token | Hex | Usage |
|---|---|---|
| `--primary` | `#1B3A6B` | Primary buttons, borders, headings |
| `--primary-dark` | `#0F2245` | Navbar, dark section backgrounds, footer |
| `--accent` | `#F4A825` | CTAs, highlights, active states, gold accents |
| `--accent-light` | `#FCC84A` | Accent hover states, lighter highlights |
| `--teal` | `#00A8A8` | Secondary accent, Physics subject color, teal gradients |
| `--light-bg` | `#F5F7FA` | Section alternating background |
| `--text` | `#1A1A2E` | Body text, headings |
| `--text-muted` | `#6B7280` | Captions, metadata, placeholder text |
| `--border` | `#E5E9F0` | Card borders, dividers, form fields |
| `--success` | `#16A34A` | Success states, correct answers, Biology |
| `--danger` | `#DC2626` | Error states, validation, hard difficulty |

### Typography Scale

| Use | Font | Weight | Size |
|---|---|---|---|
| Page title / hero h1 | Barlow Condensed | 800 | `clamp(2.8rem, 6vw, 5rem)` |
| Section titles h2 | Barlow Condensed | 800 | `clamp(2rem, 4vw, 3.2rem)` |
| Card titles h3/h4 | Barlow Condensed | 800 | `1.25–1.6rem` |
| Body copy | DM Sans | 400 | `1rem` (16px) |
| Captions / meta | DM Sans | 500 | `0.82–0.88rem` |
| Labels / badges | Barlow Condensed | 700–800 | `0.75–0.95rem` |
| Navigation links | Barlow Condensed | 600 | `1.05rem` |

### Spacing & Shape

| Token | Value | Usage |
|---|---|---|
| `--radius` | `12px` | Small cards, form inputs, badges |
| `--radius-lg` | `20px` | Main content cards, modals, panels |
| `--shadow-sm` | `0 2px 8px rgba(27,58,107,0.08)` | Card resting state |
| `--shadow-md` | `0 8px 32px rgba(27,58,107,0.12)` | Card hover, modals |
| `--shadow-lg` | `0 20px 60px rgba(27,58,107,0.18)` | Floating elements, lightboxes |
| `--transition` | `all 0.3s cubic-bezier(0.4, 0, 0.2, 1)` | All interactive transitions |
| `section-pad` | `padding: 80px 0` | All top-level sections |

### Subject Color Coding

Used consistently across DPP cards, PYQ cards, share cards, and subject tags:

| Subject | Class | Background | Text |
|---|---|---|---|
| Mathematics | `badge-math` / `vst-math` | `rgba(27,58,107,0.1)` | `--primary` |
| Physics | `badge-phys` / `vst-phys` | `rgba(0,168,168,0.1)` | `--teal` |
| Chemistry | `badge-chem` / `vst-chem` | `rgba(244,168,37,0.12)` | `#B7750A` |
| Biology | `badge-bio` / `vst-bio` | `rgba(22,163,74,0.1)` | `#166534` |

---

*This journal is a living document. Update it whenever a significant change is made to the project — new features, architectural decisions, resolved bugs, or team changes.*

*Last entry: March 2026 — Prabhakar*
