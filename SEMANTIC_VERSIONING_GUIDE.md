# The Ultimate Guide to Software Versioning (SemVer) for Browser Extensions

This guide provides a comprehensive reference on how software versioning works, how to choose the right version for future releases, and the exact step-by-step workflow for updating the **LongShot** extension (and any browser extension).

---

## 1. The Core Structure: Semantic Versioning (`SemVer`)

Most modern software, npm packages, and browser extensions follow **Semantic Versioning** (`MAJOR.MINOR.PATCH`):

```text
       1    .    0    .    5
       │         │         │
    [MAJOR]   [MINOR]   [PATCH]
```

### What Each Number Represents:

| Segment | Name | When to Increment | What it Signals | Example |
| :---: | :---: | :--- | :--- | :--- |
| **First** | **MAJOR** | Breaking changes, massive redesigns, or rewriting core architecture. | Major milestone; users expect substantial visible shifts or paradigm changes. | `1.0.0` ➔ `2.0.0` |
| **Middle** | **MINOR** | New features, major UI/UX refinements, or feature enhancements added in a backward-compatible way. | Significant enhancement; new tools or redesigned placements. Resets PATCH to 0! | `1.0.5` ➔ `1.1.0` |
| **Last** | **PATCH** | Bug fixes, performance tweaks, security hotfixes, small styling corrections. | Stability release; fixes issues without altering core workflows or feature sets. | `1.0.5` ➔ `1.0.6` |

---

## 2. The Golden Rule of Version Bumping: The Reset Rule

> **Whenever a higher-level number increases, every number to its right MUST reset back to `0`.**

### Why `1.0.5` ➔ `1.1.0` (and NEVER `1.1.6`):

1. **If you only fix bugs:**
   - Keep `MAJOR` (`1`) and `MINOR` (`0`) unchanged.
   - Increment `PATCH`: `5` ➔ `6`.
   - Result: **`1.0.6`**.

2. **If you introduce UI refinements or new features:**
   - Increment `MINOR`: `0` ➔ `1`.
   - **The reset rule applies**: the `PATCH` number resets from `5` to **`0`**.
   - Result: **`1.1.0`**.

3. **Why `1.1.6` is incorrect:**
   - Incrementing both `MINOR` (`0` ➔ `1`) and `PATCH` (`5` ➔ `6`) at once skips versions.
   - To store reviewers and users, `1.1.6` falsely implies that versions `1.1.0`, `1.1.1`, `1.1.2`, `1.1.3`, `1.1.4`, and `1.1.5` were already released and published previously.

---

## 3. Real-World Decision Matrix

Use this quick cheat-sheet whenever you are deciding on the next version number:

| Current Version | What Was Changed | Next Version | Rationale |
| :---: | :--- | :---: | :--- |
| `1.0.5` | Fixed a slider lag or small text typo | **`1.0.6`** | Pure bug fix / patch |
| `1.0.5` | Redesigned toolbar placements, added animations, improved shape selection | **`1.1.0`** | UI/UX refinement & workflow enhancements |
| `1.1.0` | Fixed a small edge-case bug found in 1.1.0 | **`1.1.1`** | First bug fix for the 1.1.x line |
| `1.1.0` | Added Cloud Upload / Google Drive integration | **`1.2.0`** | Major new capability added |
| `1.2.4` | Rebuilt extension from scratch or moved to Manifest V4 / completely new UX | **`2.0.0`** | Major architectural overhaul |

---

## 4. Browser Store Requirements (Chrome, Edge, Firefox)

When submitting an update to the Chrome Web Store, Microsoft Edge Add-ons, or Mozilla Firefox Add-ons:

1. **Strictly Monotonically Increasing**:
   The new version string must always be numerically greater than the currently published version. You can never submit `1.0.5` again, and you can never downgrade to `1.0.4`.
2. **Format Constraints**:
   Chrome, Edge, and Firefox support 1 to 4 integers separated by dots:
   - Example: `1.1.0` (Standard)
   - Example: `1.1.0.1` (Emergency hotfix format if needed)
   - Each number must be an integer between `0` and `65535`.
3. **No Letters or Suffixes**:
   Do not include strings like `v1.1.0-beta` in `manifest.json`. Only use clean digits and dots: `"1.1.0"`.

---

## 5. Step-by-Step Release Checklist for LongShot

Whenever you prepare a new release:

### Step 1: Update the Version in `manifest.json`
Open `manifest.json` in the root directory and update the `version` field:
```json
{
  "manifest_version": 3,
  "name": "LongShot - Full Page & Scrolling Screenshot",
  "version": "1.1.0"
}
```

### Step 2: Run the Multi-Browser Build Script
Open your terminal in the project root directory and run:
```bash
node build.js
```
This automatically:
- Validates JavaScript syntax across all source files.
- Audits Manifest V3 offline and remotely hosted code compliance.
- Updates versions in `dist/chrome`, `dist/edge`, and `dist/firefox`.
- Packages ready-to-upload ZIP archives into the `dist/` folder:
  - `dist/longshot-chrome-v1.1.0.zip`
  - `dist/longshot-edge-v1.1.0.zip`
  - `dist/longshot-firefox-v1.1.0.zip`

### Step 3: Run the Test Suite
Ensure zero regressions by running:
```bash
node tests/test_suite.js
```
All tests must report **PASS**.

### Step 4: Upload to Browser Stores
- **Chrome Web Store Developer Dashboard**:
  Upload `dist/longshot-chrome-v1.1.0.zip`
- **Microsoft Partner Center (Edge)**:
  Upload `dist/longshot-edge-v1.1.0.zip`
- **Mozilla Add-on Developer Hub (Firefox)**:
  Upload `dist/longshot-firefox-v1.1.0.zip`
