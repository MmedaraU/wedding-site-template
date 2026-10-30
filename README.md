#  Wedding Website Template

A custom, static wedding website. No build step, no frameworks, no dependencies. Just HTML, CSS, and vanilla JavaScript.

**Live Date:** 16 December 2028  
**Location:** Eket, Akwa Ibom

---

## 🚨 PRE-LAUNCH CHECKLIST (Placeholders to Replace)

Before sharing the link with guests, you must find and replace all the bracketed placeholders and subject-to-change details listed below.

### 1. Website Content (`index.html`)
*   **Wishing Well:** Replace `[YOUR BANK NAME]`, `[YOUR ACCOUNT NAME]`, `[YOUR ACCOUNT NUMBER]`.
*   **Programme:** The Google Drive link is already set. Just ensure the file permissions in Google Drive are set to "Anyone with the link can view".
*   **Wedding Photos:** Replace `[YOUR_GOOGLE_PHOTOS_LINK_HERE]` (found in the Hero section and the Programme section).
*   **Local Help (In Colours Section):** Replace `[Coordinator Name 1]`, `[Phone Number 1]`, `[Coordinator Name 2]`, `[Phone Number 2]`.

### 2. Google Maps Links (`index.html`)
In the Programme section, update the `<a href="...">` tags with the actual Google Maps links for your venues.

### 3. The Google Apps Script
Open your Apps Script editor and update the `EMAIL_CONFIG` at the very top:
*   **`logoUrl`**: Host your logo on Sirv and paste the URL here.
*   **`coupleEmail`**: Currently set to `'mediumana@gmail.com, okparaemmanuel2017@gmail.com'`.

### 4. The Password Gate (`index.html`)
Find `const CORRECT_HASH = '...';` in the `<script>` block. Replace the hash with your new SHA-256 hashed password.

---

## 1. The Files
- `index.html` — The main website.
- `404.html` — The custom "page not found" page.
- `scanner.html` — The private page for ushers (Currently dormant).
- `RESTORE_QR_CHECKIN.md` — Instructions for turning QR codes back on.
- `README.md` — This file.

---

## 2. The Google Sheets Setup

You now need **three** tabs in your Google Sheet:
1.  `RSVP`
2.  `Letters`
3.  `Guest List` (For your planner)

### A. RSVP Tab Headers
Paste this TSV into Cell A1:
```text
Timestamp	Name	Email	Attending	Guests	Requests	CheckedIn
```

### B. Letters Tab Headers
Paste this TSV into Cell A1:
```text
Timestamp	Name	Message
```

### C. Guest List Tab Headers (Crucial for sync)
The sync script looks for these exact headers in your `Guest List` tab:
```text
Names	Guest Response	Number to expect	Category	How to invite	Invited to
```
*(When someone RSVPs, the script will automatically find their name, update their "Guest Response" to "Coming" or "Not Coming", and update the "Number to expect").*

### D. The "New Version" Rule
If you make *any* change to the Apps Script code, you **must** redeploy it as a **New version** (`Deploy > Manage deployments > Edit > Version: New version > Deploy`). If you don't, Google will keep running the old code.

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
- Display: `Fraunces`
- Body: `Newsreader`
- Sans/UI: `Inter`
