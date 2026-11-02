# ESET Endpoint Antivirus Installation and Central Deployment

## ICT Department

**Project:** ESET Endpoint Antivirus Deployment  
**Management Platform:** ESET PROTECT  
**Licence:** ESET PROTECT Entry  
**Deployment Target:** Windows Desktop and Laptop Computers  
**Licence Capacity:** 50 devices  
**Licence Expiry:** 14 March 2029  
**Status:** Deployment documentation and implementation guide

---

## 1. Project Overview

This document outlines the process of installing and centrally managing ESET Endpoint Antivirus across Wamae & Allen LLP office computers using the ESET PROTECT platform.

The objective is to ensure that company computers are protected against malware, viruses, ransomware and other security threats while allowing the ICT Department to monitor and manage endpoint protection from a central console.

The deployment covers:

- ESET PROTECT account and console setup.
- Licence registration and verification.
- Downloading the ESET installation package.
- Installing ESET through Windows Command Prompt (CMD).
- Deploying the ESET Management Agent.
- Centrally installing and activating ESET Endpoint Antivirus.
- Monitoring endpoint protection.
- Verifying successful installations.
- Troubleshooting common installation problems.

## 2. Licence Information

The firm has an ESET PROTECT Entry subscription.

| Item | Details |
|---|---|
| Organisation | Wamae & Allen LLP |
| Customer ID | wam00016 |
| Order Number | 758275 |
| Subscription | ESET PROTECT Entry |
| ESET PROTECT | 50 devices |
| Endpoint & Server Security | 50 devices |
| Expiry Date | 14 March 2029 |

**Security note:** The activation key and other sensitive licence credentials must not be included in this repository. Store them securely and restrict access to authorised ICT personnel.

## 3. Understanding the ESET Deployment Components

Three main components are involved in the deployment.

### 3.1 ESET Endpoint Antivirus

This is the endpoint security application installed on individual Windows computers. It provides antivirus and malware protection.

### 3.2 ESET Management Agent

The agent is installed on each managed computer and establishes communication between that computer and the ESET PROTECT console.

It allows the ICT administrator to:

- Monitor endpoint protection.
- Deploy software installation tasks.
- Apply security policies.
- Monitor device status.
- Manage updates and security settings.

### 3.3 ESET PROTECT Console

The central management platform used by the ICT Department to manage all enrolled computers from one interface.

Official portal: https://protecthub.eset.com/

---

## 4. Pre-Installation Requirements

Before starting the deployment, confirm the following:

1. The computer is running a supported Windows operating system.
2. The computer has a working internet connection.
3. Administrator access is available.
4. The computer has sufficient free disk space.
5. Existing third-party antivirus software has been checked and incompatible products removed where necessary.
6. The ESET PROTECT subscription is valid.
7. The computer has been assigned an appropriate hostname.
8. The computer is connected to the company network or has internet access for cloud deployment.

For centrally managed installation, the ESET Management Agent must be installed and successfully communicating with the console.

## 5. Accessing ESET PROTECT

1. Open a web browser.
2. Navigate to https://protecthub.eset.com/.
3. Sign in using the firm's authorised ESET account.
4. Open the ESET PROTECT management console.
5. Confirm that the organisation's subscription is available.
6. Verify the number of available device seats.

If the firm has not yet configured the console, complete the account and console registration process first.

## 6. Registering and Verifying the Licence

1. Open the subscription or licence management section.
2. Add or connect the firm's ESET subscription.
3. Enter the activation key when requested.
4. Confirm that the subscription is recognised.
5. Verify the subscription expiry date and available seats.

The licence should be assigned to the endpoint security products during installation or through the appropriate activation task.

**Important:** Do not confuse the activation key with the ESET Management Agent. The key activates the security product; the agent connects the computer to the management console.

---

## 7. Installing ESET Through CMD

This section covers local installation using Windows Command Prompt.

### 7.1 Download the ESET MSI Installer

1. Visit the official ESET Endpoint Antivirus download and installation documentation:

   https://help.eset.com/eea/13/en-US/installation.html

2. Download the appropriate Windows MSI installer.
3. Select the correct architecture, normally 64-bit for modern office computers.
4. Create a folder on the computer:

```cmd
mkdir C:\ESET
```

5. Save or copy the downloaded MSI installer into this folder.

Example installer filename:

