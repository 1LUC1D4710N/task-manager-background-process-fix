# Quick Start Guide

## TL;DR - Apply the Fix in 3 Steps

### Step 1: Download

Download the `.reg` file from this folder

### Step 2: Apply

Right-click the `.reg` file → **Merge** → **Yes** when prompted

### Step 3: Restart

Restart your computer

---

## What This Fixes

✅ Task Manager no longer duplicates in background processes  
✅ [X] button properly terminates Task Manager  
✅ Reduced system resource consumption  

---

## Did It Work?

Open PowerShell and run:

```powershell
Get-Process taskmgr | Measure-Object | Select-Object -ExpandProperty Count
```

Should show only 1 or 0 processes (instead of multiple duplicates).

---

## Need to Undo?

### Option 1: Registry Editor

1. `Win + R` → type `regedit` → Enter
2. Navigate to: `HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\FeatureManagement\Overrides`
3. Right-click `14` folder → Delete
4. Restart

### Option 2: Command Prompt (Admin)

```cmd
REG DELETE "HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\FeatureManagement\Overrides\14" /f
```

Then restart.

### Option 3: PowerShell (Admin)

```powershell
Remove-Item -Path "HKLM:\SYSTEM\ControlSet001\Control\FeatureManagement\Overrides\14" -Force
```

Then restart.

---

## Important Notes

⚠️ **Temporary Fix**: Once Microsoft releases an official hotfix, delete the `Overrides\14` registry folder.

📋 **Requires Admin**: You need administrator privileges to apply this fix.

💾 **Backup Registry**: Consider backing up your registry before applying (optional but recommended).

🔄 **Restart Required**: Changes take effect only after restart.

---

## Need More Details?

- **User Guide**: See `README.md`
- **Technical Info**: See `TECHNICAL_DETAILS.md`
- **Testing Script**: Check out [kill-taskmgr-script](https://github.com/1LUC1D4710N/kill-taskmgr-script)

---

## Sources

- Online Article: [Make Tech Easier](https://www.maketecheasier.com/fix-windows-task-manager-duplication-bug/)
- Original Registry: [GitHub - CreateMediaRefresh25H2/Other](https://github.com/SimonMacer/CreateMediaRefresh25H2/blob/main/Other/Resolve%20Task%20Manager%20process%20might%20continue%20to%20run%20in%20background%20after%20app%20is%20closed.reg)
- Testing Script: [GitHub - kill-taskmgr-script](https://github.com/1LUC1D4710N/kill-taskmgr-script)
