# Matter Build Environment

How to create a Matter build environment for the [Silicon Labs Github Matter repository](https://github.com/SiliconLabs/matter) using Ubuntu Desktop on VirtualBox

## VirtualBox

1. Download and install the [VirtualBox](https://www.virtualbox.org/wiki/Downloads) installation for you platform

2. In VirtualBox, click the *New* button to create a new virtual machine to open the new virtual machine wizard

3. On the *Name and operating system page:*
   Set *Name* to your preference, I used: `Ubuntu 22.04.1 Desktop AMD64`
   Set *Machine Folder* to your preference, I used the default folder
   Set *Type*: `Linux`, this will automatically be selected if `Ubuntu` is included in your machine *Name*
   Set *Version*: `Ubuntu (64-bit)` this will automatically be selected if `Ubuntu` is included in your machine *Name*

4. On the *Memory size* page, set to: `8192MB`

5. On the *Hard disk* page, select `Create virtual hard disk now`

6. On the *Hard disk file type* page, select: `VDI`

7. On the *Storage on physical hard disk* page, select `Dynamically allocated`

8. On the *File location and size* page: use the default folder or select to your preference, set a minimum of `64 GB` for the maximum file size

9. The wizard is complete and the new virtual machine should appear in the main VirtualBox window

### VirtualBox References

* [How to run Ubuntu on a virtual machine using VirtualBox](https://ubuntu.com/tutorials/how-to-run-ubuntu-desktop-on-a-virtual-machine-using-virtualbox#1-overview)

## Ubuntu

1. Download the Ubuntu installation, at the time of writing the current version is 22.04.1 available from the main [Download Ubuntu Desktop](https://ubuntu.com/download/desktop) page, previous versions can be downloaded from the *Past releases and other flavours* section of the [Alternative Downloads](https://ubuntu.com/download/alternative-downloads) page

2. In the VirtualBox main window, select the virtual machine and click *Start*

3. The first time a virtual machine is started a *Select start-up disk* window will be opened, select downloaded Ubuntu .iso file

4. When the .iso loads, press `Enter` to select `Try or install Ubuntu`

5. On the *Welcome* screen, select your language and click `Install Ubuntu`

6. On *Keyboard layout*, select your country and layout

7. On *Updates and other software*, select `Minimal installation` and `Download updates while installing Ubuntu`

8. On *Installation Type*, select `Erase disk and install Ubuntu`

9. On *Where are you?*, select your location

10. On *Who are you?* set to your preference, I used:
    *Your name*: `Ubuntu`
    *Your computer's name*: `Ubuntu Desktop`
    *Pick a username*: `ubuntu`
    *Password*: `matter`
    *Log in*: `Require my password to log in`
    *Use Active Directory*: `No`

11. Ubuntu will then install and reboot

12. Complete the post install wizard according to your preferences 

13. When prompted by the *Software Updater*allow Ubuntu to install updates and reboot

14. Use the *Applications* screen to open the *Settings* application and set *Screen Display > Resolution* to your preference, it may be useful to pin the *Settings* application to the *Favourites* bar by right-clicking it in the *Applications* screen

15. Use the *Applications* screen to open the *Terminal*, this is another application worth adding to the *Favourites* bar

16. In the *Terminal*, issue the following commands: 
    `sudo apt update` to update the available application packages
    `sudo apt upgrade -y` to upgrade installed packages to the latest version, without prompts
    `sudo apt install gcc make perl` to install dependencies for the next step

17. On the virtual machine's menu bar, select *Devices > Insert Guest Additions CD image...*

18. If the CD doesn't run and install automatically: 
    Right-click the CD on the *Favourites* bar and select `New Window`
    In the *Files* window that opens, right-click in the blank space and select `Open in Terminal`
    Enter the command `sudo ./VBoxLinuxAdditions.run install` to install the guest additions
    Enter the command `sudo usermod -aG vboxsf $(whoami)` to allow the current user to access folders shared with the host machine
    Right-click the CD on the *Favourites* bar and select `Eject`
    Reboot the virtual machine to complete the guest additions installation

19. Now the guest additions are installed the virtual machine's *Devices* menu can be used to configure shared folders and a shared clipboard

### Ubuntu References

* [How to run Ubuntu on a virtual machine using VirtualBox](https://ubuntu.com/tutorials/how-to-run-ubuntu-desktop-on-a-virtual-machine-using-virtualbox#1-overview)

* [virtualbox - Guest Additions not working - Ask Ubuntu](https://askubuntu.com/a/1416292)

## Matter Build Environment

1. Open the *Terminal* application and issue the following commands:

2. `sudo apt-get install git gcc g++ pkg-config libssl-dev libdbus-1-dev libglib2.0-dev libavahi-client-dev ninja-build python3-venv python3-dev python3-pip unzip libgirepository1.0-dev libcairo2-dev libreadline-dev` 
   to install dependencies and utilities for the Matter build environment

3. `git clone https://github.com/SiliconLabs/matter` 
   to clone the Silicon Labs Matter Github repository (v0.3.0 at the time of writing):

4. `cd matter` to move to the *Matter* folder

5. `git submodule update --init --recursive`
   to initialise and update the repository submodules

6. `./scripts/examples/gn_efr32_example.sh ./examples/lighting-app/efr32/ ./out/lighting-app BRD2601B`
   to build the lighting app example for the EFR32MG24/BRD2601B development board, different examples and boards can be selected on the command line, see the individual readme files in the individual examples folders for lists of supported boards

### Matter Build Environment References

* [Matter Software Requirements](https://github.com/SiliconLabs/matter/blob/release_0.3.0/docs/silabs/general/SOFTWARE_REQUIREMENTS.md) (from [Silicon Labs Github Matter repository](https://github.com/SiliconLabs/matter))

* [CHIP EFR32 Lighting Example](https://github.com/SiliconLabs/matter/blob/release_0.3.0/examples/lighting-app/efr32/README.md) (from [Silicon Labs Github Matter repository](https://github.com/SiliconLabs/matter))

## Ubuntu Applications

The following applications will be of use in the Ubuntu virtual machine:

* [J-Link from Segger (64-bit DEB Installer)](https://www.segger.com/downloads/jlink/), command-line flash programmer and debugger, used by Simplicity Commander
  To install: right-click download and select `open with other application` then `Software Install`

* [Simplicity Commander](https://www.silabs.com/developers/mcu-programming-options): GUI flash programmer, use the virtual machine *Devices > USB* menu entries to connect USB devices from the host machine to the virtual machine
  To install: extract ZIP, extract .tar.bz, copy *commander* folder to Home* folder, the run the *commander* application from the folder

* [Visual Studio Code](https://code.visualstudio.com/), feature-rich text editor for software development
  To install: right-click download and select `open with other application` then `Software Install`

(end)














































































































































































































































