# Prompt-windeploy












# 
```


```

# Prompt 3 (sekali copy). Fokusnya adalah Hardware Detection & Safety Validation.
```
You are continuing the WinDeploy project.

Phase 2 has been completed and verified as PRODUCTION READY.

Do not rewrite existing modules.

Do not modify completed download functionality.

Your task is to implement Phase 3: Hardware Detection & Safety Validation.

This phase MUST NEVER modify disks.

This phase only detects, validates, reports and asks for confirmation.

==================================================
OBJECTIVES
==================================================

Create a production-grade hardware detection system before Windows deployment.

Implement only safe read-only operations.

==================================================
SYSTEM DETECTION
==================================================

Detect:

- CPU architecture
- CPU model
- CPU cores
- Total RAM
- Available RAM
- Virtualization platform
- Hypervisor
- BIOS or UEFI
- Boot mode
- Secure Boot status if available
- Disk controller type
- Network interfaces
- Internet connectivity
- Public IP
- Hostname
- Linux distribution
- Kernel version

==================================================
VIRTUALIZATION DETECTION
==================================================

Automatically detect:

KVM
QEMU
VMware
VirtualBox
Hyper-V
Xen
OpenVZ
LXC
Docker
Proxmox
Unknown

If unsupported virtualization is detected display a warning.

==================================================
DISK DETECTION
==================================================

Detect every disk.

Display:

Device
Model
Vendor
Interface
Transport
Capacity
Sector Size
Partition Table
Filesystem
Mounted
Mount Points
SSD/HDD
NVMe/SATA/VirtIO

Automatically determine the most likely installation disk.

Never modify anything.

==================================================
SAFETY VALIDATION
==================================================

Check:

Running as root

Enough RAM

Enough disk space

Supported CPU architecture

Supported virtualization

Internet available

Download directory writable

Temporary directory writable

Configuration exists

Images.json valid

Download module available

If any validation fails

Display clear reason

Stop safely

==================================================
INSTALLATION RISK ANALYSIS
==================================================

Display warnings if:

Multiple disks detected

Windows already exists

Existing Linux installation detected

Unknown partition table

Encrypted disks

RAID

LVM

Mounted installation target

Display confirmation before continuing.

==================================================
INTERACTIVE SUMMARY
==================================================

Display a professional summary similar to:

========================================

WinDeploy Hardware Validation

========================================

CPU:

...

RAM:

...

Virtualization:

KVM

Boot:

UEFI

Installation Disk:

/dev/vda

Capacity:

100 GB

Internet:

OK

Images:

OK

Download Module:

OK

Overall Status:

READY

========================================

==================================================
EXIT STATUS
==================================================

READY

WARNING

FAILED

Colorize output using existing logger.

==================================================
LOGGING
==================================================

Log:

Hardware detection

Disk detection

Virtualization detection

Validation results

Warnings

Errors

Summary

==================================================
ARCHITECTURE
==================================================

Use the existing modular architecture.

Create helper modules if needed.

Suggested files:

scripts/hardware.sh

scripts/safety.sh

Do not modify deployment modules.

==================================================
DO NOT
==================================================

Do NOT partition disks.

Do NOT format disks.

Do NOT deploy Windows.

Do NOT write bootloader.

Do NOT modify any partition.

Everything in this phase must be read-only.

==================================================
DOCUMENTATION
==================================================

Update README.md.

Document:

Hardware Detection

Disk Detection

Safety Validation

Virtualization Support

System Requirements

==================================================
QUALITY
==================================================

ShellCheck clean

bash -n clean

No duplicated code

Use existing logging framework

POSIX compatible where possible

==================================================
FINAL REPORT
==================================================

When finished provide:

- Files created
- Files modified
- Detection features implemented
- Validation checklist
- Testing instructions
- Example terminal output

Finally print exactly:

WinDeploy Phase 3

STATUS: PRODUCTION READY

```
# 
```
Continue from the current repository state.

Do not implement any new features.

Your only task is to repair install.sh until it is production-ready.

Requirements:

- Fix every ShellCheck warning.
- Fix the malformed IFS assignment.
- Remove all placeholder comments.
- Verify every sourced module exists.
- Verify every function call exists.
- Verify download.sh integration.
- Verify exit codes.
- Verify syntax using bash -n.
- Verify install.sh is the only remaining blocker.

After repairing install.sh:

Run a complete project audit again.

Check:

- bash -n on every shell script
- ShellCheck on every script
- source/import validation
- images.json validation
- README consistency
- download module integration
- logging integration
- exit codes
- install.sh entrypoint

If any issue is found, repair it immediately.

Only stop when the entire repository passes all validation.

Finally print exactly:

WinDeploy Phase 2
STATUS: PRODUCTION READY

Then provide:

- Modified files
- Validation results
- Remaining TODOs (must be NONE)

`
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
