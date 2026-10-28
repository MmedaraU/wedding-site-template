# Wedding Website Template

A custom, static wedding website. No build step, no frameworks, no dependencies. Just HTML, CSS, and vanilla JavaScript. 

**Live Date:** 16 December 2028  
**Location:** Eket, Akwa Ibom

---

## 🚨 PRE-LAUNCH CHECKLIST (Placeholders to Replace)

Before sharing the link with guests, you must find and replace all the bracketed placeholders and subject-to-change details listed below.

### 1. Travel & Stay Details (`index.html`)
Find the `<section class="travel-section">` block and replace:
*   `[Hotel Name & Address]`: The name and address of the hotel.
*   `[Discounted Rate]`: The final negotiated room rate (e.g., `₦10,000`). **This appears in two places:** on the website (Travel section) and in the Google Apps Script (Accommodation email).
*   `[Church Name], [Church Address]`: The name and address of the church.
*   `[Reception Hall Name], [Reception Hall Address]`: The name and address of the reception venue.
*   `[Park Name]`: The name of the park for departure.
*   `[Coordinator Name 1] / [Phone Number 1]`: Local contact for guests if they get lost.
*   `[Coordinator Name 2] / [Phone Number 2]`: Alternate local contact.

### 2. Google Maps Links (`index.html`)
In the Travel section, find the `<a href="...">` tags and replace the generic search links with the actual links. 
*   `https://www.google.com/maps?q=Hotel+Name+Address+Eket`
*   `https://www.google.com/maps?q=Church+Name+Address+Eket`
*   `https://www.google.com/maps?q=Reception+Hall+Name+Address+Eket`
*   `https://www.google.com/maps?q=Park+Name+Address+Eket`

### 3. Wishing Well / Gifts (`index.html`)
Find the `<section class="wishing-well wrap">` block and replace:
*   `[YOUR BANK NAME]`
*   `[YOUR ACCOUNT NAME]`
*   `[YOUR ACCOUNT NUMBER]` (This is also the text that gets copied when the user clicks the button).

### 4. Day-of Programme Link (`index.html`)
In the Programme section, find the `<a href="[YOUR_GOOGLE_DRIVE_LINK]">` button and replace the bracketed text with the shareable link to your Google Drive PDF.

### 5. The Google Apps Script (Backend & Email)
Open your Apps Script editor and update the following:
*   **`logoUrl`**: (At the very top) If you have a logo for the email header, host it on a public image host like **Sirv** and paste the direct image URL here. If left as `''`, it uses a text-based monogram.
*   **Email 2 (Accommodation)**: Scroll down to the second email template and replace:
    *   `[YOUR BANK NAME]`
    *   `[YOUR ACCOUNT NAME]`
    *   `[YOUR ACCOUNT NUMBER]`
    *   `[YOUR PHONE NUMBER]` (Where guests send their payment receipts).

### 6. Images (`index.html`)
The site currently uses placeholder images from `picsum.photos`. 
*   Replace the Hero Image (`1600x1067`).
*   Replace the Story Image (`900x1200`).
*   Replace the three Gallery Images (`900x1125`).

### 7. The RSVP Form Connection (`index.html`)
Ensure the `SCRIPT_URL` variable at the top of the `<script>` block is updated with your deployed Apps Script URL (it must end in `/exec`).

---

## 1. The Files
- `index.html` — The main website.
- `404.html` — The custom "page not found" page.
- `README.md` — This file.

---

## 2. How to Make Changes

### A. Text & Content
Open `index.html` in any text editor. Content is written directly in the HTML.
- **Names:** Search for `Mmedara & Ikedinachi`.
- **Story:** Search for `<div class="story__text"`.
- **Schedule:** Search for `<ol class="programme">`.
- **Dress Code (Colours):** Search for `<div class="aso-grid">`.
- **Wishing Well:** Search for `<section class="wishing-well">`.

### B. Photos
To use real photos:
1. Create an `images` folder next to `index.html`.
2. Put your photos in it.
3. Replace the `src="https://picsum.photos/..."` with `src="images/your-photo.jpg"`.
4. **Aspect Ratios:**
   - **Hero Image:** Landscape on desktop (`3:2`), portrait on mobile (`4:5`). Size: `1600x1067`.
   - **Story Image:** Portrait (`3:4`). Size: `900x1200`.
   - **Gallery Images:** Uniform portrait (`4:5`). Size: `900x1125`.

### C. The Countdown
The countdown targets **16 December 2028 at 08:00 WAT**. 
To change it, find this line in the `<script>` block:
`const TARGET = Date.UTC(2028, 11, 16, 7, 0, 0);`
*(Note: Months are 0-indexed, so `11` is December. WAT is UTC+1).*

### D. Mobile Navigation
On screens smaller than 1024px, the left-hand bead rail disappears and is replaced by a hamburger menu. 
- The links are located in `<nav class="mobile-menu" id="mobileMenu">`.
- The toggle animation is controlled by JS (`initMobileMenu()`).

---

## 3. The Forms (RSVP & Letters)

Both forms submit silently to a Google Sheet using a Google Apps Script. The RSVP form also sends automated HTML confirmation emails via `MailApp`.

### A. Google Sheet Setup
You need a Google Sheet with two tabs named exactly `RSVP` and `Letters`.

**Paste these TSV strings into Cell A1 of each tab:**

**RSVP Tab:**
```text
Timestamp	Name	Email	Attending	Guests	GuestNames	Children	Accommodation	Transport	Requests
```

**Letters Tab:**
```text
Timestamp	Name	Message
```

### B. ⚠️ The #1 Rule for Apps Script
If you make *any* change to the Apps Script code, you **must** redeploy it as a **New version** (`Deploy > Manage deployments > Edit > Version: New version > Deploy`). If you don't, Google will keep running the old code.

### C. Troubleshooting Forms
If data stops writing to the sheet or emails stop sending:
1. Check the `SCRIPT_URL` in `index.html`. It must be the `/exec` URL.
2. Check the **Executions** log in the Apps Script editor for errors.
3. Ensure your sheet tab names and headers match exactly (case-sensitive).

### D. Email Deliverability & Logos
*   **Daily Limit:** Google Apps Script has a daily email limit (100/day for free Gmail, 1,500/day for Workspace). Data will still save to the sheet even if emails fail.
*   **Email Logo Hosting:** Email clients require images to have public URLs. **Sirv** is recommended for hosting your email logo. Upload the logo to Sirv, copy the direct image link, and paste it into the `logoUrl` variable in the Apps Script. 

### E. Aso Ebi (Private Arrangement)
The website features a "Colours of the Day" section to guide guests on what to wear. There is **no Aso Ebi ordering mechanism on the site**. If you decide to provide Aso Ebi fabric to specific guests, you will manage this privately outside of the website's RSVP system.

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
- Display: `Fraunces` (Variable font; uses `WONK` and `SOFT` axes)
- Body: `Newsreader`
- Sans/UI: `Inter`

---

## 5. Deploying
Because this is pure static HTML/CSS/JS, you can host the site itself anywhere for free:
- **Netlify Drop:** Drag the folder containing your files onto [app.netlify.com/drop](https://app.netlify.com/drop).
- **Vercel:** Run `vercel` in the terminal.
- **GitHub Pages:** Push to a repo and enable Pages in settings.

*Note: Ensure `404.html` is at the root of your deployment folder. Most hosts will automatically serve it for missing routes.*