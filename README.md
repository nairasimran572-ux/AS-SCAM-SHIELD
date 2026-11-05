# CyberGuard Pro

A multi-page cybersecurity education platform built with HTML, CSS and vanilla JavaScript. Includes an educational threat-warning checker, local password-strength estimator, browser-based password generator, learning checklist, quiz, local progress reports, and optional Gemini AI assistant.

## Project files

- `index.html` — home page
- `dashboard.html` — overview and learning checklist
- `detector.html` — local warning checks and optional AI analysis
- `assistant.html` — AI cybersecurity Q&A
- `password-lab.html` — local password estimator and generator
- `learning.html` — five learning topics
- `quiz.html` — beginner/intermediate/advanced quiz
- `reports.html` — locally saved quiz history
- `assets/css/style.css` — shared responsive design
- `assets/js/` — page logic and AI endpoint configuration
- `worker/worker.js` — secure Gemini API proxy for Cloudflare Workers

## 1. Preview locally

You can open `index.html` directly, but a local web server is recommended. In VS Code, install the Live Server extension, right-click `index.html`, and choose **Open with Live Server**.

## 2. Publish the website on GitHub Pages

1. Sign in to GitHub and create a new public repository, for example `cyberguard-pro`.
2. Extract this ZIP file on your computer.
3. Open the extracted project folder. Upload the *contents* of the folder (not an extra nested folder) into the repository. Keep the `assets` and `worker` folders.
4. Commit the files to the `main` branch.
5. Open repository **Settings → Pages**.
6. Under **Build and deployment**, choose **Deploy from a branch**.
7. Select branch `main` and folder `/ (root)`, then click **Save**.
8. Wait for GitHub Pages to finish deploying. Your site will be at `https://YOUR-USERNAME.github.io/cyberguard-pro/`.
9. If you use a repository name other than `cyberguard-pro`, the URL will use that repository name.

## 3. Enable Gemini AI securely (optional)

The static website works without AI. The threat detector's local quick-check, password lab, lessons, quiz and reports do not require an API key. The AI assistant and AI threat analysis need a Cloudflare Worker.

1. Create a Gemini API key through Google AI Studio. Keep it private.
2. Create/sign in to a Cloudflare account and open **Workers & Pages**.
3. Create a Worker named `cyberguard-ai`.
4. Replace the starter Worker code with the complete contents of `worker/worker.js`, then deploy.
5. In the Worker settings, add an environment variable/secret named `GEMINI_API_KEY` and paste your Gemini API key as its secret value. Do not put the key in this repository.
6. Add a variable named `ALLOWED_ORIGIN` with your exact GitHub Pages origin, for example `https://YOUR-USERNAME.github.io`. Do not include the repository path or a trailing slash. This is a browser restriction, not authentication; use provider-side quotas/rate limits for production.
7. Copy the deployed Worker URL, for example `https://cyberguard-ai.YOUR-SUBDOMAIN.workers.dev`.
8. Open `assets/js/config.js` and replace `https://YOUR_WORKER_URL.workers.dev` with your actual Worker URL.
9. Commit and push the updated `config.js` file to GitHub. Wait for Pages to redeploy.
10. Open the site and test the AI assistant with a harmless question.

### Important AI and security notes

- Never commit a Gemini API key to GitHub or place it in browser JavaScript.
- The Worker is a basic proxy, not a complete production security gateway. Add rate limiting, abuse monitoring and suitable usage quotas before public launch.
- Set `ALLOWED_ORIGIN` to your exact GitHub Pages origin. CORS alone does not prevent non-browser clients from calling a public endpoint.
- AI answers can be inaccurate. Do not use the detector as proof that a message or URL is safe or malicious.
- Do not submit passwords, one-time codes, recovery codes, private messages or sensitive personal data to the AI.
- This project does not scan URLs, open links, inspect files, or provide antivirus protection.
- Local progress uses browser `localStorage`; it is not synced between devices and may be cleared by the browser.

## 4. Customization

- Change colors in the `:root` section at the top of `assets/css/style.css`.
- Edit quiz questions in `assets/js/quiz.js`.
- Edit lesson content in `assets/js/learning.js`.
- Edit page navigation in `assets/js/app.js`.
- Change the AI model in `worker/worker.js` if you choose a supported Gemini model.

## 5. Troubleshooting

- **CSS or images do not load:** keep the `assets` folder at the repository root and preserve the folder names.
- **GitHub Pages shows 404:** check Settings → Pages, branch `main`, folder `/ (root)`, and ensure `index.html` is at the repository root.
- **AI says it is not configured:** check `assets/js/config.js`, the Worker URL, and the Worker deployment.
- **AI returns an error:** check the `GEMINI_API_KEY` secret, API availability and quota, then inspect Worker logs.
- **Changes are not visible:** wait for deployment to finish and refresh the browser with Ctrl+F5.

## License

Use and modify this starter project for learning. Add your own attribution and review all third-party service terms before public deployment.
