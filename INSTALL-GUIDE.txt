# INSTALL GUIDE — Inbox Automation Outlook Add-in
# =====================================================
# Before you can sideload the add-in, the files must be
# hosted on an HTTPS server Outlook can reach.
# Choose ONE of the two options below.
# =====================================================


════════════════════════════════════════════════════════
OPTION 1 — GitHub Pages (Free, permanent, no coding)
════════════════════════════════════════════════════════

1. Go to https://github.com and sign in (or create a free account)

2. Click the "+" icon → "New repository"
   - Name it: outlook-automation-addin
   - Set to PUBLIC
   - Click "Create repository"

3. Upload the files:
   - Click "uploading an existing file"
   - Drag all 3 files into the box: manifest.xml, taskpane.html, commands.html
   - Click "Commit changes"

4. Enable GitHub Pages:
   - Click "Settings" tab → "Pages" in the left sidebar
   - Under "Source" select "Deploy from a branch"
   - Branch: main  /  Folder: / (root)
   - Click "Save"
   - Wait ~2 minutes, then your site is live at:
     https://YOUR-GITHUB-USERNAME.github.io/outlook-automation-addin/

5. Update manifest.xml with YOUR URL:
   - Open manifest.xml in Notepad
   - Find and replace ALL 3 instances of:
       https://localhost:3000/taskpane.html
     with:
       https://YOUR-GITHUB-USERNAME.github.io/outlook-automation-addin/taskpane.html
   - Also replace:
       https://localhost:3000/commands.html
     with:
       https://YOUR-GITHUB-USERNAME.github.io/outlook-automation-addin/commands.html
   - Save the file
   - Re-upload the updated manifest.xml to GitHub

6. Now proceed to "SIDELOAD INTO OUTLOOK" below ↓


════════════════════════════════════════════════════════
OPTION 2 — Run locally on your computer (Easiest, but
           Outlook must be on the same machine)
════════════════════════════════════════════════════════

1. Install Node.js from https://nodejs.org (LTS version)

2. Open Command Prompt or Terminal, navigate to the folder
   where you saved the 3 add-in files:
     cd C:\Users\YourName\Downloads\outlook-addin

3. Run this command to start a local HTTPS server:
     npx office-addin-dev-server start

   OR if that doesn't work:
     npx http-server -p 3000 --ssl --cert localhost.crt --key localhost.key

   The server runs at https://localhost:3000
   (manifest.xml already points here — no changes needed)

4. Leave the Command Prompt open while using Outlook

5. Now proceed to "SIDELOAD INTO OUTLOOK" below ↓


════════════════════════════════════════════════════════
SIDELOAD INTO OUTLOOK (do this after hosting is set up)
════════════════════════════════════════════════════════

Windows — Outlook Desktop:
  1. Open Outlook
  2. Click FILE in the top-left ribbon
  3. Click "Manage Add-ins" → your browser opens
  4. In the browser, click "My add-ins" (left sidebar)
  5. Scroll to bottom → "Custom add-ins"
  6. Click "+ Add a custom add-in" → "Add from file…"
  7. Select your manifest.xml file
  8. Click "Install" on the warning dialog
  9. CLOSE and REOPEN Outlook
  10. Open any email → "Inbox Automation" appears in the ribbon!

Mac — Outlook Desktop:
  1. Open Outlook
  2. Click TOOLS in the menu bar (top of screen)
  3. Click "Add-ins…"
  4. Click "+" at the bottom left
  5. Select manifest.xml
  6. Restart Outlook


════════════════════════════════════════════════════════
TROUBLESHOOTING
════════════════════════════════════════════════════════

"Add-in won't load / blank panel"
→ The taskpane.html URL in manifest.xml is not reachable.
  Double-check your GitHub Pages URL is correct and live.
  Try opening the taskpane.html URL directly in a browser — it should load.

"Manifest validation error"
→ Make sure you updated ALL URL references in manifest.xml (there are 3).

"I don't see Inbox Automation in the ribbon"
→ Close and fully reopen Outlook. Also check that you opened an email first —
  the button only appears in the reading/email view, not in the calendar or main view.

"NET::ERR_CERT_INVALID (local server)"
→ Open https://localhost:3000 in Chrome, click Advanced → Proceed anyway.
  This trusts the local certificate for Outlook to load the add-in.

Still stuck? Open the add-in manager URL directly:
  https://aka.ms/olksideload
