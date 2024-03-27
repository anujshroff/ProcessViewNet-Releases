## v10.6
Improvements:
- Encrypted text editor will be hidden from screen sharing. If the Windows API returns false, then the textbox will be hidden.
- A show button has been added to force the textbox to be visible.

## v10.5
Improvements:
- Encryption Tools now includes a standalone base64 encoding and decoding feature.
- Encryption Tools can now be opened via the Ctrl + Alt + E hotkey.
- Ctrl + Alt + T can now be used to open a preset encrypted text file. The file that this hotkey will open can be set from the encrypted text editor with the file in question open.
- HotKey registration status has been moved from the title bar to the status bar.
- HotKeys can now be disabled either in app or through the settings.json file. In app changes must be saved via Ctrl + S.

## v10.4
Improvements:
- Updater will now check to see what the latest compatible version is rather than defaulting to the latest tag.
- Updater now allows for rolling signing keys.
- These settings have been removed from settings.json and are no longer overrideable: 
  - RSAModulus
  - RSAExponent
  - GithubRepoAPIURL
  - RSASignatureBaseURL

## v10.3
Improvements:
- Add file count to disk usage extension breakdown
- Enable sort by column header for extension breakdown

## v10.2
Improvements:
- Disk Usage will now break down disk usage by file extension.

## v10.1
New Features:
- Added Disk Usage function (Ctrl + D).
  - Hide smaller folders (1).
    - Added DiskUsageHideFoldersLessThanBytes setting in settings.json to set cutoff size.
  - Add folder to exclusions list (2).
  - Open folder in explorer (3).

Improvements:
- Better precision handling for human readable byte size conversion

Bug Fixes:
- Corrected a typo in the window style configuration. However, there should be no visible difference.

## v10.0
New Features:
- Status text in the status bar area of all windows can be clicked to access a history of logs from that run of ProcessViewNet.

## v9.10
New Features:
- VirusTotal reports will change to configured VirusTotalAlertColor (default: Red) if Bad or Sus are > 0.
- VirusTotalAlertColor can be configured in settings.json file. Ctrl + S in the app will expose the setting in the file.

Improvements:
- In Encryption Tools, base64 checkbox will now also apply to hash encoding and will not be a default setting.
- Encryption Tools (Ctrl + E) will launch in a new process.

## v9.9
New Features:
- A right click (context menu) option has been added for recalculating the hash for a pvnsettings file. This will show up after reregistering pvn file associations.
- Encrypted Text Editor now has its own Font Family and Font Size settings which can be configured in the Font Selector or in the settings file. Re-save the settings file (Ctrl + S) to expose the setting names.
- Alternate Data Streams can now be copied to new file's default stream for convenience.

Improvements:
- Hash failures of pvnsettings files can be bypassed allowing for use of pvnsettings file anyway.
- Proceeding to use a hash failed pvnsettings file will trigger an option to recalculate the hash and update the pvnsettings file.

## v9.8
Improvements:
- Message dialog boxes with only one button (Close, etc) and no other controls can be closed by hitting enter or escape

Bug Fixes:
- Properly show base64 decoding and decryption failure error messages when opening a pvnsettings file

## v9.7
New Features:
- Encrypted Text Editor generates a pvnsettings file that contains relevant encryption settings information
  - This can be disabled
  - pvnsettings file can be registered to open with Encryption Tools
    - Clicking on pvnsettings file will ask for the password or the key and iv reading other settings from the file
  - Clicking on pvn file will look for a pvnsettings file (appends .pvnsettings to pvn filename) to help read settings
    - This can also be disabled

Improvements:
- Encryption Tools closes files as soon as possible thus releasing locks sooner
- Ensure input and output file names are not the same
- Add clear form button in Encryption Tools to clear out textboxes

Bug Fixes:
- Help text corrected to reflect that the print screen function generates PNGs instead of BMPs
- Saving a non-base64 encoded file from within the encrypted text editor no longer fails

## v9.6
New Features:
- Encrypted Text Editor now shows character count on the status bar
- Encrypted Text Editor status bar will show a performance warning if the character count is 250,000 characters or more

Improvements:
- Use RandomNumberGenerator instead of RNGCryptoServiceProvider for generating salts

Bug Fixes:
- Tray Icon will be disabled and re-enabled every minute for the 1st 5 minutes. This is to work around ProcessViewNet occasionally starting before explorer does (via Task Scheduler), often after rebooting for updates.

## v9.5
Bug Fixes:
- Update process will properly use the public key specified in the settings.json file when verifying the signature of the downloaded update. Previously, the settings.json override was being ignored making the public key override feature almost useless.

## v9.4
Improvements:
- When opening a pvn file through explorer (double click, etc), application shutdown mode will be set to last window allowing the user to close the Encryption Tools window while leaving open the Encrypted Text Editor.
- Application loader will check the running .NET Framework version showing an error message and gracefully exiting if the minimum version requirement has not been met.

## v9.3
New Features:
- In Encryption Tools, a password confirmation textbox has been added which will be checked when deriving a key and iv from a password during encryption or open new text editor functions.

Improvements:
- KeyDown event handling has been moved from ListView to Window which will catch key presses as long as the window has focus regardless of which control on the window has focus.

Bug Fixes:
- When printing from the encrypted text editor, the column width will be set to the document page width to eliminate multiple columns on a single page.

## v9.2
New Features:
- Encryption Tools now has a built-in text editor.
    - Text files can be decrypted to this text editor instead of disk.
    - An option to create a new encrypted text file through the text editor.
    - Saving from the editor will write the file to disk with the encryption settings specified when the editor was opened.
    - Basic print functionality.
- .pvn extension can be associated with Encryption Tools making opening an encrypted file easier by double clicking it.

Improvements:
- When ProcessViewNet starts as a scheduled task, it will relaunch itself relieving Task Scheduler of any supervisory burden.

Bug Fixes:
- Use UTF8 encoding and decoding for Encryption Tools.
- Salt header will be preserved, if found, when using Manual Key mode.

## v9.1
New Features:
- Remote IP addresses can be submitted to VirusTotal in the Open Ports function.

Improvements:
- When using the encryption tools, the hashing function will display hashes in the output text box instead of writing to a file.
- VirusTotal results will have a tool tip showing the age of the results.

Bug Fixes:
- VSS unmanaged resources will properly be deallocated.

## v9.0
New Features:
- VirusTotal Integration
    - Right click a process, driver, or process module and select Scan with VirusTotal
    - First submission will popup a terms of service agreement dialog
    - You will need to set your API Key (free signup @ virustotal.com) in this dialog and accept the terms of service
    - Hit Ctrl + S to save settings and expose additional settings
    - VirusTotalMaxScanAgeDays (default 30) is the max age, in days, of a previous scan to accept
        - Older scans will trigger a rescan request
        - Files not found will trigger a file upload (Up to 190.37 MB)
    - VirusTotalAnalysisRecheckIntervalSeconds (default 60) is the polling interval, in seconds, for checking a scan that is queued or in progress
    - VirusTotalScanTimeoutMinutes (default 5) is the max time, in minutes, the entire process can take before timing out
        - Slow upload of file
        - Scan stuck in queued or in-progress state
- Font Profiles can be added in settings file
- Font Profile can be selected in the font selector context menu

Improvements:
- Screenshots function will save files as PNGs instead of BMPs

Bug Fixes:
- Screenshots function was cutting off 3/4 of some screenshots. It should now be able to get actual rectangle sizes in those scenarios so a full screenshot can be taken.
- Path cleaning will ensure the cleaned file or directory path exists. If not, the original returned value from the Windows API will be preserved.