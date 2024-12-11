# clean-windows11
auto script for windows 11

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
