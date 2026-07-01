# VerifyStay — Frontend

> A 5-step web verification wizard for Airbnb property listings — built with pure HTML + CSS + JS

[![HTML](https://img.shields.io/badge/HTML-5-orange?style=flat-square)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![CSS](https://img.shields.io/badge/CSS-3-blue?style=flat-square)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![JavaScript](https://img.shields.io/badge/JavaScript-ES6-yellow?style=flat-square)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![No Framework](https://img.shields.io/badge/No%20Framework-Zero%20Dependencies-green?style=flat-square)]()

---

## Live Demo

🔗 **[https://verifystay-frontend.vercel.app]**

---

## What Does This Do?

This is the host-facing web app that collects all verification data before an Airbnb listing goes live.

It runs entirely in the browser — no app download, no phone required.

---

## 5-Step Verification Flow

```
Step 1 → Host Identity
         Enter name, PAN number, Aadhaar

Step 2 → GPS Location
         Browser captures live GPS automatically
         Address geocoded to lat/long via Nominatim

Step 3 → Live Photo
         One-time OTP shown on screen
         Host takes webcam photo with OTP visible
         OR uploads phone photo (GPS embedded in EXIF)

Step 4 → 7/12 Land Record
         Upload 7/12 Utara / Khasra / Property Card
         PDF or image accepted

Step 5 → Listing Details
         Title, description, price
         Scanned for fraud keywords before submission
```

---

## Browser Features Used

| Feature | Web API | Purpose |
|---------|---------|---------|
| Live GPS | `navigator.geolocation` | Capture host's real-time location |
| Webcam | `navigator.mediaDevices.getUserMedia` | Take live photo at property |
| File Upload | `<input type="file">` | Upload 7/12 land record |
| Address Geocoding | Nominatim (OpenStreetMap) | Convert address → lat/long |
| EXIF GPS | Read via backend (piexif) | Verify photo taken at property |

> **No API key needed** — Nominatim is free and open source.

---

## Project Structure

```
verifystay-frontend/
└── index.html    # Complete app — HTML + CSS + JS in one file
```

That's it. One file. No build step. No dependencies. No framework.

---

## Run Locally

### Option 1 — Just open the file

```bash
# Double-click index.html in your file explorer
# OR
open index.html        # macOS
start index.html       # Windows
xdg-open index.html    # Linux
```

### Option 2 — With a local server (recommended for GPS/webcam)

```bash
# Python
python -m http.server 3000

# Node.js
npx serve .

# Then open: http://localhost:3000
```

> **Important:** GPS and webcam require HTTPS or localhost.  
> Opening the file directly (`file://`) may block these features in some browsers.

---

## Connect to Backend

By default the frontend calls:
```javascript
const API_URL = "http://localhost:8000";
```

To connect to your deployed backend, update this line in `index.html`:

```javascript
const API_URL = "https://your-backend.onrender.com";
```

> **Offline mode:** If the backend is not running, the frontend automatically uses built-in demo logic — it still works and shows results!

---

## Deploy to Vercel (Free)

### Option 1 — Drag and drop

1. Go to [vercel.com](https://vercel.com)
2. Drag the `frontend/` folder onto the Vercel dashboard
3. Done — live in 30 seconds!

### Option 2 — Via CLI

```bash
npm install -g vercel
cd frontend/
vercel deploy
```

### Option 3 — Via GitHub

1. Push this repo to GitHub
2. Import on Vercel → select the repo
3. Set root directory to `frontend/`
4. Deploy

---

## Deploy to Netlify (Free)

1. Go to [netlify.com](https://netlify.com)
2. Drag the `frontend/` folder onto the deploy area
3. Live instantly!

---

## Demo Flow — What to Enter

### ✅ VERIFIED listing (score 85+/100)

| Step | Field | Value |
|------|-------|-------|
| 1 | Host name | `Ramprasad Londhe` |
| 1 | PAN | `ABCPS1234D` |
| 1 | Aadhaar | `987654324521` |
| 2 | Address | `Survey No 661, Tulshi, Mohol, Solapur, Maharashtra 413213` |
| 2 | GPS | Click "Capture My Location" → Allow |
| 2 | Geocode | Click "Geocode Address" |
| 3 | Photo | Take webcam photo OR upload from phone |
| 4 | Land Record | Upload 7/12 Satbara PDF |
| 5 | Description | `Peaceful farmhouse. Free WiFi and parking.` |

**Result → VERIFIED 85–90/100 ✅**

---

### ❌ BLOCKED listing (score 0–15/100)

| Step | Field | Value |
|------|-------|-------|
| 1 | Host name | `Rajesh Kumar` |
| 1 | PAN | `AAAAA1111A` |
| 2 | Address | `Sea View Villa, Goa Beach Road` |
| 2 | GPS | Skip (don't capture) |
| 3 | Photo | Skip |
| 4 | Land Record | Skip |
| 5 | Description | `Pay Rs 2000 UPI advance to confirm booking` |

**Result → SUSPICIOUS 0/100 ❌**

---

## Key Design Decisions

**Why no framework?**  
Zero build step. Anyone can open it — no `npm install`, no bundler, no config.  
The entire app is one `index.html` — easy to audit, easy to deploy.

**Why does it work offline?**  
The frontend has built-in demo logic that mirrors the backend scoring exactly.  
If the API is unreachable, it falls back automatically — no error shown to user.

**Why Nominatim instead of Google Maps?**  
Nominatim (OpenStreetMap) is free, open source, and requires no API key.  
In a production integration, Google Maps Platform would give better accuracy.

**Why OTP on screen?**  
The random 6-digit OTP proves the photo was taken live — not uploaded from the internet.  
A fake host cannot find a stock photo that matches the OTP shown at verification time.

---

## Browser Compatibility

| Browser | GPS | Webcam | File Upload |
|---------|-----|--------|-------------|
| Chrome 90+ | ✅ | ✅ | ✅ |
| Firefox 88+ | ✅ | ✅ | ✅ |
| Safari 14+ | ✅ | ✅ | ✅ |
| Edge 90+ | ✅ | ✅ | ✅ |

> **Best experience:** Chrome on desktop with location and camera permissions allowed.

---

## Author

**Ramprasad Vilas Londhe**  
B.Tech IT  
[github.com/Ramprasadlondhe2005](https://github.com/Ramprasadlondhe2005)  
[ramprasadlondhe24@gmail.com](mailto:ramprasadlondhe24@gmail.com)
