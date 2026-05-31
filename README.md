# MatchFlow — Matchmaking Web App

This repo contains a polished static matchmaking frontend and a Google Apps Script backend for saving submissions to Google Sheets.

## Project files

# Project files

```
just for fun/
├── index.html         Main static web app
├── apps-script.gs     Google Apps Script backend for Sheets
├── profile.jpg        Local reveal image
├── vercel.json        Vercel static deployment config
└── README.md          This guide
```

## What was fixed

1. Redesigned the multi-step form with clear step cards and progress tracking.
2. Converted inputs to selection-based controls for matching requirements.
3. Rebuilt submission flow with a processing overlay and reveal page.
4. Fixed the profile card to use dynamic values and a stable local image fallback.
5. Added Google Sheets backend logic with header validation and append-only storage.

## Deployment

### Vercel

1. Push this folder to a GitHub repo.
2. Create a new Vercel project.
3. Import the repo and deploy.

### Netlify

1. Create a new site from Git.
2. Select the repo.
3. Deploy the static site.

No server is required. `index.html` is a static front end.

## Google Sheets setup

### 1. Create the spreadsheet

1. Open Google Sheets.
2. Create a new sheet.
3. Name the first worksheet `Responses` or leave the default.

### 2. Create the Apps Script project

1. Go to `https://script.google.com`.
2. Create a new project.
3. Replace the default code with the contents of `apps-script.gs`.
4. Save the script.

### 3. Deploy as Web App

1. Click `Deploy` → `New deployment`.
2. Select `Web app`.
3. Execute as: `Me`.
4. Who has access: `Anyone`.
5. Deploy and copy the Web App URL.

### 4. Configure the frontend

1. Open `index.html`.
2. Replace the placeholder value in the `SHEET_URL` constant with your Web App URL.

```js
const SHEET_URL = "https://script.google.com/macros/s/YOUR_SCRIPT_ID/exec";
```

### 5. Test the submission

1. Deploy the site.
2. Complete the form.
3. Submit and verify that the new row appears in your Google Sheet.

## Apps Script backend behavior

The backend does the following:

- Ensures header row exists with:
  - `Timestamp`, `Profession`, `Age`, `Height`, `Personality`, `Lifestyle`, `Salary`, `Notes`
- Appends each submission as a new row.
- Does not overwrite existing data.

## Debug checklist

- [ ] Confirm `SHEET_URL` is replaced with your script URL.
- [ ] Confirm the Google Apps Script is deployed with access `Anyone`.
- [ ] Confirm the sheet contains the correct header row.
- [ ] Confirm form navigation works across all steps.
- [ ] Confirm the reveal page appears after submit.
- [ ] Confirm the profile image loads from `profile.jpg` and falls back if needed.

## Notes

- The form includes a modern dark UI and minimal animations.
- The frontend uses `fetch(..., { mode: 'no-cors' })` to submit to Google Apps Script without a server.
- This project is ready for Vercel or Netlify deployment.
