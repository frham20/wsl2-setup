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
1. Reboot
1. Download and run the [Linux Kernel Update](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)
1. Set default WSL version to 2
   - Using Powershell
      ```
      wsl --set-default-version 2
      ```
1. Install [Ubuntu 20.04](https://www.microsoft.com/store/apps/9n6svws3rx71) from the Microsoft Store
   1. Launch it
   1. Create user account and set password
   1. Close the ubuntu terminal
1. *(optional)* Move Ubuntu to whichever drive you want
   1. Export the distro to tar file
      ```
       ...
      ```
   1. Stop / Unregister previous distro
      ```
       ...
      ```
   1. Import tar file distro specifying installation directory
      ```
       ...
      ```
1. Set the default distro in WSL
   ```
   wsl --set-default Ubuntu-20.04
   ```

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
   - Find the profile entry for Ubuntu-20.04
   ```json
   {
      "guid": "{07b52e3e-de2c-5db4-bd2d-ba144ed6c273}",
      "hidden": false,
      "name": "Ubuntu-20.04",
      "source": "Windows.Terminal.Wsl"
   }
   ```
   - Copy the guid field into the global *defaultProfile* setting
   ```json
   "defaultProfile": "{07b52e3e-de2c-5db4-bd2d-ba144ed6c273}",
   ```
1. Install the Powerline fonts on Windows
   - Open a Powershell terminal
   - Clone the powerline fonts repository from github and install the fonts
      ```
      git clone https://github.com/powerline/fonts
      cd fonts
      ./install.ps1
      ```
1. Setup Ubuntu terminal to use the proper color scheme and font
   ```json
   {
      "guid": "{07b52e3e-de2c-5db4-bd2d-ba144ed6c273}",
      "hidden": false,
      "name": "Ubuntu-20.04",
      "source": "Windows.Terminal.Wsl",
      "colorScheme": "Firewatch",
      "fontFace": "Noto Mono for Powerline",
      "fontSize": 10,
      "startingDirectory": "\\\\wsl$\\Ubuntu-20.04\\home\\fhamel"
   }
   ```

## Ubuntu Setup
1. Open a terminal to Ubuntu
1. Disable Root Access
   ```bash
   sudo passwd -l root
   ```
1. Update & Upgrade the packages
   ```bash
   sudo apt update
   sudo apt upgrade
   ```
1. git hack for speed on NTFS mounted volumes


## Bash Setup
1. Open a terminal to Ubuntu
1. Set Bash as the default shell
   ```bash
   chsh -s /bin/bash
   ```
1. Close and reopen the terminal
1. Install [powerline-go](https://github.com/justjanne/powerline-go)
   1. Install the GO language package
      ```bash
      sudo apt install golang-go
      ```
   1. Download the GO based powerline-go package
      ```bash
      go get -u github.com/justjanne/powerline-go
      ```
1. Edit .bashrc file in the user root directory
   1. Comment everything related to setting the PS1 var
   1. Add this to the end
      ```bash
      # Support for powerline-go
      function _update_ps1() {
          PS1="$($HOME/go/bin/powerline-go -hostname-only-if-ssh -colorize-hostname -error $?)"
      }

      if [ "$TERM" != "linux" ] && [ -f "$HOME/go/bin/powerline-go" ]; then
         PROMPT_COMMAND="_update_ps1; $PROMPT_COMMAND"
      fi
      ```
   1. Save and close


## Visual Studio Code Setup

- install vscode WSL server
- setup VSCode terminal fonts for bash