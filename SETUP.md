# Reply Tracker — Setup Guide

Do this once. After that, just open Outlook — nothing to start or maintain.

---

## Step 1 — Put the files on GitHub (5 min)

1. Go to https://github.com/new
2. Repository name: `reply-tracker`
3. Set it to **Public**
4. Click **Create repository**
5. Upload all files from this folder (drag & drop them onto the GitHub page)
6. Go to **Settings** → **Pages** → Source: **Deploy from a branch** → Branch: `main` → Save
7. Wait ~1 min → your add-in is now live at:
   **https://sabit12.github.io/reply-tracker**

---

## Step 2 — Create an Azure AD App (5 min, one time forever)

This lets the add-in read your Outlook inbox on your behalf.

1. Go to https://portal.azure.com
2. Search **"App registrations"** → click **New registration**
3. Name: `Reply Tracker`
4. Supported account types: **Accounts in any organizational directory and personal Microsoft accounts**
5. Redirect URI: choose **Single-page application (SPA)** → paste:
   `https://sabit12.github.io/reply-tracker/taskpane.html`
6. Click **Register**
7. On the next screen, copy the **Application (client) ID** (looks like `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`)

### Add permissions
1. Left menu → **API permissions** → **Add a permission** → **Microsoft Graph** → **Delegated permissions**
2. Search and add: `Mail.Read`
3. Search and add: `User.Read`
4. Click **Add permissions**

---

## Step 3 — Paste your Client ID into the add-in

1. Open `taskpane.html` in Notepad
2. Find this line near the top:
   ```
   const CLIENT_ID = 'YOUR_CLIENT_ID_HERE';
   ```
3. Replace `YOUR_CLIENT_ID_HERE` with the ID you copied in Step 2
4. Save the file
5. Go back to GitHub → open `taskpane.html` → click the pencil (edit) icon → paste the updated content → commit

---

## Step 4 — Install the add-in in Outlook (one time)

### Outlook on the Web
1. Go to https://outlook.office.com
2. Open any email → click **…** (More actions) in the toolbar
3. Click **Get Add-ins**
4. Go to **My add-ins** → **Add a custom add-in** → **Add from file…**
5. Upload `manifest.xml` from this folder
6. Done — **"Unreplied Emails"** button now appears in your Outlook toolbar

### Outlook Desktop (Windows)
1. Open Outlook → **File** → **Manage Add-ins** (opens Outlook Web)
2. Follow the same steps above

---

## You're done!

After every reboot — just open Outlook. The add-in loads from GitHub automatically. No server, nothing to start.

- Open any email → click **Unreplied Emails** in the ribbon
- Sign in with Microsoft the first time (never again after that)
- See all emails where you were in To/CC but haven't replied
