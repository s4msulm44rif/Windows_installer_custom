# UnattendedWinstall

## Introduction

UnattendedWinstall leverages Microsoft's [Answer Files](https://learn.microsoft.com/en-us/windows-hardware/manufacture/desktop/update-windows-settings-and-scripts-create-your-own-answer-file-sxs?view=windows-11) (or Unattend files) to automate and customize Windows installations. </br> It enables modifications to Windows Settings and Packages directly in the Windows ISO during setup.

### Why Use an Answer File?

#### Security

- Provides transparency by allowing inspection of all changes in the answer file.
- Runs directly on official Windows ISOs from Microsoft, eliminating the need for unofficial sources.
- Utilizes a Microsoft-supported feature designed for streamlined mass deployment of Windows installations.

#### Automation

- Enables automated configuration across multiple devices, saving time and effort by eliminating repetitive manual setups.

> [!NOTE] 
> UnattendedWinstall has been tested and optimized for personal use. For those interested in customizing further, [create your own answer file](https://schneegans.de/windows/unattend-generator/) following [this video guide](https://youtu.be/WyLiJl-NQU8).

### Versions

[![Version 2 Release (Latest)](https://img.shields.io/badge/Version-2.1.0%20Latest-0078D4?style=for-the-badge&logo=github&logoColor=white)](https://github.com/memstechtips/UnattendedWinstall/releases/tag/v2.1.0)
[![Version 1 Release](https://img.shields.io/badge/Version-1.0.0-FFA500?style=for-the-badge&logo=github&logoColor=white)](https://github.com/memstechtips/UnattendedWinstall/releases/tag/v1.0.0)

### Support the Project

If UnattendedWinstall has been useful to you, consider supporting the project, it really does help!

[![Support via PayPal](https://img.shields.io/badge/Support-via%20PayPal-FFD700?style=for-the-badge&logo=paypal&logoColor=white)](https://paypal.me/memstech)

### Feedback and Community

If you have feedback, suggestions, or need help with UnattendedWinstall, please feel free to join the discussion on GitHub or our Discord community:

[![Join the Discussion](https://img.shields.io/badge/Join-the%20Discussion-2D9F2D?style=for-the-badge&logo=github&logoColor=white)](https://github.com/memstechtips/UnattendedWinstall/discussions)
[![Join Discord Community](https://img.shields.io/badge/Join-Discord%20Community-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://www.discord.gg/zWGANV8QAX)

## Requirements

- Windows 10 or Windows 11  
  - *(Tested on Windows 10 22H2 & Windows 11 24H2)*
  - *(32-bit, 64-bit and arm64 is supported)*

## What Does UnattendedWinstall Do?

The UnattendedWinstall answer file comes with detailed descriptions for nearly all configurations and registry tweaks, which are available for inspection here on GitHub. For customization, download the answer file and open it in editors like [Cursor](https://www.cursor.com/) or [VSCode](https://code.visualstudio.com/).

### Sources and Contributions

<details>
  <summary>Click to Show</summary>

- **Base Answer File Generation**:
  - [Schneegans Unattend Generator](https://schneegans.de/windows/unattend-generator/)
- **Tweaks & Optimizations**:
  - [ChrisTitusTech WinUtil](https://github.com/ChrisTitusTech/winutil)
  - [FR33THY's Ultimate Windows Optimization Guide](https://github.com/FR33THYFR33THY/Ultimate-Windows-Optimization-Guide)
- **Additional Tweaks**:
  - [Tiny11Builder](https://github.com/ntdevlabs/tiny11builder)
  - [Ten Forums](https://www.tenforums.com/)
  - [Eleven Forum](https://www.elevenforum.com/)
  - [Winaero Tweaker](https://winaerotweaker.com/)

</details>

### Key Features

- Ability to choose Windows Edition (Pro is not enforced anymore as in v2.0.0)
- Bypasses Windows 11 system requirements
- Disables Windows Defender services by default
  - *prompted to enable after Windows installation*
- Disables User Account Control by default
  - *prompted to enable after Windows installation*
- Allows execution of PowerShell scripts by default
- Skips forced Microsoft account creation during Windows setup
- Removes preinstalled bloatware apps except Microsoft Edge, Notepad and Calculator
  - Copilot and Recall is Disabled.
- Sets privacy-related registry keys to disable telemetry
- Limits Windows Update to install only security updates for one year
- Optimizes registry with various optimization and customization-related keys
  - *See the "Set-RecommendedHKLMRegistry" and "Set-RecommendedHKCURegistry" functions for more information*
- Disables unnecessary scheduled tasks
- Configures Windows services for optimal performance
- Enables the Ultimate Performance power plan

> [!NOTE] 
> Use the `UWScript.ps1` file once Windows is installed to reapply or revert settings in case Windows Update resets some of the settings or if you encounter any issues.  
> It can also be used to achieve a similar experience to UnattendedWinstall on an existing Windows installation without reinstalling Windows.
>
> ---
>
> **Before Running the Script**
>
> Ensure you open PowerShell as an administrator. Additionally, set the execution policy to allow script execution by running the following command:
>
> ```powershell
> Set-ExecutionPolicy Unrestricted
> ```
>
> Running PowerShell with elevated permissions and enabling script execution will ensure that `UWScript.ps1` can apply the necessary system changes.

## Usage Instructions

To use an answer file, include `autounattend.xml` at the root of your Windows Installation Media to be executed during Windows setup.

> [!IMPORTANT]  
> Ensure the answer file is named `autounattend.xml`; otherwise, it won’t be recognized by the installer.

---

### Using Memory's [WIMUtil](https://github.com/memstechtips/WIMUtil) (Highly Preferred)

To use **WIMUtil**, follow these steps to launch PowerShell as an Administrator and run the installation script:

1. **Open PowerShell as Administrator:**
   - **Windows 10/11**: Right-click on the **Start** button and select **Windows PowerShell (Admin)** or **Windows Terminal (Admin)**. </br> PowerShell will open in a new window.

2. **Confirm Administrator Privileges**: 
   - If prompted by the User Account Control (UAC), click **Yes** to allow PowerShell to run as an administrator.

3. **Paste and Run the Command**:
   - Copy the following command:
     ```powershell
     irm "https://github.com/memstechtips/WIMUtil/raw/main/src/WIMUtil.ps1" | iex
     ```
   - To paste into PowerShell, **Right-Click** or press **Ctrl + V** in the PowerShell or Terminal window. </br> This should automatically paste your copied command.
   - Press **Enter** to execute the command.

Once launched, **WIMUtil** guides you through a wizard:

1. **Select or Download Windows ISO**
2. **Add Latest UnattendedWinstall Answer File Automatically**
3. **Extract and Add Current Device Drivers to Installation Media**
4. **Create New ISO with Customizations Included**
5. **Create a Bootable USB Flash Drive with [Ventoy](https://github.com/ventoy/Ventoy)**
6. **Copy the New ISO File to the Ventoy Flash Drive**
7. **Boot from the USB flash drive, choose your ISO & Install Windows**

For more info, check out the official [WIMUtil](https://github.com/memstechtips/WIMUtil) GitHub Repo.

---

### Old Methods
#### Method 1: Create a Bootable Windows Installation USB

- [Video Tutorial](https://youtu.be/pDEZDD_gEbo)

<details>
  <summary>Click to Show Instructions</summary>

  1. Download the `autounattend.xml` file and save it on your computer.
  2. Create a [Windows 10](https://www.microsoft.com/en-us/software-download/windows10) or [Windows 11](https://www.microsoft.com/en-us/software-download/windows11) Bootable Installation USB drive with [Rufus](https://rufus.ie/en/) or the Media Creation Tool.
  
     > **Important**  
     > - Some users have reported issues with the Media Creation Tool when creating the Windows Installation USB. Use it at your own discretion.  
     > - When using Rufus, don’t select any of the checkboxes in “Customize Your Windows Experience,” as it creates another `autounattend.xml` file that might overwrite settings in the UnattendedWinstall file.

  3. Copy the `autounattend.xml` file you downloaded in Step 1 to the root of the Bootable Windows Installation USB you created in Step 2.
  4. Boot from the Windows Installation USB, do a clean install of Windows as normal, and the scripts will run automatically.

</details>

#### Method 2: Create a Custom ISO File

- [Video Tutorial](https://youtu.be/pDEZDD_gEbo?si=ChEGghEOLCyLSnp7&t=1117)

<details>
  <summary>Click to Show Instructions</summary>

  1. Download the `autounattend.xml` file and save it on your computer.
  2. Download the [Windows 10](https://www.microsoft.com/en-us/software-download/windows10) or [Windows 11](https://www.microsoft.com/en-us/software-download/windows11) ISO file depending on the version you want.
  3. Download and install [AnyBurn](https://anyburn.com/download.php)
     - In AnyBurn, select the “Edit Image File” option.
     - Navigate to and select the Official Windows ISO file you downloaded in Step 2.
     - Click on “Add” and select the `autounattend.xml` file you downloaded in Step 1, or just click and drag the `autounattend.xml` into the AnyBurn window.
     - Click on “Next,” then on “Create Now.” You should be prompted to overwrite the ISO file; click on “Yes.”
     - Once the process is complete, close AnyBurn.
  4. Use the ISO file to install Windows on a Virtual Machine OR use a program like [Rufus](https://rufus.ie/en/) or [Ventoy](https://github.com/ventoy/Ventoy) to create a bootable USB flash drive with the edited Windows ISO file.

  > **Important**  
  >
  > - When using Rufus, don’t select any of the checkboxes in “Customize Your Windows Experience,” as it creates another `autounattend.xml` file that might overwrite settings in the UnattendedWinstall file.

  5. Boot from the Windows Installation USB, do a clean install of Windows as normal, and the scripts will run automatically.

</details>

#### Method 3: Use Ventoy Auto Install Plugin

- [Video Tutorial](https://youtu.be/4AGZQJTyCOs)

<details>
  <summary>Click to Show Instructions</summary>

  1. Download the `autounattend.xml` file and save it on your computer.
  2. Download the [Windows 10](https://www.microsoft.com/en-us/software-download/windows10) or [Windows 11](https://www.microsoft.com/en-us/software-download/windows11) ISO file, depending on the version you want.
  3. Download and install [Ventoy](https://github.com/ventoy/Ventoy) to your desired USB flash drive.
  4. Prepare the folder structure:
      - In your newly created Ventoy USB disk, create the following folders: `ISO` and `Templates`. <br/> *They should be at the root of the drive.*
      - Inside of the `ISO` folder, create a new folder called `Windows`.
      - Copy your Windows ISO files in the `ISO\Windows` folder.
      - Copy your `autounattend.xml` into the `Templates` folder.
  5. Start VentoyPlugson. Depending on your OS, the steps might differ.
      - On Windows, run the `VentoyPlugson.exe` file.
      - A new browser window should open up with a Ventoy web interface ready to go.
      - Select the `Auto Install Plugin` menu from the list.
      - Click on the `Add` button.
      - Select [parent] to make the whole Windows ISO folder benefit from the plugin.
      - In the Directory Path, paste in the absolute path to your `Windows` folder. </br> example: `F:\ISO\Windows` (Replace `F` with your drive letter.)
      - In the Template Path, paste in the absolute path to your `autounattend.xml` file. </br> example: `F:\Templates\autounattend.xml` (Replace `F` with your drive letter.) <br/> (PSA: If you have more `autounattend.xml` files, you can add them later on!)
      - Click on `OK` and you should see a message saying that the configuration has been saved successfully.
      - Close the VentoyPlugson browser window and stop the VentoyPlugson application.
  6. Boot from the Ventoy USB drive in the computer where you want to install windows.
     - After selecting a Windows ISO to boot from, you will be prompted to boot with the `/Templates/autounattend.xml` file.
     - Select that option and the `autounattend.xml` will be automatically executed during installation.

</details>

## FAQ

### How can I apply these settings to an existing Windows installation?

- Run the [`UWScript.ps1`](https://github.com/memstechtips/UnattendedWinstall/blob/main/UWScript.ps1) file or use the [Chris Titus Tech Windows Utility](https://github.com/ChrisTitusTech/winutil) ([Video](https://youtu.be/pldFPTnOCGM)).

### Can this answer file be used for an in-place upgrade?

- No, in-place upgrades do not support answer files.

### Why is Windows still updating automatically?

- Feature updates are delayed for a year; however, security and driver updates continue as usual.

### Why don't I have internet after installing Windows?

<details>
  <summary>Click to Show Instructions</summary>

  If you’re unable to connect to the internet after installation, it’s likely because your Wi-Fi or LAN (Ethernet) drivers are missing. Windows sometimes doesn’t include all necessary drivers for network adapters, especially if they’re specific to your device.

  To resolve this, follow these steps:

  1. **Download your network driver** from the manufacturer’s website on another computer with internet access. Look for Wi-Fi or LAN drivers specific to your device model.
  2. **Transfer the driver** to your Windows installation via USB drive.
  3. **Install the driver** on your Windows system and restart if necessary.

  After installation, you should be able to connect to the internet.

</details>

### How can I access the previous "IoT-LTSC-Like," "Standard," and "Core" versions of the file(s)?

  - You still have access to the previous files here: [Version 1.0.0 Release](https://github.com/memstechtips/UnattendedWinstall/releases/tag/v1.0.0).

  > [!NOTE]  
  > You need to download the `Source Code.zip` file. Once extracted, you’ll have access to all the previous v1.0.0 files.

### Why isn't Microsoft Edge Uninstalled?

<details>
  <summary>Click to Show Explanation</summary>

  I spent a lot of time trying to find a way to uninstall Microsoft Edge during Windows installation. However, it was challenging because of differences between Windows 10 22H2 and Windows 11 24H2. My goal is to use Microsoft’s supported uninstall methods, and I plan to add an easy Edge removal option in future releases.

  In the meantime, if you wish to remove Edge after Windows installation, consider using [this script by FR33THY](https://github.com/FR33THYFR33THY/Ultimate-Windows-Optimization-Guide/blob/main/6%20Windows/14%20Edge.ps1). FR33THY’s *Ultimate Windows Optimization Guide* was a major inspiration for version 2.0.0 of this project, and I highly recommend exploring it for additional Windows optimization tips.

</details>

### How can I add my own Registry Tweaks to v2.0.0 of the `autounattend.xml` file?

<details>
  <summary>Click to Show Instructions</summary>

  You can also still add your own registry entries to the v2.0.0 file, and it is actually easier if you understand where to add it. I'll give a brief explanation.

  For registry entries that apply to the local machine, i.e., `HKEY_LOCAL_MACHINE` registry keys, you can find the `function SetRecommendedHKLMRegistry` in the `autounattend.xml` file, see here: https://github.com/memstechtips/UnattendedWinstall/blob/93305192ed6d64e0f5b98a89f447927480285354/autounattend.xml#L1981

  and then add whatever registry entries you want to add in `.reg` format, like the rest of the entries are set, and just make sure you add it before the `"@` to make it part of the `.reg` file that will be generated, see here: https://github.com/memstechtips/UnattendedWinstall/blob/93305192ed6d64e0f5b98a89f447927480285354/autounattend.xml#L3412

  and it will then be applied to the registry.

  Similarly, if you have `HKEY_CURRENT_USER` registry keys, you can add those to the `User Customization.ps1` file in the same way as explained above, starting here:
  https://github.com/memstechtips/UnattendedWinstall/blob/93305192ed6d64e0f5b98a89f447927480285354/autounattend.xml#L3912
  so below the `Windows Registry Editor Version 5.00` and then ending before the `"@` here: https://github.com/memstechtips/UnattendedWinstall/blob/93305192ed6d64e0f5b98a89f447927480285354/autounattend.xml#L4423

  > **Note**  
  > The above links might not take you to the correct lines of code once new versions of the file are released, but it does take you to the correct lines on v2.0.0.

https://youtu.be/ZxxPxhr-5Kg
</details>


