# Prompt-windeploy










# Prompt 3: Disk Detection & Safety Validation
```
Audit the entire Download Manager implementation before continuing to the next phase.

Verify:

- ShellCheck passes on every modified shell script.
- No syntax errors.
- No broken imports or source statements.
- All referenced files exist.
- images.json schema is valid.
- Mirror failover works correctly.
- Maintenance mode works correctly.
- Manual download mode works correctly.
- Resume download works.
- SHA256 verification works.
- Retry logic works.
- Logging works.
- Exit codes are correct.
- README matches the implementation.

If you find any issue, fix it immediately.

Do not implement any new features.

Only audit, repair, test, and report.

When everything passes, print:

"Prompt 2 verified and production-ready."

```


# 
```
Continue implementing Prompt 2 from the current repository state.

Do not restart or regenerate completed work.

Complete every unfinished task from the existing implementation plan until all items are marked done.

Repair any incomplete files, verify the download module works end-to-end, update README.md, validate config/images.json, and ensure all download features are fully implemented.

Do not modify deployment modules or unrelated files.

When finished, provide:
- All completed tasks
- Modified files
- Remaining TODOs (if any)
- Testing instructions
- Confirmation that Prompt 2 is fully complete.

```
# 
```
You are continuing the WinDeploy project. Continue from the existing repository without rewriting completed modules. Preserve the current modular architecture, coding style, logging framework, documentation style, and file structure.

Your task is to fully implement the Download Manager subsystem. Do NOT implement Windows deployment, disk partitioning, formatting, bootloader installation, or image writing. Focus only on downloading and validating Windows images.

Requirements:

1. Download Manager
- Automatic download.
- Resume interrupted downloads.
- Retry failed downloads automatically.
- Configurable timeout.
- Download progress percentage.
- Download speed.
- Estimated remaining time.
- Support Ctrl+C cancellation.
- Remove incomplete downloads after user cancellation.
- Continue download if partially downloaded file exists.

2. Mirror System
Support unlimited mirrors defined inside config/images.json.

Example:

{
  "windows-server-2022": {
    "name": "Windows Server 2022",
    "status": "online",
    "version": "2022",
    "size": "5.2GB",
    "sha256": "xxxxxxxx",
    "mirrors": [
      "https://mirror1...",
      "https://mirror2...",
      "https://mirror3..."
    ],
    "manual_download": "https://..."
  }
}

Mirror logic:

- Try mirror 1.
- If failed automatically try mirror 2.
- Continue until successful.
- If every mirror fails, automatically switch to Manual Download mode.

3. Manual Download Mode

Display:

- Official download page.
- Mirror list.
- Manual download instructions.

Do not automatically download in manual mode.

4. Maintenance Mode

If image status equals "maintenance":

Display:

--------------------------------------------------
Image is temporarily unavailable.

The download link is currently under maintenance.

Please try again later.
--------------------------------------------------

Exit safely.

5. Validation

After download perform:

- SHA256 verification.
- File size verification.
- File existence verification.

If validation fails:

- Delete corrupted file.
- Continue with next mirror.
- Never continue deployment using corrupted images.

6. Internet Detection

Before downloading:

- Verify internet connection.
- Detect DNS failure.
- Detect unreachable hosts.

Provide friendly error messages.

7. Error Handling

Handle:

- HTTP 403
- HTTP 404
- HTTP 500
- Connection timeout
- DNS failure
- Permission denied
- Disk full
- Corrupted download
- Interrupted download
- Invalid checksum

The installer must never crash.

Return meaningful exit codes.

8. Logging

Log:

- Selected image
- Selected mirror
- Download started
- Download completed
- Retry count
- Timeout
- Checksum verification
- Mirror switching
- Manual mode
- Maintenance detection
- Validation success
- Validation failure

Use the existing logging framework.

9. User Interface

Provide a clean terminal UI similar to:

================================================
WinDeploy Download Manager
================================================

Image:
Windows Server 2022

Mirror:
Mirror 2 / 3

Status:
Downloading...

Progress:
██████████░░░░░░ 58%

Speed:
48 MB/s

Remaining:
1m 42s

================================================

If all mirrors fail:

--------------------------------------------------
Automatic download is currently unavailable.

Possible reasons:

• Server maintenance
• Mirror offline
• Network issue

Please use Manual Download mode.
--------------------------------------------------

10. Architecture

Only modify files related to downloading.

Allowed:

- scripts/download.sh
- config/images.json
- README.md

If needed create helper functions or helper modules dedicated only to downloading.

Do NOT modify:

- deploy.sh
- disk.sh
- boot.sh
- finish.sh
- install.sh logic unrelated to download
- deployment pipeline

11. Documentation

Update README.md with:

- Automatic Download
- Resume Download
- Mirror System
- Manual Download
- Maintenance Mode
- SHA256 Verification
- Error Recovery

12. Code Quality

- ShellCheck clean.
- Modular functions.
- No duplicated code.
- Safe Bash practices.
- POSIX compatible where possible.
- Preserve existing architecture.
- Do not remove existing features.

At the end provide:

- List of modified files.
- New helper functions.
- Testing instructions.
- Sample images.json.
- Summary of implemented features.

Do not implement Windows deployment in this phase. Only complete a production-ready Download Manager.

```
