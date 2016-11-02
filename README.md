# CrashLogger
<b>Microsoft Office 2016 Crash Logger Tool</b>

Purpose: Configures the computer to log and archive Office 2016 crash reports</br>
Usage: `CrashLogger [--Install] [--Uninstall] [--ViewLog]`</br>
Example: `CrashLogger --Install`</br>

NOTE: CrashLogger requires Microsoft Office 2016 for Mac 15.28 or later</br>

<b>How CrashLogger works</b></br>
CrashLogger leverages a new ability in Office 2016 15.28 to save the last crash log to disk.</br>
When `CrashLogger --Install` is run, the following occurs:<br>
1. The CrashLogger script is copied to `$HOME/Library/Application Support/com.microsoft.CrashLogger`<br>
2. A scratch area is created: `$HOME/Library/Group Containers/UBF8T346G9.ms/MerpScratch/`<br>
3. An archive area is created: `$HOME/Library/Group Containers/UBF8T346G9.ms/MerpArchive/`<br>
4. A LaunchAgent is configured to monitor the creation of new crash reports</br>
5. MERP crash logging is enabled through `defaults write com.microsoft.errorreporting IsStoreLastCrashEnabled -bool TRUE`</br>


<b>What happens when an Office application crashes?</b></br>
1. Microsoft Error Reporting will send the crash report to the Watson server and then persist the log to disk at `$HOME/Library/Group Containers/UBF8T346G9.ms/MerpTempItems/LastSentCrashReport.zip`</br>
2. The LaunchAgent will be triggered</br>
3. The LaunchAgent unzips the crash log, extracts key information, then moves the report to the archive area using a file name based on the date and time of the crash</br>
4. The LaunchAgent writes a one-line summary of the crash to `$HOME/Library/Group Containers/UBF8T346G9.ms/MerpArchive/CrashSummary.txt`</br>
5. The LaunchAgent will send the one-line summary to the console log</br>


<b>Example of console log entry</b></br>
`11/1/16 7:34:21.943 PM pbowden[60463]: com.microsoft.CrashLogger 2016-11-02 02:34:17 com.microsoft.Excel 15.28.0.161031 SIG_FORCE_QUIT 29c2 CrashReport-161101-193421.txt`
