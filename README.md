# Task Manager Background Process Fix

## Overview

This registry fix resolves an issue where the Task Manager process might continue to run in the background after the app is closed, causing process duplication and system resource waste.

**Status**: ✅ Verified and tested

## 📥 Quick Download

**[⬇️ Download Registry Fix](https://raw.githubusercontent.com/1LUC1D4710N/task-manager-background-process-fix/main/Task%20Manager%20Background%20Process%20Fix.reg)**

Right-click the downloaded `.reg` file → **Merge** → **Yes** → **Restart** ✅

## Issue Description

In Windows 11 Insider Preview Build 28000 and certain other builds, Task Manager exhibits a bug where:
- The process may not properly terminate when clicking the [X] button
- Duplicate Task Manager processes accumulate in the background
- System resources are unnecessarily consumed by orphaned processes

## Solution

This fix applies three registry entries to the Windows Feature Management overrides:

### What's Applied

The registry file enables the following features via Feature Management overrides:

1. **KB5067036 CU Main Feature Bundle** (ViVetool ID: 57048231)
   - CFR RKey: 1318466191
   - Enables core features for the cumulative update

2. **Task Manager Process Grouping Fix** (ViVetool ID: 49407484)
   - CFR RKey: 4188347533
   - Fixes: Some apps might unexpectedly not be grouped with their processes
   - *Requires KB5067036 to be enabled*

3. **Task Manager Termination Fix** (ViVetool ID: 45036792)
   - CFR RKey: 4027031693
   - Fixes: Task Manager cannot terminate the process using the [X] button

All three entries set:
- `EnabledState` = `0x00000002` (Enabled)
- `EnabledStateOptions` = `0x00000000` (Default options)

## Installation

### Prerequisites

- Windows 11
- Administrator privileges
- Backup of your registry (recommended)

### Steps

1. **Backup Registry** (Optional but recommended)
   - Press `Win + R`
   - Type: `regedit`
   - Press Enter
   - File → Export → Save as backup

2. **Apply the Fix**
   - Download the `.reg` file
   - Right-click on the file
   - Select "Merge"
   - Click "Yes" when prompted for confirmation
   - Restart your computer

### PowerShell Alternative

```powershell
# Run as Administrator
$regPath = "HKLM:\SYSTEM\ControlSet001\Control\FeatureManagement\Overrides\14"
New-Item -Path $regPath -Force | Out-Null
New-ItemProperty -Path "$regPath\1318466191" -Name "EnabledState" -Value 2 -PropertyType DWord -Force | Out-Null
New-ItemProperty -Path "$regPath\1318466191" -Name "EnabledStateOptions" -Value 0 -PropertyType DWord -Force | Out-Null
New-ItemProperty -Path "$regPath\4188347533" -Name "EnabledState" -Value 2 -PropertyType DWord -Force | Out-Null
New-ItemProperty -Path "$regPath\4188347533" -Name "EnabledStateOptions" -Value 0 -PropertyType DWord -Force | Out-Null
New-ItemProperty -Path "$regPath\4027031693" -Name "EnabledState" -Value 2 -PropertyType DWord -Force | Out-Null
New-ItemProperty -Path "$regPath\4027031693" -Name "EnabledStateOptions" -Value 0 -PropertyType DWord -Force | Out-Null
```

Then restart your computer.

## Verification

You can monitor Task Manager processes using PowerShell:

```powershell
# Monitor Task Manager processes
while ($true) {
    $processes = Get-Process -Name taskmgr -ErrorAction SilentlyContinue
    Write-Host "[$(Get-Date -Format 'HH:mm:ss')] Task Manager processes: $($processes.Count)"
    Start-Sleep -Seconds 1
}
```

For automated killing after duration, see the companion script: [kill-taskmgr-script](https://github.com/1LUC1D4710N/kill-taskmgr-script)

## Uninstallation / Reverting Changes

If you need to undo this fix:

1. **Using Registry Editor**
   - Press `Win + R`
   - Type: `regedit`
   - Press Enter
   - Navigate to: `HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\FeatureManagement\Overrides`
   - Right-click on the `14` folder
   - Select "Delete"
   - Restart your computer

2. **Using Command Prompt (As Administrator)**
   ```cmd
   REG DELETE "HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\FeatureManagement\Overrides\14" /f
   ```
   Then restart your computer.

3. **Using PowerShell (As Administrator)**
   ```powershell
   Remove-Item -Path "HKLM:\SYSTEM\ControlSet001\Control\FeatureManagement\Overrides\14" -Force -ErrorAction SilentlyContinue
   ```
   Then restart your computer.

## ⚠️ Important Advisory

**This is a temporary workaround fix.**

Once Microsoft releases an official hotfix for this issue, the `Overrides\14` registry folder can be safely deleted. Monitor Microsoft's official support channels and Windows 11 release notes for announcements regarding:

- KB5067036 or subsequent cumulative updates
- Official fixes for Task Manager process management

When the official hotfix is released, follow the "Uninstallation" steps above to revert these registry changes.

## Sources

- **Online Article**: [Make Tech Easier - Fix Windows Task Manager Duplication Bug](https://www.maketecheasier.com/fix-windows-task-manager-duplication-bug/)
- **Original Registry File**: [SimonMacer/CreateMediaRefresh25H2/Other](https://github.com/SimonMacer/CreateMediaRefresh25H2/blob/main/Other/Resolve%20Task%20Manager%20process%20might%20continue%20to%20run%20in%20background%20after%20app%20is%20closed.reg)
- **Verification Script**: [kill-taskmgr-script](https://github.com/1LUC1D4710N/kill-taskmgr-script)

## Testing Confirmation

✅ **Verified**: Task Manager no longer duplicates in background processes after application closure.

Tested with:
- Windows 11 Insider Preview Build 28000 and related builds
- PowerShell process monitoring
- Multiple open/close cycles

## License

Based on community fixes and shared resources. Use at your own discretion.

---

**Last Updated**: November 2025
