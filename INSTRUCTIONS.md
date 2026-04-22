Instructions: Always-Online Lead Collection (100% Free)
This architecture uses GitHub for hosting and Google as the backend. It is designed to be zero-cost, zero-maintenance, and bypass modern browser security restrictions.

Step 1: Prepare Your Google Sheet
Create a new Google Sheet.

In the first row, create these headers: Date, name, email.

Go to Extensions > Apps Script.

Delete all existing code and paste this "no-fail" script:

JavaScript
function doPost(e) {
  const lock = LockService.getScriptLock();
  lock.tryLock(10000); // Wait for 10s to avoid overlap

  try {
    const doc = SpreadsheetApp.getActiveSpreadsheet();
    const sheet = doc.getActiveSheet();
    
    // Extract data from the form
    const name = e.parameter.name; 
    const email = e.parameter.email;
    const date = new Date();

    // Append data to the sheet
    sheet.appendRow([date, name, email]);

    return ContentService
      .createTextOutput(JSON.stringify({ "result": "success" }))
      .setMimeType(ContentService.MimeType.JSON);

  } catch (err) {
    return ContentService
      .createTextOutput(JSON.stringify({ "result": "error", "error": err.toString() }))
      .setMimeType(ContentService.MimeType.JSON);
  } finally {
    lock.releaseLock();
  }
}
Step 2: Deploy the Backend
In Apps Script, click Deploy > New deployment.

Select Web app.

Set Execute as: Me.

Set Who has access: Anyone. (CRITICAL: Do not select "Anyone with a Google account").

Click Deploy. Authorize the permissions (Click Advanced > Go to [Project Name] if warned).

Copy the Web App URL.

Step 3: Connect Your HTML Form
Update your index.html with the following logic. This uses no-cors mode to ensure Google doesn't block the request.

HTML
<form id="lead-form">
  <input type="text" name="name" placeholder="Name" required>
  <input type="email" name="email" placeholder="Email" required>
  <button type="submit" id="submit-btn">Join Waitlist</button>
</form>

<script>
  const scriptURL = 'YOUR_WEB_APP_URL_HERE'; // PASTE YOUR URL HERE
  const form = document.getElementById('lead-form');
  const btn = document.getElementById('submit-btn');

  form.addEventListener('submit', e => {
    e.preventDefault();
    btn.disabled = true;
    btn.innerText = "Saving...";

    fetch(scriptURL, { 
      method: 'POST', 
      body: new FormData(form),
      mode: 'no-cors' // Allows the request to succeed without CORS errors
    })
    .then(() => {
      alert("Success! You're on the list.");
      btn.innerText = "Joined!";
      form.reset();
    })
    .catch(error => {
      console.error('Error!', error.message);
      btn.disabled = false;
      btn.innerText = "Try Again";
    });
  });
</script>
Step 4: Host on GitHub Pages
Create a public repository on GitHub.

Upload your index.html and any CSS/images.

Go to Settings > Pages.

Set the Source to Deploy from a branch and select main / root.

Your site is now live at https://yourusername.github.io/repo-name/.