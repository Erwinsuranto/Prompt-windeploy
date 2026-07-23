# Prompt-windeploy





















# 
```


```
# 
```


```
# 
```


```
# Phase 8
```
You are continuing the WinDeploy project.

Phase 7 has been completed and verified as PRODUCTION READY.

Do not rewrite completed modules.

Do not modify previous phases except for required integration.

Your task is to implement Phase 8: Windows Configuration.

==================================================
OBJECTIVES
==================================================

Implement the complete Windows first-boot configuration.

Support both:

- Windows Server 2019
- Windows Server 2022
- Windows Server 2025
- Windows 10
- Windows 11

==================================================
AUTOUNATTEND
==================================================

Generate a complete autounattend.xml.

Support:

- Administrator password
- Computer name
- Time zone
- Keyboard layout
- Locale
- Language
- Organization
- Owner
- Product key placeholder
- Skip OOBE
- Auto logon (optional)
- First logon commands
- RunOnce commands

==================================================
ADMINISTRATOR
==================================================

Support:

- Random password
- User supplied password
- Password validation
- Secure password generation
- Password logging (masked)

==================================================
NETWORK
==================================================

Configure:

- DHCP
- Static IPv4
- Gateway
- DNS
- IPv6 enable/disable
- MTU
- Interface detection

==================================================
REMOTE DESKTOP
==================================================

Automatically:

Enable RDP

Enable Remote Desktop Firewall Rules

Enable NLA option

Configure RDP service

Verify RDP enabled

==================================================
VIRTIO
==================================================

Automatically detect and install:

Storage drivers

Network drivers

Balloon drivers

SCSI drivers

Serial drivers

QEMU guest agent (optional)

==================================================
SERVICES
==================================================

Configure:

Remote Desktop

Windows Update

Plug and Play

RPC

Network services

==================================================
VALIDATION
==================================================

Verify:

Administrator configured

Network configured

Drivers installed

RDP enabled

Firewall configured

Autounattend valid

==================================================
DRY RUN
==================================================

Support dry-run.

Display every action.

Never modify deployed Windows.

==================================================
ERROR HANDLING
==================================================

Handle:

Invalid XML

Missing drivers

Missing autounattend

Network failure

Password validation failure

Registry errors

Service configuration errors

Stop safely.

==================================================
LOGGING
==================================================

Log:

Autounattend generation

Password generation

Driver installation

Network configuration

RDP configuration

Validation

Errors

Completion

==================================================
ARCHITECTURE
==================================================

Suggested modules:

scripts/windows_config.sh

scripts/autounattend.sh

scripts/network_config.sh

scripts/virtio.sh

scripts/rdp.sh

scripts/password.sh

==================================================
README
==================================================

Update documentation.

Include:

Autounattend

Drivers

RDP

Networking

Administrator

==================================================
QUALITY
==================================================

ShellCheck clean

bash -n clean

No duplicated code

Strict mode:

set -euo pipefail

Use existing logging framework.

==================================================
FINAL REPORT
==================================================

Provide:

- Files created
- Files modified
- Supported Windows versions
- Supported VirtIO drivers
- Validation performed
- Dry-run demonstration
- Testing instructions
- Example output

Finally print exactly:

WinDeploy Phase 8

STATUS: PRODUCTION READY

```
# Prompt Phase 7
```

You are continuing the WinDeploy project.

Phase 6 has been completed and verified as PRODUCTION READY.

Do not rewrite completed modules.

Do not modify Download Manager, Hardware Detection, Partition Manager, Filesystem Manager, or Image Deployment except for required integration.

Your task is to implement Phase 7: Windows Boot Configuration.

This phase prepares the deployed Windows installation so it can boot correctly on both UEFI and Legacy BIOS systems.

Do NOT configure Windows users.

Do NOT enable RDP.

Do NOT install drivers.

Those belong to later phases.

==================================================
OBJECTIVES
==================================================

Implement a production-grade Windows boot configuration subsystem.

Support:

- UEFI
- Legacy BIOS

Automatically detect boot mode from previous phases.

==================================================
SUPPORTED TOOLS
==================================================

Automatically detect and safely use:

bcdboot

bootsect

efibootmgr (Linux)

bcdedit (Windows environment if available)

blkid

lsblk

mount

umount

==================================================
UEFI SUPPORT
==================================================

Automatically:

Mount EFI System Partition.

Verify FAT32 filesystem.

Create Microsoft Boot directory.

Copy EFI boot files.

Generate BCD store.

Verify:

EFI/Microsoft/Boot exists.

bootmgfw.efi exists.

BCD exists.

==================================================
LEGACY BIOS SUPPORT
==================================================

Configure BIOS boot.

Create System Reserved boot files.

Generate BCD.

Prepare boot sector.

Verify boot files exist.

==================================================
BOOT VALIDATION
==================================================

Verify:

BCD exists.

Boot manager exists.

EFI boot files exist.

Correct partition selected.

Windows directory present.

System32 present.

Boot directory valid.

Architecture compatible.

==================================================
AUTO DETECTION
==================================================

Automatically detect:

Windows partition.

EFI partition.

System Reserved partition.

Boot mode.

Disk layout.

==================================================
ERROR HANDLING
==================================================

Handle:

Missing EFI partition.

Missing boot files.

Invalid BCD.

Wrong partition.

Mount failure.

Copy failure.

Permission denied.

Disk errors.

Stop immediately.

Never continue after boot configuration failure.

==================================================
ROLLBACK
==================================================

If boot configuration fails:

Unmount every mounted partition.

Restore clean state.

Log exact reason.

Do not continue.

==================================================
DRY RUN
==================================================

Support dry-run mode.

Print every command.

Never modify boot files.

==================================================
LOGGING
==================================================

Log:

Boot mode.

Selected partitions.

Mounted partitions.

Boot files copied.

BCD generated.

Validation.

Errors.

Completion.

==================================================
ARCHITECTURE
==================================================

Use modular architecture.

Suggested modules:

scripts/boot_config.sh

scripts/boot_uefi.sh

scripts/boot_bios.sh

scripts/boot_validate.sh

==================================================
README
==================================================

Update documentation.

Include:

UEFI boot

Legacy BIOS boot

BCD generation

Boot validation

Recovery

==================================================
QUALITY
==================================================

ShellCheck clean.

bash -n clean.

No duplicated code.

Strict mode:

set -euo pipefail

Use existing logging framework.

POSIX compatible where possible.

==================================================
FINAL REPORT
==================================================

When finished provide:

- Files created
- Files modified
- Supported boot modes
- Validation performed
- Dry-run demonstration
- Testing instructions
- Example terminal output

Finally print exactly:

WinDeploy Phase 7

STATUS: PRODUCTION READY
```
# Prompt Phase 6
```

You are continuing the WinDeploy project.

Phase 5 has been completed and verified as PRODUCTION READY.

Do not rewrite completed modules.

Do not modify Download Manager, Hardware Detection, Partition Manager, or Filesystem Manager except for required integration.

Your task is to implement Phase 6: Windows Image Deployment.

This phase copies the Windows operating system onto the prepared partition.

Do NOT configure bootloader.

Do NOT configure Windows.

Do NOT modify BCD.

Do NOT enable RDP.

Those belong to later phases.

==================================================
OBJECTIVES
==================================================

Implement a production-grade Windows deployment engine.

Support deployment from:

- install.wim
- install.esd
- split SWM images

Automatically detect the image type.

==================================================
SUPPORTED TOOLS
==================================================

Automatically detect and use:

wimlib-imagex

or

dism (when available)

Prefer wimlib-imagex.

If required tools are missing,

display installation instructions.

==================================================
IMAGE DETECTION
==================================================

Automatically detect:

install.wim

install.esd

install.swm

Verify:

Image exists

Readable

Supported

Checksum validated

==================================================
IMAGE INFORMATION
==================================================

Display:

Edition

Architecture

Language

Version

Build

Compression

Available indexes

Image size

==================================================
INDEX SELECTION
==================================================

If multiple indexes exist:

Display menu:

Windows Server Standard

Windows Server Datacenter

Windows 11 Pro

Windows 11 Enterprise

etc.

Allow automatic or manual selection.

==================================================
DEPLOYMENT
==================================================

Apply selected image onto Windows partition.

Show:

Progress

Percentage

Current operation

Estimated remaining time

Speed

==================================================
VALIDATION
==================================================

Before deployment verify:

Filesystem ready

Partition exists

Enough free space

Selected image valid

Index valid

Target writable

Abort safely if validation fails.

==================================================
POST DEPLOYMENT VALIDATION
==================================================

Verify:

Windows directory exists

Program Files exists

Users exists

Windows/System32 exists

Registry hives exist

Boot directory exists

Expected file count

Image successfully applied

==================================================
ERROR HANDLING
==================================================

Handle:

Corrupted WIM

Corrupted ESD

Missing image

Invalid index

Unsupported image

Disk full

Permission denied

Interrupted deployment

Read errors

Write errors

Stop immediately.

Never continue after failure.

==================================================
ROLLBACK
==================================================

If deployment fails:

Stop deployment.

Log exact reason.

Never continue into boot configuration.

==================================================
LOGGING
==================================================

Log:

Selected image

Selected index

Deployment started

Progress

Validation

Errors

Completion

==================================================
DRY RUN
==================================================

Support simulation mode.

Display every command.

Never apply image.

==================================================
ARCHITECTURE
==================================================

Use modular architecture.

Suggested modules:

scripts/image.sh

scripts/image_detect.sh

scripts/image_apply.sh

scripts/image_validate.sh

scripts/image_index.sh

==================================================
README
==================================================

Update documentation.

Include:

Supported image formats

Index selection

Deployment process

Validation

Recovery

==================================================
QUALITY
==================================================

ShellCheck clean.

bash -n clean.

No duplicated code.

Strict mode:

set -euo pipefail

Use existing logging framework.

==================================================
FINAL REPORT
==================================================

When finished provide:

- Files created
- Files modified
- Supported image formats
- Supported deployment tools
- Validation performed
- Dry-run demonstration
- Testing instructions
- Example deployment output

Finally print exactly:

WinDeploy Phase 6

STATUS: PRODUCTION READY
```
# Filesystem & Formatting
```

You are continuing the WinDeploy project.

Phase 4 has been completed and verified as PRODUCTION READY.

Do not rewrite completed modules.

Do not modify the Download Manager, Hardware Detection, or Partition Manager except for integration if absolutely necessary.

Your task is to implement Phase 5: Filesystem & Formatting.

This phase formats only the partitions created during Phase 4.

Never repartition disks in this phase.

==================================================
OBJECTIVES
==================================================

Implement a production-grade filesystem formatting subsystem for both UEFI and Legacy BIOS installations.

Support automatic validation before and after formatting.

==================================================
SUPPORTED FILESYSTEMS
==================================================

UEFI (GPT)

EFI System Partition
- FAT32

Microsoft Reserved (MSR)
- No filesystem

Windows Partition
- NTFS

--------------------------------------------------

Legacy BIOS (MBR)

System Reserved
- NTFS

Windows Partition
- NTFS

==================================================
SUPPORTED TOOLS
==================================================

Automatically detect and safely use:

mkfs.fat
mkfs.vfat
mkfs.ntfs
mkntfs
ntfslabel
fatlabel
blkid
lsblk
wipefs

Display installation guidance if required tools are missing.

==================================================
SAFETY VALIDATION
==================================================

Before formatting verify:

- Running as root
- Phase 4 completed successfully
- Partition layout validated
- Target partitions exist
- Correct partition count
- Partitions are not mounted
- Target disk matches selected installation disk
- Dry-run mode respected
- No active formatting process

Abort safely if any validation fails.

==================================================
FORMATTING
==================================================

UEFI

Format EFI partition:

FAT32

Label:

SYSTEM

Skip formatting MSR.

Format Windows partition:

NTFS

Label:

Windows

--------------------------------------------------

Legacy BIOS

Format System Reserved:

NTFS

Label:

System

Format Windows partition:

NTFS

Label:

Windows

==================================================
DRY RUN MODE
==================================================

Support simulation mode.

When enabled:

Do NOT execute formatting.

Print every command that would be executed.

Display resulting filesystem layout.

==================================================
POST FORMAT VALIDATION
==================================================

Verify:

Filesystem created successfully

Filesystem type correct

Partition labels correct

UUID readable

Partitions accessible

Expected size

No formatting errors

==================================================
ERROR HANDLING
==================================================

Handle:

Formatting failure

Unsupported filesystem

Read-only device

Permission denied

Disk disconnected

Tool missing

Unexpected command failure

Stop immediately.

Never continue deployment after formatting failure.

==================================================
ROLLBACK
==================================================

If validation fails after formatting:

Stop deployment.

Log exact failure.

Do not continue to Windows deployment.

==================================================
LOGGING
==================================================

Log:

Formatting started

Filesystem selected

Partition formatted

Partition label applied

Validation passed

Validation failed

Errors

Completion

==================================================
ARCHITECTURE
==================================================

Use the existing modular architecture.

Create modules if needed.

Suggested files:

scripts/filesystem.sh

scripts/filesystem_fat32.sh

scripts/filesystem_ntfs.sh

scripts/filesystem_validate.sh

Integrate cleanly with Phase 4.

==================================================
DO NOT
==================================================

Do NOT repartition disks.

Do NOT deploy Windows.

Do NOT install bootloader.

Do NOT modify image deployment.

Do NOT change completed modules except for integration.

==================================================
README
==================================================

Update documentation.

Include:

Filesystem support

Formatting flow

Partition labels

Dry Run mode

Validation

Recovery behavior

==================================================
QUALITY
==================================================

ShellCheck clean.

bash -n clean.

No duplicated code.

Use existing logging framework.

Strict mode:

set -euo pipefail

POSIX compatible where possible.

==================================================
FINAL REPORT
==================================================

When finished provide:

- Files created
- Files modified
- Supported filesystems
- Validation performed
- Safety checks
- Dry-run demonstration
- Testing instructions
- Example terminal output

Finally print exactly:

WinDeploy Phase 5

STATUS: PRODUCTION READY
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
