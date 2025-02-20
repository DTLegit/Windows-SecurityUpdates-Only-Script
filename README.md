# Windows-SecurityUpdates-Only-Script
This script changes the Windows Update Policy settings to receive only security updates by adjusting the Target Release Version policy/registry settings to be locked on to the current feature release of the system. This ensures persistence through updates by scheduling a task that checks a timestamp file and updates registry settings when needed.
