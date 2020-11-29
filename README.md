# Windows Subsystem for Linux
My custom setup step by step instructions

## Base WSL2 Setup

[Reference](https://docs.microsoft.com/en-us/windows/wsl/install-win10)

Requires at a minimum Windows 10 1903 18362.1049

1. Make sure the Windows 10 build revision is **greater than 1049**, in case it isn't
   - Run *Windows Update* or
   - Download and run the [update](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4566116) manually
1. Enable the WSL
   - Using Powershell as Admin
      ```
      dism /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
      ```
1. Enable the Virtual Machine Platform
   - Using Powershell as Admin
      ```
      dism /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
      ```
1. Download and run the [Linux Kernel Update](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)
1. Set default WSL version to 2
   - Using Powershell
      ```
      wsl --set-default-version 2
      ```
1. Install [Ubuntu 20.04](https://www.microsoft.com/store/apps/9n6svws3rx71) from the Microsoft Store
1. Move Ubuntu to whichever drive you want
   1. Export the distro to tar file
   1. Stop / Unregister previous distro
   1. Import tar file distro specifying installation directory

## Windows Terminal Setup

1. Install the [Windows Terminal](https://aka.ms/terminal) from the Microsoft Store
1. Open the Terminal Settings and add those to the global properties
   ```json
    "copyOnSelect": false,
    "copyFormatting": false,
    "largePasteWarning": true,
    "multiLinePasteWarning": false,
   ```
1. Add the Firewatch scheme to the color schemes ( taken from [here](https://windowsterminalthemes.dev/) )
   ```json
    "schemes": [
        {
            "name": "Firewatch",

            "black": "#585f6d",
            "red": "#d95360",
            "green": "#5ab977",
            "yellow": "#dfb563",
            "blue": "#4d89c4",
            "purple": "#d55119",
            "cyan": "#44a8b6",
            "white": "#e6e5ff",
            "brightBlack": "#585f6d",
            "brightRed": "#d95360",
            "brightGreen": "#5ab977",
            "brightYellow": "#dfb563",
            "brightBlue": "#4c89c5",
            "brightPurple": "#d55119",
            "brightCyan": "#44a8b6",
            "brightWhite": "#e6e5ff",
            "background": "#1e2027",
            "foreground": "#9ba2b2"
        }
    ],
   ```
1. Set default terminal to Ubuntu
1. Powerline fonts installation on Windows
1. Setup Ubuntu terminal

## Ubuntu Setup

...
- default user
- disable root access
- apt upgrade
- git hack for speed on NTFS mounted volumes


## Bash Setup

- go compiler
- powerline-go
- .bashrc

## Visual Studio Code Setup

- install vscode WSL server
- setup VSCode terminal fonts for bash