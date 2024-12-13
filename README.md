# Unattended Windows Installation

This project leverages Microsoft's [Answer Files](https://learn.microsoft.com/en-us/windows-hardware/manufacture/desktop/update-windows-settings-and-scripts-create-your-own-answer-file-sxs?view=windows-11) (or Unattend files) to automate and customize Windows installations. It allows for modifications to Windows settings and package installations directly from the Windows ISO during setup.

## Why Use an Answer File?

### Security
- **Transparency**: All modifications are documented within the answer file, allowing for review.
- **Official Sources**: Utilizes official Microsoft ISOs, reducing reliance on untrusted sources.
- **Microsoft Support**: Leverages a feature designed for secure, mass deployment of Windows.

### Automation
- **Efficient Configuration**: Automates settings across multiple devices, significantly reducing manual setup time.

### Supported Windows Versions
- **Windows 10 or Windows 11**  
  - *Tested on Windows 10 22H2 & Windows 11 24H2*
  - *Supports 32-bit, 64-bit, and ARM64 architectures*

## What Does The XML File Do?

The XML file, `autounattend.xml`, includes:
- Detailed descriptions of configurations and registry tweaks, available for review on GitHub.
- Customization options. To edit, download the file and use editors like [Cursor](https://www.cursor.com/) or [VSCode](https://code.visualstudio.com/).

### Sources and Contributions

<details>
  <summary>Click to Expand</summary>

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

- **Edition Selection**: No longer enforced to use Pro edition as in v2.0.0.
- **Bypasses System Requirements** for Windows 11.
- **Security Adjustments**: 
  - Disables Windows Defender services by default (with an option to enable post-installation).
  - Disables User Account Control by default (with an option to enable post-installation).
- **Script Execution**: Allows running PowerShell scripts by default.
- **Account Setup**: Skips forced Microsoft account creation during setup.
- **Bloatware Removal**: Removes most preinstalled apps except Microsoft Edge, Notepad, and Calculator; disables Copilot and Recall.
- **Privacy & Telemetry**: Configures registry to disable telemetry.
- **Update Management**: Limits Windows Update to security patches for one year.
- **Performance Tuning**: 
  - Optimizes registry settings, scheduled tasks, and services for performance.
  - Enables Ultimate Performance power plan.

> [!NOTE]  
> Use `UWScript.ps1` after installation to adjust or revert settings if Windows Update or other processes alter them. This script can also apply similar customizations to an existing Windows installation without reinstallation.

> **Before Running the Script**  
> Run PowerShell as an administrator and set the execution policy:
> ```powershell
> Set-ExecutionPolicy Unrestricted
> ```

## Usage Instructions

To utilize the answer file:

- Place `autounattend.xml` at the root of your Windows Installation Media.

> [!IMPORTANT]  
> Ensure the file is named `autounattend.xml` for recognition by the Windows setup.

### Method 1: Create a Bootable Windows Installation USB

<details>
  <summary>Click to Expand Instructions</summary>

  1. **Download** `autounattend.xml`.
  2. **Create Bootable USB**: Use [Rufus](https://rufus.ie/en/) or Microsoft's Media Creation Tool to make a Windows Installation USB.
     
     > **Important**  
     > - Media Creation Tool might cause issues; use at discretion.
     > - Avoid selecting "Customize Your Windows Experience" in Rufus to prevent overwriting the answer file.

  3. **Copy** `autounattend.xml` to the root of the USB.
  4. **Boot and Install**: Boot from the USB for installation; the answer file will execute automatically.

</details>

### Method 2: Create a Custom ISO File

<details>
  <summary>Click to Expand Instructions</summary>

  1. **Download** `autounattend.xml`.
  2. **Get Windows ISO**: Download from [Windows 10](https://www.microsoft.com/en-us/software-download/windows10) or [Windows 11](https://www.microsoft.com/en-us/software-download/windows11).
  3. **Use AnyBurn**: 
     - Choose "Edit Image File", select your ISO, add `autounattend.xml`, and recreate the ISO.
  4. **Create Bootable Media**: Use the new ISO with Rufus or Ventoy to make a bootable drive.

  > **Important**  
  > - Similar to Method 1, avoid customizing experience in Rufus.

  5. **Install Windows**: Boot from the modified ISO or USB for automatic setup.

</details>

### Method 3: Use Ventoy Auto Install Plugin

<details>
  <summary>Click to Expand Instructions</summary>

  1. **Download** `autounattend.xml`.
  2. **Prepare Ventoy**: Install Ventoy on a USB, create necessary folders (`ISO`, `Templates`).
  3. **Add Files**: Place Windows ISOs in `ISO\Windows`, `autounattend.xml` in `Templates`.
  4. **Configure Ventoy Plugin**: Use VentoyPlugson to set up auto-installation with the answer file.
  5. **Install**: Boot from the Ventoy USB and select the ISO with the answer file option for automatic setup.

</details>

## FAQ

### Can this answer file be used for an in-place upgrade?

- No, answer files are not supported for in-place upgrades.

### Why is Windows still updating automatically?

- Feature updates are delayed for one year, but security updates continue as usual.

### Why don't I have internet after installing Windows?

<details>
  <summary>Click to Expand Instructions</summary>

  If there's no internet connection post-installation:
  
  - **Driver Issue**: Download network drivers from your hardware manufacturer on another machine, transfer via USB, and install them on your new Windows setup.

</details>