```text
ees_nt64.msi
```

The actual filename may differ depending on the downloaded version and language.

### 7.2 Open Command Prompt as Administrator

1. Click Start.
2. Search for CMD.
3. Right-click Command Prompt.
4. Select Run as administrator.

### 7.3 Confirm the Installer Exists

Run:

```cmd
dir C:\ESET\*.msi
```

Confirm that the downloaded installer appears in the results.

### 7.4 Execute the Silent Installation

Run the following command, replacing the filename with the actual installer filename:

```cmd
msiexec.exe /i "C:\ESET\ees_nt64.msi" /qn /norestart /L*v "C:\ESET\install.log"
```

**Explanation of the command:**

| Parameter | Function |
|---|---|
| msiexec.exe | Windows Installer service |
| /i | Installs the MSI package |
| /qn | Performs installation without a graphical interface |
| /norestart | Prevents automatic computer restart |
| /L*v | Creates a detailed installation log |
| install.log | Records installation activities and errors |

The installation runs silently in the background.

### 7.5 Check the Installation Result

Check the installation log:

```cmd
notepad C:\ESET\install.log
```

Check whether the default installation directory exists:

```cmd
if exist "C:\Program Files\ESET\ESET Endpoint Antivirus" (echo ESET installation folder found) else (echo Check installation)
```

The installation directory may differ depending on the product version and configuration.

**Important:** A successful MSI installation does not automatically establish central management. The ESET Management Agent and product activation must also be addressed.

---

## 8. Central Deployment Through ESET PROTECT

For the firm's 50-device subscription, central deployment is the preferred approach for managing multiple office computers.

### 8.1 Generate an ESET PROTECT Live Installer

1. Sign in to the ESET PROTECT cloud console.
2. Navigate to the installer deployment section.
3. Select the Windows installation option.
4. Choose the appropriate ESET endpoint security product.
5. Include the ESET Management Agent.
6. Configure the installation settings.
7. Select the firm's subscription where the installer creation process provides that option.
8. Generate the installer package.
9. Download the generated executable.

The generated package should contain the ESET Management Agent and the selected endpoint security application.

### 8.2 Copy the Installer to the Target Computer

Create a folder:

```cmd
mkdir C:\ESET
```

Copy the generated installer into this folder.

For example:

```text
C:\ESET\ESET_Office_Installer.exe
```

Use the actual downloaded filename.

### 8.3 Run the Central Deployment Installer Through CMD

Open CMD as Administrator.

Execute:

```cmd
cd /d C:\ESET
```

Then run:

```cmd
ESET_Office_Installer.exe --silent --acceptterms
```

Replace the filename with the actual generated installer filename.

The parameters mean:

- `--silent` – runs the installer without user interaction.
- `--acceptterms` – accepts the applicable legal documents.

The installer requires internet access to retrieve the necessary ESET components.

**Important:** ESET PROTECT Live Installer requires the appropriate administrator account. ESET documentation specifies the built-in local Administrator account or a domain administrator account where applicable. Test the installation using an authorised administrative account before wider deployment.

Official instructions:

https://help.eset.com/epi/4/en-US/cloud_win.html

### 8.4 Confirm Agent Communication

After installation:

1. Open the ESET PROTECT console.
2. Navigate to Computers.
3. Locate the newly installed computer.
4. Confirm that it appears in the device list.
5. Check its last connected time.
6. Confirm that the management agent is communicating successfully.

---

## 9. Activating ESET Endpoint Antivirus

If activation was not included in the installer configuration:

1. Open the ESET PROTECT console.
2. Navigate to the relevant computer.
3. Check its product activation status.
4. Use the appropriate activation or subscription assignment option.
5. Assign the firm's valid subscription.
6. Confirm that activation succeeds.

Alternatively, the MSI installer supports activation through an activation property:

```cmd
msiexec.exe /i "C:\ESET\ees_nt64.msi" /qn ACTIVATION_DATA=key:YOUR-ACTIVATION-KEY
```

Replace the placeholder with the actual activation key only when using an approved secure deployment process.

**Security recommendation:** Prefer assigning the subscription through ESET PROTECT rather than embedding the actual key in scripts, command history or GitHub files.

---

## 10. Verifying Successful Deployment

After installation, perform the following checks.

### 10.1 On the Windows Computer

