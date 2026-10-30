# Wedding Website Template

A custom, static wedding website. No build step, no frameworks, no dependencies. Just HTML, CSS, and vanilla JavaScript.

**Live Date:** 16 December 2028  
**Location:** Eket, Akwa Ibom

---

## 🚨 PRE-LAUNCH CHECKLIST (Placeholders to Replace)

Before sharing the link with guests, you must find and replace all the bracketed placeholders and subject-to-change details listed below.

### 1. Website Content (`index.html`)
*   **Wishing Well:** Replace `[YOUR BANK NAME]`, `[YOUR ACCOUNT NAME]`, `[YOUR ACCOUNT NUMBER]`.
*   **Programme:** The Google Drive link is already set. Just ensure the file permissions in Google Drive are set to "Anyone with the link can view".
*   **Wedding Photos:** Replace `[YOUR_GOOGLE_PHOTOS_LINK_HERE]` (found in both the Hero section and the Programme section).
*   **Local Help (In the Colours section):** Replace `[Coordinator Name 1]`, `[Phone Number 1]`, `[Coordinator Name 2]`, `[Phone Number 2]`.

### 2. Google Maps Links (`index.html`)
In the **Programme** section, update the `<a href="...">` tags with the actual Google Maps links for your venues:
*   `https://www.google.com/maps?q=Family+Compound+Onna`
*   `https://www.google.com/maps?q=Church+Name+Address+Eket`
*   `https://www.google.com/maps?q=Reception+Hall+Name+Address+Eket`

### 3. The Google Apps Script
Open your Apps Script editor and update the `EMAIL_CONFIG` at the very top:
*   **`logoUrl`**: Host your logo on Sirv (or any public image host) and paste the URL here.
*   **`coupleEmail`**: Enter both of your emails separated by a comma (e.g., `'a@gmail.com, b@gmail.com'`).

### 4. The Password Gate (`index.html`)
Find `const CORRECT_HASH = '...';` in the `<script>` block at the bottom. Replace the hash with your new SHA-256 hashed password.

### 5. Test the RSVP → Guest List Sync
Before sharing the site, submit a test RSVP for a name already on the Guest List:
1. Use a real guest's name (e.g. one from the sheet).
2. Open the sheet → `RSVP` tab → confirm the row wrote correctly.
3. Open the sheet → `Guest List` tab → that guest's `Guest Response` should now read `Coming` (or `Not Coming`), and `Number to expect` should match what was submitted.
4. Delete the test row from the `RSVP` tab afterward.

### 6. Review the Auto-Added Bucket Before Inviting
Any name that doesn't match an existing Guest List row gets appended with **Category = `RSVP (auto-added)`**. Before running `Generate Invitations` in the planner, set three fields on every flagged row:
- **Category** → change from `RSVP (auto-added)` to the real bucket.
- **How to invite** → `Physical Card` for anyone getting a card.
- **Invited to** → required for `generateInvites()`; blank rows are silently skipped.

---

## 1. The Files
- `index.html` — The main website.
- `404.html` — The custom "page not found" page.
- `README.md` — This file.

---

## 2. The Forms & Google Sheets

### A. Google Sheet Setup
Ensure your Google Sheet has three tabs named exactly: `RSVP`, `Letters`, and `Guest List`.

**Paste these TSV headers into Cell A1:**

**RSVP Tab:**
```text
Timestamp	Name	Attending	Email	Guests	Requests
```
*(Note: Since we removed the scanner, the `CheckedIn` column is no longer needed. You can delete it from your sheet if it exists).*

**Letters Tab:**
```text
Timestamp	Name	Message
```

**Guest List Tab:**
The sync script needs these exact headers (spelling matters):
```text
Names	Category	Number to expect	Guest Response	How to invite	Invited to	Accomodation Option
```

### B. The "New Version" Rule
If you make *any* change to the Apps Script code, you **must** redeploy it as a **New version** (`Deploy > Manage deployments > Edit > Version: New version > Deploy`). If you don't, Google will keep running the old code.

### C. Dynamic Letters
The website automatically fetches the **6 most recent** letters from your Google Sheet and displays them. If you want to hide a letter, simply delete the row from the Google Sheet. If the sheet is empty, it defaults to showing the hardcoded sample letters.

### D. RSVP → Guest List Sync
Every RSVP submission triggers an automatic sync in the backend. It runs synchronously inside the same `doPost` request.

**What it does:**
1. **Writes the RSVP row** to the `RSVP` tab.
2. **Syncs to `Guest List`:**
   - **If the name matches an existing row** → updates only `Guest Response` and `Number to expect`. Every other column is **never touched**.
   - **If the name doesn't match** → appends a new row with `Category = RSVP (auto-added)` (your signal to review), and `Invited to` left blank.
3. **Emails the couple** a notification with the RSVP details.
4. **Emails the guest** a confirmation (if attending), reminding them to bring their physical invitation card.

**Name matching is forgiving** — titles (`Mr`, `Mrs`, `Pastor`, `Chief`), the word "family", and punctuation are stripped before comparison. So `"Mr. Okpara & Family"` and `"okpara"` match.

### E. Re-Syncing Historical RSVPs
If you have RSVPs from before the sync was deployed, or you've edited the `RSVP` sheet by hand:
1. In the Apps Script editor, function dropdown → select **`syncAllRsvpsToGuestList`** → click **Run**.
2. A toast confirms how many rows were reconciled.

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