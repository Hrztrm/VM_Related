# VM_Related

## What I Usually Do

0. Create a snapshot of the base "BASE". Nothing done on it, just do the fresh install Windows OS installation things. 
1. Go to https://ninite.com/ and install some applications. Recommended are:
	1. Firefox
	2. Chrome
	3. 7-zip
	4. Thunderbird (Sometimes)
	5. Notepad++
	6. Everything
```
https://ninite.com/7zip-chrome-everything-firefox-notepadplusplus-thunderbird/ninite.exe
as of 21/2/2024
```
2. Remove unneeded application i.e "People", "Maps", "Xbox", "Cortana". Do this sparingly.

```
Some things to uninstall
Feedback Hub
Game Bar
Get Help
Mixed Reality Portal
Phone Link
Microsoft To Do Lists

To change 
Disable Web Results through Search Bar

1. Open RegEdit and go to HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows
2. Create New DWORD key called DisableSearchBoxSuggestions
3. Set the data value to 1
4. Reboot
```
3. Disable the "News and Interests" taskbar
4. Go through the installed applications so you don't have to go through the "Fresh Install Application. Want to sync..." prompts every time you revert snapshot.
5. Shutdown and create a snapshot now. 
	- Name it as "Base - Uninstalled Fluff and Installed Applications". 
	- Description will put the installed applications and the login credentials. 

```Powershell
# Script to do everything I said here, except of creating a snapshot
# Ninite Installation. If you have problems here, open microsoft edge first, before running this script.
$url = "https://ninite.com/7zip-chrome-everything-firefox-notepadplusplus-thunderbird/ninite.exe" 
$outputPath = "C:\Users\Public\ninite.exe" 
Invoke-WebRequest -Uri $url -OutFile $outputPath
saps $outputPath
sleep(1)
del $outputPath

#Uninstall Fluffs

# Disable Web Results in Search Bar
# Create the registry key and set its value 
$regPath = "HKCU:\Software\Policies\Microsoft\Windows\Explorer" 
$keyName = "DisableSearchBoxSuggestions" 

# Checks if the key exists or not
if (!(Test-Path -Path $regPath)) { 
	New-Item -Path $regPath -Force 
}

# The disabling part
New-ItemProperty -Path $regPath -Name $keyName -PropertyType DWORD -Value 1 -Force 


#Shutdowns the Computer
#Stop-Computer
```

Better Event logs
https://github.com/Yamato-Security/EnableWindowsLogSettings/blob/main/YamatoSecurityConfigureWinEventLogs.bat

Configuration (Bloatware Removal n stuff)
https://privacy.sexy

Some tool
https://kurtzimmermann.com/index_e.html#features6-2
