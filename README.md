

# Jira Ticket Enforcement in Git Commits

Ensure every Git commit is linked to a Jira ticket (e.g., `PROJ-123`) with this cross-platform Git hook. Works on **Windows (PowerShell)**, **macOS**, and **Unix/Linux**.

## Table of Contents
1. [Features](#features)
2. [Prerequisites](#prerequisites)
3. [Installation](#installation)
4. [Usage](#usage)
5. [Troubleshooting](#troubleshooting)
6. [FAQs](#faqs)

---

## Features
- **Cross-Platform**: Auto-detects OS (Windows/PowerShell or Unix/bash).
- **Merge Commit Support**: Skips validation for merge commits.
- **Clear Errors**: Shows red error messages for invalid commits (Windows) or standard errors (Unix).
- **Security**: PowerShell execution policy bypassed only for this script.

---

## Prerequisites
- **Git** installed ([Download Git](https://git-scm.com/downloads))
- **PowerShell 5.1+** (Windows users - preinstalled on Windows 10/11)

---

## Installation

### 1. Clone the Repository
```bash
git clone https://github.com/your-org/your-repo.git
cd your-repo
```

### 2. Configure Git Hooks
Run this **once** to activate the hook:
```bash
git config core.hooksPath .githooks
```

### 3. Verify Executable Permissions (Unix/macOS)
```bash
chmod +x .githooks/commit-msg
```

---

## Usage

### Valid Commit Examples
```bash
git commit -m "PROJ-456: Fix login bug"
git commit -m "Add feature [PROJ-789]"
```

### Invalid Commit Examples
```bash
git commit -m "Update documentation"  # Missing Jira ticket
git commit -m "Fix typo"              # Missing Jira ticket
```

#### Expected Error (Windows/PowerShell):
```
ERROR: Commit message must contain a Jira ticket number (e.g., ABC-123).
Example: 'ABC-123: Fix the issue'
```

#### Expected Error (Unix/macOS):
```
error: Jira ticket number missing. Commit rejected.
```

---

## Bypassing the Hook (Temporary)
**Not recommended**, but for emergencies:
```bash
git commit --no-verify -m "Skipping hook for urgent fix"
```

---

## Troubleshooting

### Issue: Hook Not Blocking Commits
**Solution**:
1. Verify hooks path:
   ```bash
   git config --get core.hooksPath  # Should return `.githooks`
   ```
2. Ensure `commit-msg` file exists in `.githooks/`.

### Issue: Permission Denied (Unix/macOS)
```bash
chmod +x .githooks/commit-msg
```

### Issue: Line Ending Errors (Windows)
Run in PowerShell:
```powershell
git config --global core.autocrlf true
```

---

## FAQs

### Q: What Jira ticket formats are allowed?
**A**: Any format containing `XXX-123` (case-sensitive):
- `PROJ-123: Fix bug`
- `[PROJ-456] Update UI`
- `PROJ-789 - Add tests`

### Q: How to handle commits without a Jira ticket?
**A**: Follow your team process (e.g., create a ticket first). Bypassing is blocked by design.

### Q: Can I customize the Jira project key (e.g., `PROJ`)?
**A**: Edit the regex in `.githooks/commit-msg`:
```bash
# For Unix/bash
JIRA_PATTERN='PROJ-[0-9]+'  # Change PROJ to your project key

# For PowerShell
$JIRA_PATTERN = 'PROJ-[0-9]+'
```

---

## Repository Structure
```
repo/
├── .githooks/
│   └── commit-msg     # Cross-platform hook
├── src/               # Your code
└── README.md          # This documentation
```

---

## Contributors
- Update the hook logic in `.githooks/commit-msg`.
- Test changes on **both Windows and Unix**.

---

## Security Note
The PowerShell script bypasses execution policy **only for this hook**. No system-wide changes are made.

---

This documentation ensures consistent adoption across teams and platforms. For issues, refer to [Troubleshooting](#troubleshooting) or contact your repository maintainer/s.kumar@kimbal.io.



hello
