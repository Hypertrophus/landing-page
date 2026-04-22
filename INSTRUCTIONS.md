# Instructions: Launching a 100% Free Landing Page for Lead Collection

This guide will help you launch a completely free landing page for collecting leads using:
- GitHub Pages (free static hosting)
- Your static HTML page with a form
- Google Sheets (as a backend to collect form submissions)

## Step 1: Prepare Your Landing Page
1. Make sure your landing page (index.html) and any assets (like styles.css) are ready.
2. Your form should have fields for the data you want to collect (e.g., name, email).

## Step 2: Set Up a GitHub Repository
1. Go to [github.com](https://github.com/) and sign in or create a free account.
2. Create a new public repository (e.g., `my-landing-page`).
3. Upload your `index.html` and `assets/` folder to the repository.

## Step 3: Enable GitHub Pages Hosting
1. In your repository, go to **Settings > Pages**.
2. Under **Source**, select the `main` branch and `/ (root)` folder.
3. Save. GitHub will provide a URL like `https://yourusername.github.io/my-landing-page/`.

## Step 4: Set Up Google Sheets for Lead Collection
1. Create a new Google Sheet to store leads.
2. Go to [Google Apps Script](https://script.google.com/) and create a new project.
3. Use the following script to accept POST requests and save data to your sheet:

```javascript
function doPost(e) {
  var sheet = SpreadsheetApp.getActiveSheet();
  var data = JSON.parse(e.postData.contents);
  sheet.appendRow([data.name, data.email]); // Add more fields as needed
  return ContentService.createTextOutput('Success');
}
```

4. In Apps Script, click **Deploy > New deployment**.
5. Select **Web app**:
   - Set **Who has access** to "Anyone".
   - Deploy and copy the Web App URL.

## Step 5: Connect Your Form to Google Sheets
1. In your `index.html`, update the form to submit data via JavaScript `fetch()` to your Apps Script Web App URL.
2. Example JavaScript:

```html
<script>
document.querySelector('form').addEventListener('submit', async function(e) {
  e.preventDefault();
  const formData = new FormData(this);
  const data = Object.fromEntries(formData.entries());
  await fetch('YOUR_WEB_APP_URL', {
    method: 'POST',
    body: JSON.stringify(data),
    headers: { 'Content-Type': 'application/json' }
  });
  alert('Thank you!');
});
</script>
```

Replace `YOUR_WEB_APP_URL` with your actual Apps Script Web App URL.

## Step 6: (Optional) Use a Free Custom Domain
1. Register a free domain at [freenom.com](https://www.freenom.com/) or use a subdomain from a DNS provider.
2. In your domain settings, set a CNAME record pointing to `yourusername.github.io`.
3. In your GitHub repo, add a file named `CNAME` with your custom domain name.
4. Wait for DNS propagation.

## Step 7: Test Everything
1. Visit your GitHub Pages URL (or custom domain).
2. Submit the form and check your Google Sheet for new entries.

---

You now have a 100% free, always-online landing page for collecting leads!
