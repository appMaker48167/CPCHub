# Resource Library (GitHub-powered)

A lightweight, mobile-friendly web app that lists files from a GitHub repository, supports search & category filtering, and lets you **send/share** resource links via the device share sheet or email.

## Quick Start (Public Repo)
1. Edit `config.js` and set:
   ```js
   const CONFIG = {
     REPO_OWNER: "your-github-username",
     REPO_NAME: "your-resources-repo",
     BRANCH: "main",
     GITHUB_TOKEN: null
   };
   ```
2. Put your resources in your GitHub repo. Organize by **folders** to create categories (e.g., `Assessments/Guide.pdf`, `Coaching/Checklist.docx`, etc.).
3. Deploy this app (the files in this folder) to **GitHub Pages**:
   - Create a new repo (e.g., `resource-library-app`)
   - Upload these files
   - Settings → Pages → Select Branch (e.g., `main` / `/root`) → Save
   - Your app will be live at: `https://YOUR_USER.github.io/resource-library-app/`

## Sharing / Sending Files
- **Share button** uses the browser's **Web Share API** when available (mobile-first). Falls back to copying link.
- **Email button** opens the default mail client with a prefilled subject and body containing the file link.
- The app links to:
  - Binary files directly from `raw.githubusercontent.com`
  - Text files via GitHub "blob" view (with a "View Raw" option)

## Private Repos (Important)
Client-side tokens in `config.js` are **not secure** if your app is public. Options:
- Make your **resource repo public**, but only include materials safe to share publicly.
- Or deploy a tiny **secure proxy** (e.g., Cloudflare Worker, Vercel Function) that holds your GitHub token server-side and forwards limited API calls to this app.
- Or keep the UI private behind an authenticated host (e.g., GitHub Enterprise, internal SSO).

### Example Proxy (Concept)
- Client → `/api/tree` → Proxy adds `Authorization: Bearer <token>` → Forwards to GitHub REST → Returns sanitized JSON.
- Lock it down to specific endpoints and repos only.

## Rate Limits
- Unauthenticated GitHub API requests are limited to ~60/hour (per IP). If your team is larger or usage is high, use the proxy approach above.

## Customize
- Improve category logic (deeper nesting)
- Add tags via a `manifest.json` file in your repo
- Add icons, theming, download analytics, etc.

## License
MIT
