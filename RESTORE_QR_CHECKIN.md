# How to Restore QR Code Check-in

Currently, the QR code generation and scanner check-in logic are disabled to simplify the guest emails. When you are ready to turn it back on, follow these steps.

## Step 1: Uncomment the QR Code in the Apps Script
Open your Google Apps Script editor.

1. Look for the **Guest Emails** section inside `doPost`.
2. Find and **uncomment** these two lines (remove the `//` at the start):
```javascript
        const qrData = encodeURIComponent(e.parameter.Name + ' | ' + emailVal);
        const qrCodeUrl = `https://api.qrserver.com/v1/create-qr-code/?size=200x200&data=${qrData}`;
```
3. Find the HTML block inside `emailHtml` and **uncomment** it:
```javascript
              <div style="margin: 0 0 32px 0; padding: 20px; border-top: 1px solid ${EMAIL_CONFIG.gold}; border-bottom: 1px solid ${EMAIL_CONFIG.gold};">
                <p style="margin: 0 0 12px 0; font-family: Georgia, serif; font-size: 16px; font-weight: bold; color: ${EMAIL_CONFIG.wine};">
                  Your Check-in Pass
                </p>
                <p style="margin: 0 0 16px 0; font-family: Georgia, serif; font-size: 14px; line-height: 1.6; color: ${EMAIL_CONFIG.wine};">
                  Please present this QR code to the ushers on arrival for a speedy check-in.
                </p>
                <img src="${qrCodeUrl}" alt="Your Check-in QR Code" width="180" height="180" style="display: block; margin: 0 auto; border: 4px solid ${EMAIL_CONFIG.ivory}; border-radius: 4px;">
              </div>
```

## Step 2: Ensure Check-ins are handled in `doGet`
Because the scanner uses a `GET` request (to avoid the `no-cors` bug), the check-in logic must be inside `doGet`. 

Your current `doGet` only fetches letters. Replace your `doGet` function with this combined version:

```javascript
function doGet(e) {
  // 1. Handle Scanner Check-ins
  if (e.parameter.formType === 'CheckIn') {
    try {
      const guestData = (e.parameter.GuestData || '').toString().trim();
      const doc = SpreadsheetApp.getActiveSpreadsheet();
      const sheet = doc.getSheetByName('RSVP');
      
      if (!sheet) throw new Error('RSVP sheet not found.');
      
      const data = sheet.getDataRange().getValues();
      const headers = data[0];
      const checkedInIndex = headers.indexOf('CheckedIn');
      
      if (checkedInIndex === -1) throw new Error('CheckedIn column not found.');
      
      let found = false;
      for (let i = 1; i < data.length; i++) {
        const rowName = data[i][1].toString(); 
        if (guestData.includes(rowName) && rowName !== '') {
          sheet.getRange(i + 1, checkedInIndex + 1).setValue('Yes - ' + new Date().toLocaleTimeString());
          found = true;
          break;
        }
      }
      
      if (!found) {
        return ContentService.createTextOutput(JSON.stringify({ result: 'error', message: 'Guest not found' }))
          .setMimeType(ContentService.MimeType.JSON);
      }
      
      return ContentService.createTextOutput(JSON.stringify({ result: 'success', message: 'Checked in successfully' }))
        .setMimeType(ContentService.MimeType.JSON);
        
    } catch (error) {
      return ContentService.createTextOutput(JSON.stringify({ result: 'error', message: error.toString() }))
        .setMimeType(ContentService.MimeType.JSON);
    }
  }

  // 2. Handle Fetching Letters (Default)
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName('Letters');
  if (!sheet) return ContentService.createTextOutput(JSON.stringify([])).setMimeType(ContentService.MimeType.JSON);
  
  const data = sheet.getDataRange().getValues();
  data.shift(); // Remove header row
  
  const letters = data
    .filter(row => row[1] && row[2]) // Must have a Name and Message
    .map(row => ({ name: row[1], message: row[2] }))
    .reverse() // Show newest first
    .slice(0, 6); // Only keep the 6 most recent

  return ContentService
    .createTextOutput(JSON.stringify(letters))
    .setMimeType(ContentService.MimeType.JSON);
}
```

## Step 3: Redeploy
1. Save the Apps Script.
2. Go to **Deploy > Manage deployments**.
3. Click the pencil icon, select **New version**, and click **Deploy**.

## Step 4: The Scanner Page
The `scanner.html` file is already in your folder and is ready to go. On the wedding day, just open `yourdomain.com/scanner.html` on the ushers' phones and allow camera access.