1. Open the Start menu.
2. Search for ESET Endpoint Antivirus.
3. Open the application.
4. Confirm that the protection status is healthy.
5. Open the Update section.
6. Check for available module updates.
7. Run an initial computer scan.

### 10.2 On ESET PROTECT

Check that:

- The computer appears in the Computers section.
- The ESET Management Agent is connected.
- The correct endpoint product is installed.
- The subscription is activated.
- Detection modules are up to date.
- No critical security alerts are displayed.

### 10.3 Agent Status Log

The following file can help establish whether the management agent is operating correctly:

```text
C:\ProgramData\ESET\RemoteAdministrator\Agent\EraAgentApplicationData\Logs\status.html
```

The ProgramData folder is hidden by default.

---

## 11. Troubleshooting

| Problem | Possible Cause | Recommended Action |
|---|---|---|
| Installer does not run | Incorrect path or filename | Confirm the installer location |
| Access denied | Insufficient privileges | Run CMD using the appropriate administrator account |
| Installation fails | Existing incompatible antivirus | Check and remove incompatible security software |
| MSI installation error | Windows Installer issue | Review the installation log |
| Computer does not appear in console | Agent not installed or connected | Check agent installation and internet connectivity |
| Product not activated | Licence not assigned | Assign the subscription through ESET PROTECT |
| Modules not updating | Internet or update connectivity issue | Check network access and update settings |
| Installation requires restart | Pending system changes | Schedule and perform a controlled restart |

### MSI Installation Log

Use:

```cmd
notepad C:\ESET\install.log
```

Check the log for the error code and the cause of the failure.

---

## 12. Deployment Checklist

Use this checklist when onboarding each computer.

- [ ] Confirm computer hostname.
- [ ] Confirm Windows operating system and architecture.
- [ ] Check administrator access.
- [ ] Check for existing antivirus products.
- [ ] Confirm internet connectivity.
- [ ] Confirm ESET subscription availability.
- [ ] Generate or obtain the approved ESET installer.
- [ ] Install ESET Management Agent.
- [ ] Install ESET Endpoint Antivirus.
- [ ] Assign and activate the subscription.
- [ ] Confirm computer appears in ESET PROTECT.
- [ ] Confirm agent communication.
- [ ] Update detection modules.
- [ ] Run an initial scan.
- [ ] Confirm protection status.
- [ ] Record deployment completion in the ICT asset or deployment register.

---

## 13. Security and Maintenance Recommendations

1. Restrict access to the ESET PROTECT console to authorised ICT administrators.
2. Never store activation keys, passwords or private certificates in GitHub.
3. Keep endpoint products and detection modules updated.
4. Monitor disconnected devices and devices reporting security alerts.
5. Apply consistent security policies across company computers.
6. Review subscription usage periodically.
7. Test deployment on a small group of computers before rolling it out to all 50 devices.
8. Maintain a record of installation dates, device names and deployment status.
9. Schedule periodic endpoint protection reviews.

---

## 14. Official ESET Documentation

The following references provide additional technical guidance:

| Resource | Link |
|---|---|
| ESET Endpoint Antivirus Installation | https://help.eset.com/eea/13/en-US/installation.html |
| ESET Command-Line Installation | https://help.eset.com/eea/13/en-US/installation_command_line.html |
| ESET PROTECT Live Installer | https://help.eset.com/epi/4/en-US/cloud_win.html |
| ESET PROTECT Software Installation Task | https://help.eset.com/protect_cloud/en-US/client_tasks_software_install.html |
| ESET PROTECT Hub | https://protecthub.eset.com/ |

---

## 15. Implementation Status

This document provides the approved technical procedure for implementing ESET endpoint protection.

Actual deployment should be recorded as computers are installed and verified.

| Activity | Status |
|---|---|
| ESET subscription acquired | Confirmed from licence details |
| Licence validity | Valid until 14 March 2029 |
| ESET PROTECT console access | To be verified |
| Licence registration in console | To be verified |
| Installer generation | Pending verification |
| Pilot computer deployment | Pending |
| Central agent communication | Pending verification |
| Endpoint activation | Pending verification |
| Office-wide rollout | Pending |
| Final deployment verification | Pending |

**Prepared by:** ICT Department  
**Organisation:** Wamae & Allen LLP  
**Document purpose:** Internal technical documentation and deployment reference.
