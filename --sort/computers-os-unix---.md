
# reference and cheatsheets

[linux-cheat](https://github.com/cirosantilli/linux-cheat)
Linux tutorials and cheatsheets. Minimal examples. Mostly user-land CLI utilities.

[tldp](https://tldp.org/)
[tldp](https://web.archive.org/web/20210102182957/https://tldp.org/)
[The Linux Documentation Project: Guides](https://www.tldp.org/guides.html)
the linux documentation project.
Linux Documentation Project Guides

[Linux Command Line Cheat Sheet by DaveChild - Download free from Cheatography - Cheatography.com: Cheat Sheets For Every Occasion](https://cheatography.com/davechild/cheat-sheets/linux-command-line/?)

[Learn Linux for Beginners: From Basics to Advanced Techniques [Full Book]](https://www.freecodecamp.org/news/learn-linux-for-beginners-book-basic-to-advanced/)

## android rooting tools

[Android Debloat List](https://github.com/MuntashirAkon/android-debloat-list)

## commands - bash - 13 tools

[trinib/Linux-Bash-Commands: Ultimate list of Linux bash commands, cheatsheets and resources](https://github.com/trinib/Linux-Bash-Commands)

[Unix bash cheatsheet. Hope you find it useful · GitHub](https://gist.github.com/kdev33/d501d5726a6dcc0d1a51879941ec7cd4)

[LZone](http://lzone.de/cheat-sheet/Bash)
Bash Cheat Sheet

[LZone](http://lzone.de/cheat-sheet/Bash%20Regex)
Bash Regex Cheat Sheet

[SS64.com](https://ss64.com/bash/)
An A-Z Index of the Bash command line for Linux.

[SS64.com](https://ss64.com/bash/syntax-keyboard.html)
Bash Keyboard Shortcuts

[Aaron Zauner/community_bash_style_guide](https://github.com/azet/community_bash_style_guide)
Community Bash Style Guide.
[DevHub](https://devhub.io/repos/azet-community_bash_style_guide)
how it was discovered

[GNU🆓](https://www.gnu.org/software/bash/manual/bash.html)
Bash Reference Manual

[bahamas10/bash-style-guide](https://github.com/bahamas10/bash-style-guide)
Bash Style Guide : A style guide for writing safe, predictable, and portable bash scripts (not sh!)

[alexanderepstein/Bash-Snippets](https://github.com/alexanderepstein/Bash-Snippets)
A collection of small bash scripts for heavy terminal users
:star:

[GitHub - gruntwork-io/bash-commons: A collection of reusable Bash functions for handling common tasks such as logging, assertions, string manipulation, and more](https://github.com/gruntwork-io/bash-commons)

[GitHub - ruanyf/simple-bash-scripts: A collection of simple Bash scripts](https://github.com/ruanyf/simple-bash-scripts)

[GitHub EdOverflow/hacks: Some random scripts. Just trying to be like the cool kids.](https://github.com/EdOverflow/hacks)

## commands tools

[Linux Command Library](https://github.com/SimonSchubert/LinuxCommandLibrary)
[F-Droid](https://f-droid.org/app/com.inspiredandroid.linuxcommandbibliotheca)

[Unix Toolbox](http://cb.vu/unixtoolbox.xhtml)
Unix/Linux/BSD commands and tasks which are useful for IT work or for advanced users.

[Linux Commands Cheat Sheet | Linux Training Academy](https://www.linuxtrainingacademy.com/linux-commands-cheat-sheet)

[filetype:pdf linux commands Google Search](https://www.google.com/search?client=firefox-b-1-d&q=filetype%3Apdf+linux+commands)

## distros - FreeBSD tools

[GitHub - sbz/freebsd-commands](https://github.com/sbz/freebsd-commands)

## distros - NixOS tools

[NixOS Wiki](https://nixos.wiki/wiki/Cheatsheet)
A NixOS cheat sheet

## key bindings tools
### How to show and change a key binding

#### key bindings
* Press `CTRL + V`
* Type the key for which you want to change the binding
* The prompt will display the character sequence produced by that key. 
e.g : if after step 1 you press F12, you can get something like `^[[24~` 
(More info : [In bash, how do I bind a function key to a command?](https://stackoverflow.com/a/4201274/2309958) and [Delete keymap and completely disable key in zsh](https://unix.stackexchange.com/a/320432/220566) )

#### create a binding : 
* `bind '"\e[24~":"~"'`
* `bind '"\e[24~":""'`
* `bind '"\e[24~":"who"'`
* `bind '"\e[24~":"ssh hostname\n"'`

#### remove a binding : 
* `bind -x '"\e[24~":""'`

## kill processes without notifying tools

[Killbutmakeitlooklikeanaccident.sh | Hacker News](https://news.ycombinator.com/item?id=32125951)
[Script to inject an exit(0) syscall into a running process. NB: only x86_64 for now!](https://gist.github.com/moyix/95ca9a7a26a639b2322c36c7411dc3be)

## linux categories from reddit tools

GNU/Linux Related:

- Kernel
- GNU
- LinuxAdmin
- LinuxDevices
- FreeGaming/LinuxGaming/OpenSourceGames
- LinuxQuestions/Linux4noobs
- DistroHopping/DistroReviews
- Linux Hardware

Distributions:

- Arch
- elementary OS
- Gentoo
- openSUSE/SUSE
- Slackware
- Solus

Debian based

- Debian
- Bunsen Labs/CrunchBang
- LinuxMint
- MX Linux
- Pop!_OS
- Ubuntu/Kubuntu/Xubuntu/Ubuntu Budgie Remix, Lubuntu

RedHat

- Red Hat
- AlmaLinux
- CentOS
- Fedora
- NavyLinux
- RockyLinux

Unique

- NixOS
- Bedrock

Linux with Proprietary Elements

- Chrome OS

Embedded

- OpenWRT

Linux on Mobile:

- Android
  - Termux
- Jolla (SailfishOS)
- PostmarketOS
- Replicant
- ZeroPhone

Movements:

- Free Culture
- Free Software
- Hack Bloc

Desktop Environments:

- Budgie
- Cinnamon
- Enlightenment/e17
- GNOME
- KDE
- LXDE/LXQt
- XFCE

Learning/resources

- CommandLine
- Linuxadmin
- LinuxDev
- Linux From Scratch
- Linux Projects
- Software Freedom Law Center
- Raspberry Pi Forums
- OSdev

Creativity:

- Blender
- FOSSPhotography
- FreeCAD
- GIMP Chat
- Krita Forums/Chat
- LibreDesign
- LibreOffice
- LibreStudio
- LinuxAudio
- LinuxFilmMaking

Other operating systems:

- AROS
- BSD
- FreeBSD
- Genode
- Haiku
- HelenOS
- HURD
- Minix
- Plan 9

## package manager tools

[Nix OS Docs](https://nixos.org/manual/nix/unstable/package-management/garbage-collection.html)
Garbage Collection
handy commands for reclaiming disk space from deleted packages.

## package manager - rpm tools

[FedoraProject Wiki](https://fedoraproject.org/wiki/Packaging:RPMMacros?rd=Packaging/RPMMacros)
definitions for some common RPM specfile macros

[RPM](http://rpm.org/user_doc/macros.html)
Macro syntax
