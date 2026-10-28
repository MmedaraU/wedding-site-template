# Wedding Website Template

A custom, static wedding website. No build step, no frameworks, no dependencies. Just HTML, CSS, and vanilla JavaScript. 

**Live Date:** 16 December 2028  
**Location:** Eket, Akwa Ibom

---

## 🚨 PRE-LAUNCH CHECKLIST (Placeholders to Replace)

Before sharing the link with guests, you must find and replace all the bracketed placeholders and subject-to-change details listed below.

### 1. Website Content (`index.html`)
Find these sections and replace the bracketed text:
*   **Travel & Stay (Accommodation):** `[Discounted Rate]`, `[Hotel Name]`.
*   **Travel & Stay (Venues):** `[Church Name]`, `[Church Address]`, `[Reception Hall Name]`, `[Reception Hall Address]`.
*   **Travel & Stay (Transport):** `[Park Name]`.
*   **Travel & Stay (Local Help):** `[Coordinator Name 1]`, `[Phone Number 1]`, `[Coordinator Name 2]`, `[Phone Number 2]`.
*   **Wishing Well:** `[YOUR BANK NAME]`, `[YOUR ACCOUNT NAME]`, `[YOUR ACCOUNT NUMBER]`.
*   **Programme:** Replace `[YOUR_GOOGLE_DRIVE_LINK]` with the link to your Day-of Programme PDF.

### 2. Google Maps Links (`index.html`)
In the Travel section, find the `<a href="...">` tags and replace the generic search links with the actual links for your venues.
*   `https://www.google.com/maps?q=Hotel+Name+Address+Eket`
*   `https://www.google.com/maps?q=Church+Name+Address+Eket`
*   `https://www.google.com/maps?q=Reception+Hall+Name+Address+Eket`
*   `https://www.google.com/maps?q=Park+Name+Address+Eket`

### 3. The Google Apps Script (Backend & Email)
Open your Apps Script editor and update the following:
*   **`logoUrl`**: (At the very top) If you have a logo for the email header, host it on a public image host like **Sirv** and paste the direct image URL here. If left as `''`, it uses a text-based monogram.
*   **Email 2 (Accommodation)**: Scroll down to the second email template and replace:
    *   `[Discounted Rate]`
    *   `[YOUR BANK NAME]`
    *   `[YOUR ACCOUNT NAME]`
    *   `[YOUR ACCOUNT NUMBER]`
    *   `[YOUR PHONE NUMBER]` (Where guests send their payment receipts).

### 4. The Scanner Page (`scanner.html`)
*   Paste your deployed Google Apps Script Web App URL (the one ending in `/exec`) into the `const SCRIPT_URL = '...'` variable at the bottom of the file.

---

## 1. The Files
- `index.html` — The main website.
- `404.html` — The custom "page not found" page.
- `scanner.html` — The private page for ushers to scan QR codes on the wedding day.
- `README.md` — This file.

---

## 2. How to Make Changes

### A. Photos
To use real photos:
1. Create an `images` folder next to `index.html`.
2. Put your photos in it.
3. Replace the `src="https://picsum.photos/..."` with `src="images/your-photo.jpg"`.
4. **Aspect Ratios:**
   - **Hero Image:** Landscape on desktop (`3:2`), portrait on mobile (`4:5`). Size: `1600x1067`.
   - **Story Image:** Portrait (`3:4`). Size: `900x1200`.
   - **Gallery Images:** Uniform portrait (`4:5`). Size: `900x1125`.

### B. The Countdown
The countdown targets **16 December 2028 at 08:00 WAT**. 
To change it, find this line in the `<script>` block at the bottom of `index.html`:
`const TARGET = Date.UTC(2028, 11, 16, 7, 0, 0);`
*(Note: Months are 0-indexed, so `11` is December. WAT is UTC+1).*

### C. Timed Reveals (Hiding Sections)
You can hide any section or element until a specific date by adding `data-reveal-date="YYYY-MM-DD"` to its container. 
*   **Example:** The Shuttle Schedule currently has `data-reveal-date="2028-12-01"`. It will not show up on the site until December 1, 2028. 
*   To make it show immediately for testing, simply delete that attribute from the HTML.

---

## 3. The Forms (RSVP & Letters)

Both forms submit silently to a Google Sheet using a Google Apps Script. 

### A. Google Sheet Setup
You need a Google Sheet with two tabs named exactly `RSVP` and `Letters`.

**Paste these TSV (Tab-Separated Values) strings into Cell A1 of each tab:**

**RSVP Tab:**
```text
Timestamp	Name	Email	Attending	Guests	GuestNames	Children	Accommodation	Transport	Requests	CheckedIn
```

**Letters Tab:**
```text
Timestamp	Name	Message
```

### B. ⚠️ The #1 Rule for Apps Script
If you make *any* change to the Apps Script code, you **must** redeploy it as a **New version** (`Deploy > Manage deployments > Edit > Version: New version > Deploy`). If you don't, Google will keep running the old code.

### C. Email Deliverability & Logos
*   **Daily Limit:** Google Apps Script has a daily email limit (100/day for free Gmail, 1,500/day for Workspace). 
*   **Email Logo Hosting:** Email clients require images to have public URLs. **Sirv** is recommended for hosting your email logo. Upload the logo to Sirv, copy the direct image link, and paste it into the `logoUrl` variable in the Apps Script. 

---

## 4. The Wedding Day (QR Check-in)
The RSVP confirmation email automatically generates a QR code for each guest. 

1. On the wedding day, open `scanner.html` on a phone or tablet (e.g., `yourdomain.com/scanner.html`).
2. Allow camera access.
3. Point the camera at the guest's QR code.
4. The scanner will communicate with the Google Sheet and update the `CheckedIn` column with the time they arrived.

---

## 5. Design System

**Colors**
- Background (Wine): `#2A0E14`
- Text (Ivory): `#F5EFE6`
- Accent 1 (Coral): `#E24E42`
- Accent 2 (Gold): `#B8935A`

**Dress Code Swatches (CSS Gradients)**
- Emerald Green: `linear-gradient(135deg, #1E3A2F 0%, #0F241D 100%)`
- Dark Espresso: `linear-gradient(135deg, #3A2318 0%, #1E110B 100%)`
- Tuscan Gold: `linear-gradient(135deg, #E8D5B5 0%, #C9A46B 100%)`

**Fonts (Google Fonts)**
- Display: `Fraunces` (Variable font; uses `WONK` and `SOFT` axes)
- Body: `Newsreader`
- Sans/UI: `Inter`

---

## 6. Deploying
Because this is pure static HTML/CSS/JS, you can host the site itself anywhere for free:
- **Netlify Drop:** Drag the folder containing your files onto [app.netlify.com/drop](https://app.netlify.com/drop).
- **Vercel:** Run `vercel` in the terminal.
- **GitHub Pages:** Push to a repo and enable Pages in settings.

*Note: Ensure `404.html` is at the root of your deployment folder. Most hosts will automatically serve it for missing routes.*