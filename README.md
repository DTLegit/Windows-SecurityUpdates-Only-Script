# Windows-SecurityUpdates-Only-Script
This script changes the Windows Update Policy settings to receive only security updates by adjusting the Target Release Version policy/registry settings to be locked into the current feature release of the system. This ensures persistence through updates by scheduling a task that regularly checks a timestamp file and currently running Windows release, and updates registry settings when needed.

This script will do the following: 

1. Ensures it’s running as Administrator.
2. Creates a folder (C:\ProgramData\UpdateWindowsUpdatePoliciesAnnually) for helper scripts and a timestamp file.
3. Writes two helper scripts:
  - ApplySecuritySettings.ps1 – applies/updates the registry settings, deletes any pending 
  - ReapplySecuritySettings task, and writes a timestamp.
  - (Accepts an optional -Silent switch to suppress debug output.)
  - CheckSecuritySettings.ps1 – checks the timestamp and registry settings; if conditions are met,  it schedules a one-time task (ReapplySecuritySettings) to run the apply script. (Accepts an optional -Silent switch to suppress debug output.)
4. Registers a scheduled task (CheckSecuritySettings) to run at startup and weekly (with compatibility set to Win8), and passes the -Silent flag and hides the window. Runs under NT AUTHORITY\SYSTEM so no credentials are needed.
5. Immediately runs the ApplySecuritySettings.ps1 script to set policies on initial setup.

It sets the following settings: 

- Sets the Target Release Product Version and Release Version Info to the detected Windows release (Windows 10 or 11) and running Windows feature update (e.g. 24H2) values as detected by the script.
- Enables the deferring of quality updates and differs them by 4 days after release.
- These policies are enacted under the registry path of Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate inside the Windows registry.

This script is made publically available for use and consumption under the terms and conditions set forth by the GNU Public License Version 3, with an additional requirement of proper credit being given if used in other projects. 

NOTE: **This script is considered to be in a finished state. However, additional testing is still required (especially needs to be tested under Windows feature upgrades and older releases of Windows 11) to ensure that this can fully be used under production environments. Any and all testing and feedback/PRs to help fix any potential issues and improve code quality/effifiency with this script is welcome and highly encouraged to hopefully ensure this script gets up to production quality. Thank you in advance for your time to anyone who opts to do so.** 

Credit goes to @Britec from YouTube for the tutorial and method used in this script to configure the security-only update settings and @ChrisTitusTech for the quality update deferral recommendations. 
Thank you so much to the both of them and they are absolute legends! 
