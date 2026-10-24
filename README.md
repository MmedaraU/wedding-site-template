# Wedding Website Template

A custom, static wedding site. No build step, no frameworks, no dependencies. Just HTML, CSS, and vanilla JS.

## The Files
- `index.html` — The main site.
- `404.html` — The custom "page not found" page.
- `README.md` — This file.

## How to make changes

### 1. Text and Content
Open `index.html` in any text editor (VS Code, Notepad, etc.). The content is written directly in the HTML. 
- To change the names, search for `Mmedara & Ikedinachi`.
- To change the story, search for `<div class="story__text"`.
- To change the menu or travel details, search for `<div class="feast">` or `<div class="travel">`.

### 2. Photos
The site currently uses placeholder images from `picsum.photos`. 
To use real photos:
1. Create an `images` folder next to `index.html`.
2. Put your photos in it.
3. In `index.html`, find the `<img>` tags and replace the `src="https://picsum.photos/..."` with `src="images/your-photo.jpg"`.
4. *Note:* Keep the `aspect-ratio` in mind. The hero photo is portrait (4:5), the story photo is portrait (3:4), and the gallery photos are uniform (4:5).

### 3. The Countdown
The countdown targets **16 December 2028 at 14:30 WAT**. 
To change it, find this line in the `<script>` block at the bottom of `index.html`:
`const TARGET = Date.UTC(2028, 11, 16, 13, 30, 0);`
*(Remember: Months are 0-indexed, so `11` is December. Time is in UTC).*

### 4. The Forms (RSVP & Letters)
Both forms submit silently to a Google Sheet using a Google Apps Script.

**If the forms stop working:**
1. Check the `SCRIPT_URL` variable at the very top of the `<script>` block in `index.html`. It must be the deployed `/exec` URL.
2. Ensure your Google Sheet has two tabs named exactly `RSVP` and `Letters`.
3. Ensure the headers in Row 1 of those tabs exactly match: `Timestamp`, `Name`, `Guests`, `Notes`, `Song` and `Timestamp`, `Name`, `Message`.
4. If you need to redeploy the Apps Script, go to `Extensions > Apps Script` in your Google Sheet, click `Deploy > Manage Deployments`, and create a new version.

**To view responses:** Open the Google Sheet linked to the Apps Script. Every submission will appear in a new row.

## Design System
If you need to match the design in future edits, here are the core tokens:

**Colors**
- Background (Wine): `#2A0E14`
- Text (Ivory): `#F5EFE6`
- Accent 1 (Coral): `#E24E42`
- Accent 2 (Gold): `#B8935A`

**Fonts (Google Fonts)**
- Display: `Fraunces` (uses variable settings for optical size and softness)
- Body: `Newsreader`
- Sans/UI: `Inter`

## Deploying
Because this is pure static HTML/CSS/JS, you can host it anywhere for free:
- **Netlify Drop:** Drag the folder containing your files onto [app.netlify.com/drop](https://app.netlify.com/drop).
- **Vercel:** Run `vercel` in the terminal.
- **GitHub Pages:** Push to a repo and enable Pages in settings.