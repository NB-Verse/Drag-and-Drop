# Drop to Drive

A one-page website that lets you drag and drop any file from your laptop. The file is saved straight into your own Google Drive. Open the same website on your phone, sign in with the same Google account, and the file is there.

There are only two files: `index.html` and this `README.md`. No folders.

---

## What it does

- Drag and drop files anywhere on the page, tap to choose files, or paste a screenshot with Ctrl+V.
- Files are saved in a folder called **Drop to Drive** in your Google Drive.
- The file list refreshes on its own every 20 seconds, so anything you drop on the laptop shows up on your phone without you doing anything.
- For each file you can Open, Download, Copy link, Share (make the link public) or Delete.
- The **Open on phone** button shows a QR code. Scan it with your phone camera to open the site.
- Your files stay private unless you press **Share** on a file.

---

## Setup (about 15 minutes, one time only)

### Step 1 — Put the website on GitHub

1. Go to github.com and create a new repository. Give it any name, for example `drop`. Make it **Public**.
2. Click **Add file → Upload files** and upload `index.html` and `README.md`.
3. Go to **Settings → Pages**. Under "Branch", pick **main** and **/ (root)**, then click **Save**.
4. Wait a minute or two. Your website address will look like this:
   `https://YOUR-GITHUB-USERNAME.github.io/drop/`

Keep this address handy.

### Step 2 — Get a Google Client ID (this lets the site talk to your Drive)

1. Go to **console.cloud.google.com** and sign in with the Google account you want to save files to.
2. At the top, click the project picker and create a **New project**. Name it "Drop to Drive".
3. In the search bar, type **Google Drive API**, open it, and click **Enable**.
4. In the left menu, go to **Google Auth Platform** (on some screens it is called **APIs & Services → OAuth consent screen**).
   - Click **Get started**. App name: "Drop to Drive". Support email: your Gmail.
   - Audience: choose **External**.
   - Contact email: your Gmail. Agree and click **Create**.
5. Go to **Audience** and under **Test users**, click **Add users** and add your own Gmail address.
6. Go to **Clients** and click **Create client**.
   - Application type: **Web application**
   - Name: "Drop to Drive website"
   - Under **Authorized JavaScript origins**, click **Add URI** and enter only the start of your site address, with no folder name and no slash at the end:
     `https://YOUR-GITHUB-USERNAME.github.io`
   - Click **Create**.
7. Copy the **Client ID**. It ends with `.apps.googleusercontent.com`.

### Step 3 — Add the Client ID to the website

1. On GitHub, open `index.html` and click the pencil icon to edit.
2. Near the top of the script you will see:
   ```
   CLIENT_ID: "",
   ```
   Paste your Client ID between the quotes, like:
   ```
   CLIENT_ID: "123456-abcdef.apps.googleusercontent.com",
   ```
3. Click **Commit changes**. Wait a minute for GitHub to update the site.

(If you skip this step, the site will ask you to paste the Client ID the first time you open it. That works too, but you would have to paste it again on your phone.)

### Step 4 — Use it

1. Open your site address on the laptop and click **Sign in with Google**.
2. Google will show a screen saying **"Google hasn't verified this app."** This is normal because the app is your own. Click **Continue**.
3. Tick the box to allow access to files and click **Continue**.
4. Drop a file. Done.
5. On your phone, open the same address (or scan the QR code from **Open on phone**) and sign in with the same Google account.

---

## Good to know

- **Sign in again every hour or so.** Google only keeps this kind of sign-in active for about an hour. When it runs out, the page asks you to sign in again with one tap.
- **The site can only see files it uploaded.** It cannot read the rest of your Google Drive. This keeps your other files safe.
- **Folders:** you can't drop a whole folder. Zip it first.
- **Size limit:** large files are fine. The only limit is the free space in your Google Drive.
- **Deleted files** go to your Google Drive trash and can be restored for 30 days.
- **Sharing:** "Copy link" on a private file only works for you. Press **Share** first if someone else needs to open it.

## If something goes wrong

| What you see | What to do |
|---|---|
| Google says **"Error 400: origin_mismatch"** or **"redirect_uri_mismatch"** | The address in Step 2.6 doesn't match your site. It must be exactly `https://YOUR-GITHUB-USERNAME.github.io` with no `/drop` and no slash at the end. |
| Google says **"Access blocked: app has not completed verification"** | You haven't added your Gmail as a test user. Do Step 2.5. |
| **"Your browser blocked the sign-in pop-up"** | Allow pop-ups for your github.io site in the browser settings. |
| **"Couldn't load Google sign-in"** | Your internet, or the network you're on, is blocking Google. Try a different network. |
| Nothing happens after editing `index.html` | GitHub Pages takes 1–2 minutes to update. Refresh the page after a short wait. |
