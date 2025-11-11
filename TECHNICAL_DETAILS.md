# Technical Details

## Registry Path

```powershell
HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\FeatureManagement\Overrides\14
```

## Feature Management Entries

### Entry 1: KB5067036 CU Main Feature Bundle

- **ViVetool ID**: 57048231
- **CFR RKey**: 1318466191
- **Purpose**: Enable core features from cumulative update
- **Status**: EnabledState = 2 (Enabled)

### Entry 2: Task Manager Process Grouping Fix

- **ViVetool ID**: 49407484
- **CFR RKey**: 4188347533
- **Purpose**: Fixed - Some apps might unexpectedly not be grouped with their processes
- **Dependency**: Requires Entry 1 (1318466191)
- **Status**: EnabledState = 2 (Enabled)

### Entry 3: Task Manager Termination Fix

- **ViVetool ID**: 45036792
- **CFR RKey**: 4027031693
- **Purpose**: Fixed - Task Manager cannot terminate the process using the [X] button
- **Affected Build**: Windows 11 Insider Preview Build 28000+
- **Status**: EnabledState = 2 (Enabled)

## Registry Value Meanings

- **EnabledState = 0x00000002 (2)**: Feature is enabled
- **EnabledStateOptions = 0x00000000 (0)**: Use default options

Alternative values:

- `EnabledState = 0x00000001 (1)`: Feature is disabled
- `EnabledState = 0x00000000 (0)`: Feature is default/unset

## ControlSet001 vs ControlSet002

Windows typically maintains two control sets:

- **ControlSet001**: Usually the active control set
- **ControlSet002**: Backup control set

This fix targets ControlSet001 (the active control set). For redundancy, you may also apply the same settings to ControlSet002 by replacing "ControlSet001" with "ControlSet002" in the registry path.

## Impact

These changes:

- ✅ Affect Feature Management system-wide
- ✅ Do not disable or remove other services
- ✅ Are reversible through registry deletion
- ✅ Require system restart to take effect
- ⚠️ Are temporary until Microsoft releases official hotfix

## Monitoring Registry Changes

To verify the settings were applied correctly:

```powershell
# Check if the registry keys exist
Get-Item -Path "HKLM:\SYSTEM\ControlSet001\Control\FeatureManagement\Overrides\14" -ErrorAction SilentlyContinue

# View all values in the override key
Get-ItemProperty -Path "HKLM:\SYSTEM\ControlSet001\Control\FeatureManagement\Overrides\14\1318466191"
Get-ItemProperty -Path "HKLM:\SYSTEM\ControlSet001\Control\FeatureManagement\Overrides\14\4188347533"
Get-ItemProperty -Path "HKLM:\SYSTEM\ControlSet001\Control\FeatureManagement\Overrides\14\4027031693"
```

---

**Note**: This is technical reference material. See README.md for user-friendly installation and uninstallation instructions.
