# C/SIDE Source Control

> Whether we like it or not, the classic C/SIDE environment will be with NAV developers for quite some time.  
> C/SIDE Source Control helps you maintain C/AL code efficiently with integrated Git support.

---

## Table of Contents
1. Overview
2. Features
3. Prerequisites
4. Installation
5. Quick Start
6. Exporting / Importing Objects
7. How It Works (Object Splitting & Repository Layout)
8. Server Setup (finsql.exe extraction)
9. Typical Workflows
10. Troubleshooting & Tips
11. Building From Source
12. Roadmap / Ideas
13. Contributing
14. License

---

## 1. Overview

C/SIDE Source Control bridges classic Microsoft Dynamics NAV C/AL development and modern source control practices.  
It automates:
- Extraction of C/AL objects from NAV (when supported by your version)
- Splitting multi‑object text exports into individual, well‑organized files
- Structuring a clean Git repository per project
- Making ongoing maintenance of legacy NAV solutions more predictable

---

## 2. Features

- Git repository initialization and management
- Automatic splitting of exported `.txt` files containing multiple objects
- Object type–based folder organization
- Optional automated object extraction via `finsql.exe` (newer NAV versions)
- Manual import for older NAV versions (drag & drop text export)
- Server configuration storage for repeatable extraction
- Lightweight UI for repository setup and operations

---

## 3. Prerequisites

| Component | Purpose | Link |
|-----------|---------|------|
| Git for Windows | Source control backend | https://git-scm.com/download/win |
| Microsoft Dynamics NAV Development Environment (C/SIDE) | C/AL authoring | Provided with NAV |
| .NET & Visual Studio (for source build) | Building from source | Visual Studio 2019+ |
| finsql.exe (newer NAV versions) | Automated object extraction | Part of NAV install |

You must have Git installed prior to repository initialization.

---

## 4. Installation

### Option A: Install Published Version
Navigate here:  
`https://byxinternaldiag.blob.core.windows.net/csidesourcecontrol/publish.htm`

Follow the ClickOnce / publish installation instructions.

### Option B: Build From Source
1. Clone the repository:
   ```bash
   git clone https://github.com/byxdigital/Byx.DevTools.CSIDE-Source-Control.git
   ```
2. Open the solution in Visual Studio.
3. Restore NuGet packages if prompted.
4. Build the solution (Release preferred).
5. Run the application.

---

## 5. Quick Start

1. Launch the application.
2. Go to the tab: `Repository Setup` → `Set Destination Folder`.
   - This folder will contain the split C/AL object files and the initialized Git repository.
3. Initialize (if not already) the Git repository (the app will guide you).
4. Import objects:
   - Older NAV: Export a single `.txt` containing all needed objects from C/SIDE; drag & drop into the app.
   - Newer NAV: Use automated extraction (see Section 8).

Commit and push your initial baseline once everything looks correct.

---

## 6. Exporting / Importing Objects

### Older Versions of NAV
- Export objects to a single text file via the classic development environment.
- Drag the `.txt` file into C/SIDE Source Control.
- The application splits and categorizes objects automatically.
- Reminder: You can include ALL objects; splitting is handled for you.

### Newer Versions (Automated Extraction)
- Use `finsql.exe` with proper server/database parameters.
- Trigger the import via the app's Import function after configuring server settings.

---

## 7. How It Works (Object Splitting & Repository Layout)

When you provide a multi‑object `.txt` export:
- The tool parses object boundaries.
- Each object is written to an individual file.
- Files are placed into folders based (typically) on object type (e.g., `Tables/`, `Pages/`, `Codeunits/`, `Reports/`, etc.).
- This structure dramatically improves diff readability and Git history tracking.

Git best practices (recommended):
- Commit logically grouped changes (one feature / fix per commit).
- Use branches for new development or experimentation.

---

## 8. Server Setup (finsql.exe Extraction)

For NAV versions supporting object extraction via `finsql.exe`:

1. Navigate to: `Repository Setup` → `Server Setup`.
2. Locate and select your `finsql.exe` path.
3. Fill in server/database parameters:
   - You can copy them from: `File → Database → Information` inside the NAV Development Environment.
4. Save settings.
5. Use the Import/Extract function to pull objects directly.

If extraction fails:
- Confirm correct server/database names.
- Ensure permissions for object export.
- Run the tool with sufficient privileges.

---

## 9. Typical Workflows

### Baseline Capture
- Export all objects.
- Import/split.
- Commit as `Initial baseline`.

### Feature Development
- Make changes in NAV.
- Re‑export only changed objects (or full set if easier).
- Re‑import (changed files will update).
- Review diffs; commit with a descriptive message.

### Periodic Synchronization
- Schedule regular exports (daily/weekly) to maintain an auditable history.

### Branching Strategy
- `main` / `master`: Stable production snapshot.
- `feature/*`: Isolated development streams.
- `hotfix/*`: Urgent production fixes.

---

## 10. Troubleshooting & Tips

| Issue | Possible Cause | Action |
|-------|----------------|-------|
| Objects not splitting | Unexpected formatting in export | Re‑export ensuring standard NAV export format |
| Git operations fail | Git not installed / PATH issue | Reinstall Git; confirm `git --version` works |
| finsql extraction errors | Incorrect server parameters | Recheck Database Information dialog |
| Duplicate objects | Multiple exports without cleanup | Remove obsolete files or re‑baseline |

Tips:
- Always review diffs before committing large batches.
- Tag releases (e.g., `vYYYY.MM.DD`) for milestone snapshots.

---

## 11. Building From Source

Project layout (high level):
- UI project (WPF/WinForms depending on actual implementation)
- Logic / Services for parsing and splitting
- Git integration helpers

Build steps:
1. Ensure SDKs installed.
2. Clean → Build.
3. Run tests (if present).
4. Package (optional).

---

## 12. Roadmap / Ideas (Proposed)

- Enhanced diff viewer inside the app
- Object dependency graphing
- Automated tagging on successful extraction
- CI integration hooks
- PowerShell / CLI extraction mode
- AL migration helper (legacy to modern extensions)

(Feel free to open issues with suggestions.)

---

## 13. Contributing

Contributions welcome:
1. Fork the repository.
2. Create a feature branch: `git checkout -b feature/object-diff-improvements`.
3. Commit changes: `git commit -m "Add enhanced diff grouping"`.
4. Push branch: `git push origin feature/object-diff-improvements`.
5. Open a Pull Request with clear description.

Please ensure:
- Clear commit messages.
- No sensitive data in sample exports.
- Discussion for larger architectural shifts before implementation.

---

## 14. License

(If a license file exists, reference it here. Otherwise consider adding one such as MIT or Apache 2.0.)

Example:
This project is licensed under the MIT License – see [LICENSE](LICENSE) for details.

---

## Credits / Acknowledgements

- NAV / C/SIDE community inspiration
- Git tooling ecosystem
- Original authors/maintainers (Byx Digital)

---

## Quick Reference (TL;DR)

| Task | Action |
|------|--------|
| Install | Use published link or build from source |
| Setup Repo | Repository Setup → Set Destination Folder |
| Import (Old NAV) | Export `.txt` with all objects → Drag into app |
| Import (New NAV) | Configure `finsql.exe` → Use Import |
| Split Objects | Automatic |
| Commit | Use Git (external client or command line) |
| Update Objects | Re‑export → Re‑import → Diff → Commit |

---

> Legacy C/AL maintenance does not have to be painful—structured source control is the foundation for reliability and transition planning.
