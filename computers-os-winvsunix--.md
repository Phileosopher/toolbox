
## cli tools

[GitHub - mridgers/clink: Bash's powerful command line editing in cmd.exe](https://github.com/mridgers/clink)
[GitHub - chrisant996/clink: Bash's powerful command line editing in cmd.exe](https://github.com/chrisant996/clink)

[operable/cog](https://github.com/operable/cog/)
Bringing the power of the command line to chat
Via [Choosing a Chatbot:From Hubot to Yetibot, What You Need to Know](https://victorops.com/blog/choose-chatbotfrom-hubot-yetibot-need-know)
> Cog is engineered to be more of a framework that addresses a number of concerns many teams have, such as security. With built-in access control and audit logging functionality, Cog allows teams to collaborate on sensitive tasks with higher confidence. Taking inspiration from the command-line interface, Cog has a “pipe” operator that allows users to run a command and use that output as the input for another command in a process.

## file transfer tools

[CDC File Transfer | Hacker News](https://news.ycombinator.com/item?id=34303497)
[GitHub - google/cdc-file-transfer: Tools for synching and streaming files from Windows to Linux](https://github.com/google/cdc-file-transfer)

## windows vs linux features tools

[Paste selected text on Windows like on Linux (middle mouse button) - Super User](https://superuser.com/questions/1349626/paste-selected-text-on-windows-like-on-linux-middle-mouse-button)

## WSL enable tools
## Enable Windows Subsystem for Linux on Windows 10

* as admin : 
`dism /online /Enable-Feature /NoRestart /FeatureName:Microsoft-Windows-Subsystem-Linux` 

* create AppModelUnlock if it doesn't exist, required for enabling Developer Mode. Sources :
  * https://stackoverflow.com/questions/40033608/enable-windows-10-developer-mode-programmatically#40033638
  * https://www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10/
  * https://gallery.technet.microsoft.com/scriptcenter/Enable-developer-mode-27008e86

```registry
$registryUpdates = @{
    "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\AppModelUnlock\AllowDevelopmentWithoutDevLicense" = 1
}
$registryUpdates.GetEnumerator() | ForEach-Object {
    & reg add (Split-Path -Parent $_.Key) /v (Split-Path -Leaf $_.Key) /t REG_DWORD /d $_.Value /f | Out-Null
}
```

## WSL tools

[Windows Subsystem for Linux GUI | Hacker News](https://news.ycombinator.com/item?id=28486133)
[GitHub - microsoft/wslg: Enabling the Windows Subsystem for Linux to include support for Wayland and X server related scenarios](https://github.com/microsoft/wslg)

[Microsoft's Linux Kernel | Hacker News](https://news.ycombinator.com/item?id=20309311)
[GitHub - microsoft/WSL2-Linux-Kernel: The source for the Linux kernel used in Windows Subsystem for Linux 2 (WSL2)](https://github.com/microsoft/WSL2-Linux-Kernel)
