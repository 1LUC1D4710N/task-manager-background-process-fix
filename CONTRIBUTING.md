# Contributing

Thank you for your interest in the Task Manager Background Process Fix project!

## About This Project

This is a registry-based fix for Windows 11 that resolves an issue where the Task Manager process might continue to run in the background after the app is closed, causing process duplication and resource waste.

**Status**: ✅ Community-maintained workaround (temporary until Microsoft releases an official hotfix)

## How to Use

1. **For Users**: See [QUICK_START.md](QUICK_START.md) for simple installation steps
2. **For Detailed Info**: See [README.md](README.md) for comprehensive documentation
3. **For Technical Details**: See [TECHNICAL_DETAILS.md](TECHNICAL_DETAILS.md)

## Reporting Issues

If you encounter any problems:

1. Check if your issue is already reported in the [Issues](https://github.com/1LUC1D4710N/task-manager-background-process-fix/issues) section
2. Provide detailed information:
   - Windows version and build number
   - Whether the fix worked or not
   - Any error messages encountered
   - Steps to reproduce (if applicable)

## Suggesting Improvements

Have suggestions for improvements?

1. Check existing [Issues](https://github.com/1LUC1D4710N/task-manager-background-process-fix/issues) and [Pull Requests](https://github.com/1LUC1D4710N/task-manager-background-process-fix/pulls)
2. Create a new issue with:
   - Clear title and description
   - Why this improvement would be helpful
   - Your proposed solution (if you have one)

## Important Advisory

⚠️ **This is a temporary workaround**

Once Microsoft releases an official hotfix for this issue, users should:
1. Apply the Microsoft hotfix
2. Delete the `HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\FeatureManagement\Overrides\14` registry key
3. Remove this workaround

## Testing & Verification

If you test this fix, please share your results:
- Windows version/build
- Whether the fix resolved the issue
- Any side effects observed
- Duration of the fix effectiveness

## Sources & Attribution

This fix is based on:
- Community findings from [Make Tech Easier](https://www.maketecheasier.com/fix-windows-task-manager-duplication-bug/)
- Original registry file from [SimonMacer/CreateMediaRefresh25H2](https://github.com/SimonMacer/CreateMediaRefresh25H2)
- Testing methodology from [kill-taskmgr-script](https://github.com/1LUC1D4710N/kill-taskmgr-script)

## License

This project is licensed under the MIT License - see [LICENSE](LICENSE) file for details.

## Disclaimer

This fix modifies Windows registry settings. Use at your own risk:
- Always backup your registry before applying
- Test in a safe environment first
- Restart your system after applying
- Keep backups for easy reversal

## Questions?

Feel free to open an [Issue](https://github.com/1LUC1D4710N/task-manager-background-process-fix/issues) with your questions!

---

**Last Updated**: November 2025
