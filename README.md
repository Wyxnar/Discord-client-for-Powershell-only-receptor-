<div align="center">
<br>
<img src="assets/blackcaticon.png" width="20%" />
<br>
B L A C K - C A T
<br>
</div>
<br>
<br>

1. [Info](#info)
2. [Prerequisites](#prerequisites)
3. [Installation & Usage](#installation--usage)
4. [Support](#support)

## Info

A way to see last Discord messages in PowerShell (beta)

## Prerequisites
OS: Windows 11 (To verify, press Win + R, type "winver", and hit Enter).
PowerShell: Version 5.1 or higher (Pre-installed on Windows 11).
## Installation & Usage
1. Enter your desktop, Right Click and click New and create a Text Document.
2. Open the document and paste the code provided in the "Code" file.
3. Go to lines 2 and 3. (Line 4 is optional; if you only want one user, delete line 4. If not, follow the same steps as line 3).
4. To get your Token: Open Discord, press F12 (or Ctrl + Shift + I), go to the Console tab and paste this code:
```bash
(webpackChunkdiscord_app.push([[''],{},e=>{m=[];for(let c in e.c)m.push(e.c[c])}]),m).find(m=>m?.exports?.default?.getToken!==void 0).exports.default.getToken()
```
5. Copy the result (it looks like a long string of characters). IMPORTANT: Do not share this token with anyone.
6. In line 2 of your text document, paste the token replacing YOUR-TOKEN-HERE.
7. In line 3, replace INSERT-USER-1-NAME with the name of the person. Then, replace INSERT-CHAT-ID with the numbers found at the end of the Discord chat URL.
8. Click File > Save As. In "Save as type", choose "All Files (.)". Name the file and ensure it ends with .ps1 (Example: script.ps1).
9. Open Windows PowerShell and type the following command (replace FILENAME with your file's name): Set-ExecutionPolicy Bypass -Scope Process; & ".\FILENAME.ps1"
10. If everything is correct, the user's name will appear next to a number. Type that number to see the recent messages.
    
## Support
If you have any issues, contact me on Discord: wyxnar.
