1. Create the PowerShell Script
Step: Open Notepad (or any plain text editor) and paste the following script:

COpy and paste the isolated text paragraph.

!!!Note: You can change the sound to a custom audio file here:  (New-Object Media.SoundPlayer "Do not remove quotation !!Where your audio is!! Change in the code block below.").PlaySync() !!!



Add-Type -AssemblyName System.Windows.Forms

while ($true) {
  $batt = Get-WmiObject win32_battery
  $pct = $batt.EstimatedChargeRemaining
  $charging = $batt.BatteryStatus -in @(2, 6)

  if ($charging -and $pct -ge 80) {
    # Play custom WAV file
    (New-Object Media.SoundPlayer "C:\Windows\Media\Alarm05.wav").PlaySync()

    # Show message box
    [System.Windows.Forms.MessageBox]::Show(
      "Battery is charging and >= 80% - unplug now!",
      "Battery Alert",
      [System.Windows.Forms.MessageBoxButtons]::OK,
      [System.Windows.Forms.MessageBoxIcon]::Warning,
      [System.Windows.Forms.MessageBoxDefaultButton]::Button1,
      [System.Windows.Forms.MessageBoxOptions]::DefaultDesktopOnly
    )
  }

  Start-Sleep -Seconds 60
}







Save this file as:
Batterychecker.ps1

Choose a folder you will remember, e.g.:
C:\Users\<USERNAME>\OneDrive\Documents\Batterychecker.ps1


2. Create the VBScript Launcher
Purpose: The VBScript runs your PowerShell script hidden, so no console window appears.

Step: Open Notepad again and paste:

Copy paste the isolated paragraph. !!!EXAMPLE LOCATION BELOW CHANGE THE LOCATION AFTER -File TO WHERE YOU STORED YOUR.PS1!!!





Set objShell = CreateObject("Wscript.Shell")
objShell.Run "powershell.exe -ExecutionPolicy Bypass -File ""C:\Users\<USERNAME>\OneDrive\Documents\Batterychecker.ps1""", 0, False






Replace the path after -File if your .ps1 script is saved somewhere else.

Save this as:
RunBatteryChecker.vbs

Save it in a convenient location, for example:
C:\Users\<USERNAME>\OneDrive\Documents\RunBatteryChecker.vbs                 NOT AUTO WHEN STARTUP SEE NEXT STEP FOR AUTO


3. Place the VBScript in the Startup Folder
Step: Open the Startup folder:

Press Win + R, type:
shell:startup

Press Enter.

COPY OR MOVE your RunBatteryChecker.vbs file (or a shortcut to it) into this folder.

4. Testing
Double-click the RunBatteryChecker.vbs file to test if it runs silently.

If your battery is charging and above 80%, you should get the popup alert with sound.

No PowerShell window will show.

