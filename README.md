# THELAZYCAT - Persistent Auto-Injector v4.2

![THELAZYCAT Banner](https://img.shields.io/badge/THELAZYCAT-v4.2-blue)
![Platform](https://img.shields.io/badge/Platform-Linux%20%7C%20Termux-green)
![License](https://img.shields.io/badge/Educational-Purposes%20Only-red)

## 📖 Overview

**THELAZYCAT** is an advanced Android APK persistence injection tool designed for penetration testing and security research. This tool automates the process of embedding meterpreter reverse TCP payloads into legitimate Android applications while implementing sophisticated persistence mechanisms.

**Version**: 4.2  
**Author**: N3L  
**GitHub**: [https://github.com/n31nym0u2](https://github.com/n31nym0u2)

## ⚠️ DISCLAIMER

**EDUCATIONAL PURPOSES ONLY**

This tool is developed strictly for:
- Security research and education
- Penetration testing with proper authorization
- Academic cybersecurity studies
- Defensive security training

**LEGAL WARNING:**
- Only use on applications you own or have explicit permission to test
- Unauthorized use may violate local and international laws
- The developers are not responsible for misuse
- Users assume all legal responsibility for their actions

By using this tool, you acknowledge that you understand and accept full responsibility for its use.

## 🚀 Features

- **Automated Persistence**: Implements multiple persistence mechanisms
- **Advanced Payload Injection**: Embeds meterpreter reverse TCP payloads
- **Permission Management**: Customizable permission sets for stealth and functionality
- **Service Persistence**: Background services that survive app closure
- **Boot Persistence**: Auto-starts on device reboot
- **Activity Injection**: Injects payload into main application activities
- **Automated Signing**: Handles APK signing and alignment
- **Comprehensive Logging**: Detailed progress tracking and error reporting

## 📥 Installation & Setup

### Prerequisites

**Required Tools:**
- `apktool` - APK decompilation/compilation
- `metasploit-framework` - Payload generation
- `default-jdk` - Java development kit
- `zipalign` - APK optimization (optional but recommended)

### Installation Steps

1. **Clone the Repository**
   ```bash
   git clone https://github.com/n31nym0u2/thelazycat.git
   cd thelazycat
   ```
2. **Set Execution Permissions**
   ```bash
   chmod +x thelazycat
   ```
3. **Install Dependencies (Kali Linux/Ubuntu)**
   ```bash
   sudo apt update
   sudo apt install apktool metasploit-framework default-jdk zipalign -y
   ```
4. **Verification**
   ```bash
   sudo ./thelazycat
   ```

## 🔧 APKTool Install Manually ( Kali Linux/Ubuntu)
  ```bash
  # Install Dependencies
  sudo apt update
  sudo apt install default-jre curl wget

  # Download the wrapper script
  sudo curl -L -o /usr/local/bin/apktool https://raw.githubusercontent.com/iBotPeaches/Apktool/master/scripts/linux/apktool

  # Download the latest APKTool jar file
  sudo curl -L -o /usr/local/bin/apktool.jar https://bitbucket.org/iBotPeaches/apktool/downloads/apktool_2.9.3.jar

  # Make both executable
  sudo chmod +x /usr/local/bin/apktool
  sudo chmod +x /usr/local/bin/apktool.jar

  ```

### Payload Integration

The tool leverages $\text{Smali}$ code integration and $\text{Manifest}$ modification to seamlessly embed the payload:

  * **Payload Type:** Meterpreter reverse TCP payload.
  * **Injection Method:** $\text{Smali}$ code integration into the target application's execution flow (typically the main activity).
  * **Modifications:** Automated $\text{Manifest}$ modification for required permissions and component registration (services, receivers).
  * **Resource Management:** Automated resource merging and conflict resolution.

### Persistence Mechanisms

To ensure reliable, long-term access:

  * **Service Persistence:** Injects a background service that automatically attempts to restart if terminated.
  * **Boot Receiver:** Registers a receiver component to auto-start the payload on the device's reboot.
  * **Activity Injection:** Executes the primary payload within the main application activity's lifecycle.
  * **Foreground Service (Optional):** Can be configured to maintain background execution with higher system priority.

### Permission Sets

The tool offers flexibility in defining the payload's capabilities:

| Permission Set | Description | Key Permissions Included |
| :--- | :--- | :--- |
| **Default** | Basic permissions required for network connection and persistence. | `android.permission.INTERNET`, `android.permission.RECEIVE_BOOT_COMPLETED` |
| **Custom** | Allows the user to select additional, specific permissions as needed. | User-selected (e.g., `READ_CONTACTS`, `ACCESS_FINE_LOCATION`) |
| **Full Control** | Comprehensive set for maximum access, intended for deeply authorized testing. | Includes all common invasive permissions. |

-----

## 📱 Application Structure Compatibility

$\text{APKPwn}$ is most effective against standard applications but has limitations against modern protection techniques.

### ✅ WORKING Application Types

These types generally have standard Android build structures that the injector can successfully modify:

  * **Standard Android Applications:** Single/Multiple Activity Apps, traditional **Java**-based, **Kotlin** applications (converted to $\text{Smali}$), Simple utility apps.
  * **Game Applications:** **Unity**-based, **Cocos2d-x**, **Cocos2d-JS**, and simple 2D game engines.
  * **Utility & Productivity Apps:** File managers, System tools, Media players, Camera/Gallery, Note-taking apps.
  * **Educational & Social Apps:** E-book readers, Simple messaging/Social media clients, Weather/Reference applications.

### ⚠️ PARTIALLY WORKING Application Types

Success is dependent on the specific build configuration and often requires manual post-modification steps:

  * **Hybrid & Complex Applications:** $\text{Cordova/PhoneGap}$ (often requires manual configuration), $\text{React Native}$ (success varies), Multi-module and enterprise applications, Apps with basic JNI/native components.

### ❌ NOT WORKING Application Types

These applications employ techniques that actively prevent or severely complicate $\text{Smali}$-level modification:

  * **Protected & Obfuscated Apps:** Heavily **ProGuard** optimized, **DexGuard** protected, Apps with string encryption, control flow obfuscation, anti-tampering, or root detection.
  * **Advanced Framework Apps:** **Flutter** applications (Dart-compiled, not $\text{Smali}$), $\text{Xamarin}$ apps (.NET compiled), Native-only activities and applications, Unity **IL2CPP** builds.
  * **Security & System Apps:** $\text{VPN}$ and security-focused applications, Banking/financial apps with advanced protection, Pre-installed system applications, Device administrator/policy controllers.

| Application Type | Success Rate | Notes |
| :--- | :--- | :--- |
| Simple Utility Apps | 95% | High compatibility. |
| Unity Games | 85% | Good success rate. |
| Social Media Apps | 75% | Medium success, common anti-tampering is manageable. |
| Banking Apps | 40% | Low due to advanced protection mechanisms. |
| System Apps | 20% | Very low success due to high privileges and system integrity checks. |
| Obfuscated Apps | 15% | Rarely works unless obfuscation is basic. |

-----

## 🐛 Troubleshooting

### Common Issues

| Issue | Potential Solution(s) |
| :--- | :--- |
| **Build Errors** | Ensure sufficient disk space; Check for resource conflicts; Verify all script dependencies are correctly installed. |
| **Signing Issues** | Verify **Java** installation and environment variables; Check keystore file permissions; Ensure adequate certificate validity period. |
| **Persistence Not Working** | Test on different Android OS versions; Check the target device's battery optimization settings; Verify that the required permissions were explicitly granted by the user post-installation. |

### Debug Mode

For detailed logging and to diagnose complex issues, modify the script to allow for verbose output:

```bash
# Remove "> /dev/null 2>&1" from commands for verbose output
```

-----

## 🔒 Security & Ethical Usage

**This tool is strictly for educational, defensive, and authorized testing purposes.**

### Security Considerations

  * **Isolation:** Always use in isolated, controlled testing environments.
  * **Authorization:** Obtain explicit, proper written authorization *before* testing on any system or device.
  * **Devices:** Use dedicated testing devices that do not contain sensitive personal or corporate data.
  * **Responsible Disclosure:** Follow ethical and responsible disclosure practices for any vulnerabilities discovered.
  * **Maintenance:** Keep the tool updated to ensure the use of the latest, most secure components.

### 📝 Legal & Ethical Usage

| Permitted Uses | Prohibited Uses |
| :--- | :--- |
| Authorized penetration testing | Unauthorized access to systems |
| Security research with permission | Malicious software distribution |
| Educational cybersecurity training | Privacy violation activities |
| Defensive security preparation | Any illegal cybersecurity activities |

**License:** This tool is provided for **educational purposes only**. Users assume all responsibility for legal and ethical use.

-----

## 🤝 Contributing

Contributions are greatly appreciated and welcome\! Please consider helping with:

  * Bug fixes and general improvements.
  * Compatibility enhancements for newer Android versions or frameworks.
  * Documentation updates and clarifications.
  * **Security Vulnerability Reports** (Please follow responsible disclosure practices).
