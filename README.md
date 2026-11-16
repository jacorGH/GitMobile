<p align="center">
  <img src="icons/icon-rounded.svg" width="120" alt="GitMobile icon">
</p>

<h1 align="center">GitMobile</h1>

<p align="center">
  Push files, folders and whole projects to GitHub from your iPhone.<br>
  A single-file web app: no install, no server, no build step.
</p>

<p align="center">
  <img alt="License: MIT" src="https://img.shields.io/badge/license-MIT-2f6fe4">
  <img alt="Platform" src="https://img.shields.io/badge/platform-iPhone%20%C2%B7%20any%20browser-1b3b8f">
  <img alt="Dependencies" src="https://img.shields.io/badge/dependencies-none-0f1722">
</p>

---

## Why

Editing code on an iPhone (in Textastic or similar) is easy. Getting a project with nested folders onto GitHub is not: GitHub's mobile app can't upload folders, and iOS hides folders whose names start with a dot. GitMobile fills that gap. Zip your project in the Files app, pick the ZIP, review what changes, and push it all in one commit.

## Features

**Uploading**
- Push one or several ZIPs at once, plus loose files or (on desktop) whole folders
- Full nested folder structure is preserved
- Review screen marks every file as New, Changed, Unchanged or Delete, compared byte-for-byte against the repo
- Tap any file in the review to see a line-by-line diff before pushing
- "Unwrap" option drops a ZIP's top folder so contents land where you want
- Optional mirror mode removes repo files that aren't in your upload, except paths you protect (for example `audio/` or `app/keys/`), kept per repository
- A file saved twice on iPhone ("data 2.json", "data (1).json") goes back to its name in the repo, with a switch to keep the number
- `_github`, `_gitignore`, `_nojekyll` and similar are renamed to their dot-names, working around iOS hiding dot-folders
- However large, a push is **one commit**, so GitHub Pages deploys once and workflows run once. Big uploads are sent in parts of 50 files, wait out GitHub's rate limits, and if interrupted, Push again skips every file already uploaded
- **Quick push:** remembers which repo, branch and folder each ZIP goes to, so repeat pushes take one tap

**Browsing and editing**
- File browser with size, last commit message and "updated 2 days ago" for every file and folder
- Code editor with syntax colors (HTML, JS, CSS, JSON, YAML, Markdown), line numbers, auto-indent, find and replace, and a symbol key bar for the iPhone keyboard
- Image and text previews, file history, and one-tap restore of any older version
- Select multiple items to move or delete them in one commit
- Moving a folder onto one with the same name merges them, with Replace / Keep both / Skip for clashing files
- Download any repo or folder as a ZIP to bring it back into Textastic

**Repos, Pages and Actions**
- Create new repositories, optionally with GitHub Pages turned on
- Configure Pages from a branch or a GitHub Actions workflow, with a starter deploy workflow included
- Live GitHub Actions status after every push: running, failed (with the failing step and log), or "New version is live"
- **Run a workflow** by hand (any workflow with `workflow_dispatch`), answering its inputs, then watch the new run
- **Downloads**: a finished run's artifacts (an app build, a report), saved to Files through the share sheet. Files over
  320 MB (two app builds together) are handed to Safari, which downloads them straight to Files without holding them in memory
  (sign in to github.com in Safari once)
- **Secrets for Actions**: add, replace and delete repository secrets, typed or read from a file (a `.p8` key, a JSON). Each value is sealed on the phone with the repository's public key before it is sent
- Re-run or cancel workflow runs
- Releases with suggested version numbers and auto-written notes
- Copy a repo as the starting point for a new project
- Branch switching

## Getting started

1. Host it. Push this repo to GitHub and turn on GitHub Pages (Settings → Pages → Deploy from branch → `main`, `/ (root)`), or open `index.html` from any web host.
2. On your iPhone, open the site in Safari, tap **Share → Add to Home Screen**. It runs full screen like an app.
3. Create a token at [github.com/settings/tokens](https://github.com/settings/tokens/new?scopes=repo,workflow&description=GitMobile) with the **repo** and **workflow** scopes, and paste it into GitMobile.

Fine-grained tokens also work with these repository permissions: Contents, Workflows, Pages and Administration (to create repos) set to read and write, Actions set to read (write to re-run or start workflows), and Secrets set to read and write (to manage secrets).

## Pushing a project from iPhone

1. In the Files app, long-press your project folder and tap **Compress**.
2. In GitMobile, open the repo, tap **Add → Upload ZIPs**, and pick the ZIP.
3. Check the review, then tap **Push**.

Keep GitMobile on screen during large pushes. iOS pauses web pages in the background; if a push is interrupted, tap Push again and it continues with what's left.

## Privacy and security

- Your token is stored only in your browser's local storage and is sent only to `api.github.com`.
- There is no server, analytics or tracking. The only outside scripts are JSZip, loaded from cdnjs when you first open a ZIP, and TweetNaCl, loaded from cdnjs the first time you save a secret (it seals the value before it leaves the phone).
- Anyone with your token can act on your repos, so use an expiration date and revoke it on GitHub if your phone is lost.

## Project structure

```
index.html          The entire app (HTML, CSS and JavaScript)
manifest.json       Home-screen app settings
icons/              App icon (SVG master and PNG sizes)
README.md
LICENSE
```

## License

[MIT](LICENSE) © 2026 Jacob Cooper
