# Wedding Website Template

A custom, static wedding website. No build step, no frameworks, no dependencies. Just HTML, CSS, and vanilla JavaScript.

**Live Date:** 16 December 2028  
**Location:** Eket, Akwa Ibom

---

## 🚨 PRE-LAUNCH CHECKLIST (Placeholders to Replace)

Before sharing the link with guests, you must find and replace all the bracketed placeholders and subject-to-change details listed below.

### 1. Website Content (`index.html`)
*   **Travel & Stay:** Replace `[Discounted Rate]`, `[Hotel Name]`, `[Church Name]`, `[Church Address]`, `[Reception Hall Name]`, `[Reception Hall Address]`, `[Park Name]`, `[Coordinator Name 1]`, `[Phone Number 1]`, `[Coordinator Name 2]`, `[Phone Number 2]`.
*   **Wishing Well:** Replace `[YOUR BANK NAME]`, `[YOUR ACCOUNT NAME]`, `[YOUR ACCOUNT NUMBER]`.
*   **Programme:** Replace `[YOUR_GOOGLE_DRIVE_LINK]` with the link to your Day-of Programme PDF.
*   **Wedding Photos:** Replace `[YOUR_GOOGLE_PHOTOS_LINK_HERE]` (found in both the Hero section and the Programme section).

### 2. Google Maps Links (`index.html`)
In the Travel section, update the `<a href="...">` tags with the actual Google Maps links for your venues.

### 3. The Google Apps Script
Open your Apps Script editor and update the `EMAIL_CONFIG` at the very top:
*   **`logoUrl`**: Host your logo on Sirv (or any public image host) and paste the URL here.
*   **`coupleEmail`**: Enter both of your emails separated by a comma (e.g., `'a@gmail.com, b@gmail.com'`).
*   **Email 2 (Accommodation)**: Scroll down to the second email template and replace `[Hotel Name]`, `[Hotel Full Address]`, `[YOUR BANK NAME]`, `[YOUR ACCOUNT NAME]`, `[YOUR ACCOUNT NUMBER]`, and `[YOUR PHONE NUMBER]`.

### 4. The Password Gate (`index.html`)
Find `const CORRECT_HASH = '...';` in the `<script>` block at the bottom. Replace the hash with your new SHA-256 hashed password.

---

## 1. The Files
- `index.html` — The main website.
- `404.html` — The custom "page not found" page.
- `scanner.html` — The private page for ushers (Currently dormant).
- `RESTORE_QR_CHECKIN.md` — Instructions for turning the QR codes back on.
- `README.md` — This file.

---

## 2. The Forms & Google Sheets

### A. Google Sheet Setup
Ensure your Google Sheet has two tabs named exactly `RSVP` and `Letters`.

**Paste these TSV headers into Cell A1:**
**RSVP Tab:**
```text
Timestamp	Name	Email	Attending	Guests	GuestNames	Children	Accommodation	Requests	CheckedIn
```
**Letters Tab:**
```text
Timestamp	Name	Message
```

### B. The "New Version" Rule
If you make *any* change to the Apps Script code, you **must** redeploy it as a **New version** (`Deploy > Manage deployments > Edit > Version: New version > Deploy`). If you don't, Google will keep running the old code.

### C. Dynamic Letters
The website automatically fetches the **6 most recent** letters from your Google Sheet and displays them. If you want to hide a letter, simply delete the row from the Google Sheet. If the sheet is empty, it defaults to showing the hardcoded sample letters.

---

## 3. Hiding Sections until a Specific Date
You can hide any element until a specific date by adding `data-reveal-date="YYYY-MM-DD"` to its container.
*   **Programme Button:** Hidden until `2028-12-16` (Wedding Day).
*   **Wedding Photos Button:** Hidden until `2028-12-17` (Day after).

---

## 4. Design System
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
- Display: `Fraunces` (Variable font)
- Body: `Newsreader`
- Sans/UI: `Inter`