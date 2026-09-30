# The Complete Beginner's Guide to Software Versioning (SemVer)

A universal reference for developers, open-source maintainers, and beginners on how software versioning works across **Mobile Apps, Desktop Software, Web Applications, Browser Extensions, and Backend Libraries**.

---

## Table of Contents
1. [What is Semantic Versioning (SemVer)?](#1-what-is-semantic-versioning-semver)
2. [The Three Numbers Explained](#2-the-three-numbers-explained)
3. [The Golden Rule: The Reset Rule](#3-the-golden-rule-the-reset-rule)
4. [Real-World Decision Matrix](#4-real-world-decision-matrix)
5. [Common Beginner Mistakes to Avoid](#5-common-beginner-mistakes-to-avoid)
6. [How Versioning Works Across Different Platforms](#6-how-versioning-works-across-different-platforms)
   - [📱 Mobile Apps (Android & iOS)](#-mobile-apps-android--ios)
   - [💻 Desktop / PC Applications (Windows, macOS, Linux)](#-desktop--pc-applications-windows-macos-linux)
   - [🌐 Web Applications & SaaS](#-web-applications--saas)
   - [🧩 Browser Extensions (Chrome, Edge, Firefox)](#-browser-extensions-chrome-edge-firefox)
   - [📦 Libraries & Package Managers (NPM, Python, Rust)](#-libraries--package-managers-npm-python-rust)
7. [Pre-Releases and Beta Testing](#7-pre-releases-and-beta-testing)
8. [Universal Step-by-Step Release Checklist](#8-universal-step-by-step-release-checklist)
9. [How to Write Clean Changelogs](#9-how-to-write-clean-changelogs)

---

## 1. What is Semantic Versioning (SemVer)?

When you download software or install an app, you see numbers like `1.0.0`, `2.4.1`, or `1.1.0`. These numbers are not random—they communicate **what changed** inside the software to users, developers, app stores, and automated systems.

Most modern software follows the universal standard called **Semantic Versioning (SemVer 2.0.0)**:

```text
       1    .    0    .    5
       │         │         │
    [MAJOR]   [MINOR]   [PATCH]
```

---

## 2. The Three Numbers Explained

| Segment | Position | Name | When Do You Change It? | What Does It Signal? | Example |
| :---: | :---: | :---: | :--- | :--- | :---: |
| **First** | `X._._` | **MAJOR** | **Breaking Changes**: The software was rewritten, incompatible API changes occurred, old features were removed, or users must adapt to a major workflow overhaul. | Big milestone release. Old data, integrations, or habits might require updating. | `1.0.0` ➔ `2.0.0` |
| **Middle** | `_.Y._` | **MINOR** | **New Features & UI Improvements**: Added new capabilities, redesigned layouts, or introduced significant enhancements without breaking existing features. | Noticeable upgrade. Users get new tools or better experiences. **Resets PATCH to 0!** | `1.0.5` ➔ `1.1.0` |
| **Last** | `_._.Z` | **PATCH** | **Bug Fixes & Maintenance**: Fixed bugs, improved performance, patched security issues, or corrected typos. | Stability update. Safe drop-in upgrade with no new features or workflow changes. | `1.0.5` ➔ `1.0.6` |

---

## 3. The Golden Rule: The Reset Rule

> 💡 **The Reset Rule**: Whenever a higher-level number increases, **every number to its right MUST reset back to `0`**.

### Why `1.0.5` Becomes `1.1.0` (and NEVER `1.1.6`):

1. **Scenario A — You only fixed bugs or errors:**
   - Keep `MAJOR` (`1`) and `MINOR` (`0`) unchanged.
   - Increment `PATCH`: `5` ➔ `6`.
   - Next Version: **`1.0.6`**.

2. **Scenario B — You added a new feature or redesigned the UI:**
   - Increment `MINOR`: `0` ➔ `1`.
   - **The reset rule activates**: The `PATCH` counter resets from `5` to **`0`**.
   - Next Version: **`1.1.0`**.

3. **Why `1.1.6` is a mistake:**
   - Jumping both `MINOR` (`0` ➔ `1`) and `PATCH` (`5` ➔ `6`) at once skips versions.
   - To store reviewers, users, and package managers, jumping to `1.1.6` implies that versions `1.1.0`, `1.1.1`, `1.1.2`, `1.1.3`, `1.1.4`, and `1.1.5` were already released and forgotten.

---

## 4. Real-World Decision Matrix

Use this cheat sheet to choose your next version number:

| Current Version | What You Changed in Your Software | Next Version | Rationale |
| :---: | :--- | :---: | :--- |
| `1.0.0` | Fixed a crash bug or typo | **`1.0.1`** | Small patch |
| `1.0.5` | Fixed a button alignment issue and resolved a memory leak | **`1.0.6`** | Pure bug fix / patch |
| `1.0.5` | Added Dark Mode, redesigned navigation, and improved UI | **`1.1.0`** | UI/UX refinement & new capability (PATCH resets to 0) |
| `1.1.0` | Discovered and fixed a bug in the new Dark Mode | **`1.1.1`** | First patch in the 1.1.x series |
| `1.1.3` | Added Cloud Sync and Google Drive export | **`1.2.0`** | Major new feature added without breaking existing features |
| `1.9.0` | Added another new feature (e.g., PDF export) | **`1.10.0`** | Version numbers are not decimals! (10 is after 9) |
| `1.14.2` | Completely rewrote database engine, changed API endpoints, or rebuilt app from scratch | **`2.0.0`** | Major breaking change / new generation |

---

## 5. Common Beginner Mistakes to Avoid

### ❌ Mistake 1: Treating version numbers like decimals
- In mathematics: `1.9` is bigger than `1.10`.
- **In software versioning: `1.10.0` comes AFTER `1.9.0`!**
- The dots are separators between integers, not decimal points. You can have `1.9.0` ➔ `1.10.0` ➔ `1.11.0` ➔ `1.99.0` ➔ `1.100.0`.

### ❌ Mistake 2: Incrementing multiple numbers at the same time
- Never change `1.0.3` to `2.1.4`. Only increment the single highest segment that changed and reset everything to its right.

### ❌ Mistake 3: Bumping MAJOR for small visual changes
- Don't jump from `1.0.0` to `2.0.0` just because you changed a button color. Reserve `MAJOR` bumps for true generational upgrades or breaking changes.

### ❌ Mistake 4: Staying on `0.x.x` forever
- `0.y.z` is used during initial development when anything can change at any time. Once your software is public and stable for real users, release **`1.0.0`**.

---

## 6. How Versioning Works Across Different Platforms

Every platform uses Semantic Versioning, but stores and operating systems often pair it with an internal **Build Number** or **Version Code**.

---

### 📱 Mobile Apps (Android & iOS)

Mobile app stores require two numbers: a **Public Version Name** (what users see) and an **Internal Build Code** (an integer used by the app store to track sequential updates).

#### Android (Google Play)
Configured in `android/app/build.gradle`:
```groovy
defaultConfig {
    versionCode 12          // Must be an integer that increases by +1 on every build
    versionName "1.1.0"     // SemVer string visible to users on Google Play
}
```
- **`versionName`**: What users see in Google Play (e.g., `1.1.0`).
- **`versionCode`**: An integer (e.g., `1`, `2`, `3`, `12`) that must strictly increase with every upload, even if `versionName` didn't change.

#### iOS (Apple App Store)
Configured in Xcode or `Info.plist`:
```xml
<key>CFBundleShortVersionString</key>
<string>1.1.0</string>   <!-- Public SemVer version string -->
<key>CFBundleVersion</key>
<string>42</string>       <!-- Internal build number -->
```
- **Version (`CFBundleShortVersionString`)**: Displayed to users on the App Store (e.g., `1.1.0`).
- **Build (`CFBundleVersion`)**: Internal build iteration (e.g., `42`).

---

### 💻 Desktop / PC Applications (Windows, macOS, Linux)

Desktop applications need version identifiers embedded in binaries and installer packages.

#### Windows (`.exe` / `.msi`)
- Windows PE binaries store a 4-part version: `MAJOR.MINOR.PATCH.BUILD` (e.g., `1.1.0.0`).
- Users see Product Version `1.1.0` in the file properties dialog and Settings > Apps.

#### macOS (`.dmg` / `.app`)
- Defined in the app's `Info.plist` bundle with `CFBundleShortVersionString` (`1.1.0`).

#### Cross-Platform Desktop (Electron / Tauri)
Configured in `package.json` or `tauri.conf.json`:
```json
{
  "name": "desktop-app",
  "version": "1.1.0"
}
```

---

### 🌐 Web Applications & SaaS

SaaS web apps deployed continuously to the cloud (e.g., Vercel, AWS, Netlify) often use a combination of SemVer and Git commits:

- **Public Marketing Version**: Visible in the footer or settings page (`v1.1.0`).
- **Internal Deployment Version**: The Git commit hash or pipeline run ID (`v1.1.0-build.84a1f2`).

---

### 🧩 Browser Extensions (Chrome, Edge, Firefox)

Browser extension stores (Chrome Web Store, Edge Add-ons, Firefox Add-ons) read the version directly from `manifest.json`:

```json
{
  "manifest_version": 3,
  "name": "Awesome Extension",
  "version": "1.1.0"
}
```

**Store Rules:**
1. **Strictly Monotonically Increasing**: You cannot submit the same version number twice, and you cannot downgrade.
2. **Numbers and Dots Only**: Suffixes like `-beta` or `v` are rejected by store validators. Use clean numbers: `"1.1.0"`.
3. **Format**: 1 to 4 integers separated by dots (e.g., `1.1.0` or `1.1.0.1` for urgent store hotfixes).

---

### 📦 Libraries & Package Managers (NPM, Python, Rust)

Package managers rely on strict SemVer to keep automated dependency installations safe.

- **Node.js (NPM)** in `package.json`:
  ```json
  {
    "name": "my-library",
    "version": "1.1.0"
  }
  ```
- **Python (PyPI)** in `pyproject.toml`:
  ```toml
  [project]
  name = "my-library"
  version = "1.1.0"
  ```
- **Rust (Cargo)** in `Cargo.toml`:
  ```toml
  [package]
  name = "my-crate"
  version = "1.1.0"
  ```

---

## 7. Pre-Releases and Beta Testing

Before launching a major update publicly, you can release testing versions using a hyphen suffix:

```text
1.1.0-alpha.1   ➔   Early testing (features incomplete, unstable)
1.1.0-beta.1    ➔   Feature complete, testing for bugs
1.1.0-rc.1      ➔   Release Candidate (ready for final signoff)
1.1.0           ➔   Final official public release!
```

*Note: While package managers (like npm and cargo) support pre-release tags, app stores and extension stores typically use separate internal testing channels (e.g., Google Play Internal Track, Apple TestFlight) instead of custom text tags in the manifest.*

---

## 8. Universal Step-by-Step Release Checklist

When you are ready to ship an update for **any** software project:

```text
[1. Decide Version]  ➔  [2. Update Config]  ➔  [3. Run Tests]  ➔  [4. Build]  ➔  [5. Git Tag]  ➔  [6. Publish]
```

### Step 1: Decide on the New Version Number
Ask yourself:
- Did I break compatibility or rewrite architecture? ➔ Bump **MAJOR** (`2.0.0`).
- Did I add features, UI improvements, or new screens? ➔ Bump **MINOR** (`1.1.0`).
- Did I only fix bugs, errors, or typos? ➔ Bump **PATCH** (`1.0.6`).

### Step 2: Update the Version File
Update the configuration file in your project:
- Web Extensions: `manifest.json`
- Node / Electron / Web: `package.json`
- Android: `build.gradle` (`versionName` & increment `versionCode`)
- iOS: `Info.plist` (Version & increment Build)
- Python: `pyproject.toml`
- Rust: `Cargo.toml`

### Step 3: Run Automated Tests
```bash
npm test       # or pytest, cargo test, etc.
```

### Step 4: Build Release Binaries
Compile and package the release artifact (`.zip`, `.apk`, `.aab`, `.ipa`, `.exe`, or `.dmg`).

### Step 5: Commit and Tag in Git
Create a permanent version tag in Git history:
```bash
git add .
git commit -m "chore: release v1.1.0"
git tag -a v1.1.0 -m "Release version 1.1.0"
git push origin main --tags
```

### Step 6: Publish & Announce
Upload the packaged binaries to GitHub Releases, app store consoles, or package registries.

---

## 9. How to Write Clean Changelogs

Always maintain a `CHANGELOG.md` file following the [Keep a Changelog](https://keepachangelog.com/) format:

```markdown
## [1.1.0] - 2026-10-01

### Added
- Added Dark Mode theme toggle.
- Added drag-and-drop file import.

### Changed
- Redesigned toolbar for faster access on mobile screens.
- Improved rendering performance by 35%.

### Fixed
- Fixed crash when saving large files.
- Resolved memory leak in background worker.

### Security
- Updated dependencies to patch known vulnerabilities.
```

---

## Summary Cheat Sheet

| You Want To... | Do This: | Example |
| :--- | :--- | :---: |
| Fix a bug | Increase **PATCH** | `1.0.5` ➔ `1.0.6` |
| Add a feature or improve UI | Increase **MINOR** and **reset PATCH to 0** | `1.0.5` ➔ `1.1.0` |
| Make breaking changes | Increase **MAJOR** and **reset MINOR & PATCH to 0** | `1.1.0` ➔ `2.0.0` |

*Happy building! Feel free to share, fork, and star this guide on GitHub.*
