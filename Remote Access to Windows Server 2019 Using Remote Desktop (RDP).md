# Remote Access to Windows Server 2019 Using Remote Desktop (RDP)

## 1. Overview

Remote Desktop Protocol (RDP) allows an authorised ICT administrator to access and manage the Windows Server 2019 remotely from another computer without physically visiting the server room.

The feature provides access to the server's graphical desktop environment, allowing the administrator to perform routine maintenance, troubleshoot issues, manage shared folders, configure user accounts and monitor server performance.

**Operating System:** Windows Server 2019  
**Remote Access Technology:** Remote Desktop Protocol (RDP)  
**Default Port:** TCP 3389  
**Client Application:** Windows Remote Desktop Connection (`mstsc.exe`)

## 2. Objectives

The implementation of remote server access aims to:

- Reduce unnecessary physical visits to the server room.
- Improve efficiency in performing ICT administration tasks.
- Enable remote troubleshooting and maintenance.
- Facilitate management of shared folders and user permissions.
- Support monitoring of server resources and services.
- Simplify routine server maintenance and administration.

## 3. Prerequisites

Before configuring remote access, ensure the following:

- The server is running Windows Server 2019.
- The administrator has authorised credentials.
- The server and client computer have network connectivity.
- The server has a known IP address or hostname.
- Remote Desktop is enabled on the server.
- Windows Firewall permits authorised Remote Desktop connections.
- The connecting account has permission to access the server remotely.

## 4. Configuration Procedure

### Step 1: Enable Remote Desktop

1. Log into Windows Server 2019.
2. Open **Server Manager**.
3. Select **Local Server** from the left-hand menu.
4. Locate the Remote Desktop setting.
5. Click the current status, usually displayed as Disabled.
6. Select **Allow remote connections to this computer**.
7. Ensure Network Level Authentication (NLA) is enabled.
8. Apply the changes.

### Step 2: Configure Remote Desktop Permissions

1. Open the Remote Desktop configuration settings.
2. Select **Select Users**.
3. Add the authorised administrator account if it is not already included.
4. Ensure the account belongs to the Remote Desktop Users group or has equivalent administrative privileges.

Note: Members of the local Administrators group generally already have Remote Desktop access. Apply the principle of least privilege when assigning access.

### Step 3: Identify the Server IP Address

On the server:

1. Press `Windows + R`.
2. Type `cmd`.
3. Press Enter.
4. Execute:

```cmd
ipconfig
```

5. Identify the IPv4 address under the active network adapter.

Example:

```text
IPv4 Address: 192.168.1.10
```

The above is an illustrative address. Record the actual server IP address.

For reliable connectivity, ensure the server uses a static IP address or a DHCP reservation.

### Step 4: Configure Windows Firewall

Confirm that the Remote Desktop firewall rules are enabled for the appropriate Domain or Private network profile.

To check through PowerShell:

```powershell
Get-NetFirewallRule -DisplayGroup "Remote Desktop" |
Select-Object DisplayName, Enabled, Profile
```

If authorised and required, enable the relevant rules:

```powershell
Enable-NetFirewallRule -DisplayGroup "Remote Desktop"
```

Avoid unnecessarily enabling access on public network profiles.

## 5. Connecting to the Server Remotely

Once the server has been configured, access it from an authorised office workstation.

1. Press `Windows + R`.
2. Type:

```cmd
mstsc
```

3. Press Enter to launch Remote Desktop Connection.
4. Enter the server's IP address or hostname.
5. Click Connect.
6. Enter the authorised server username and password.
7. Complete any required authentication.
8. Verify that the Windows Server desktop loads successfully.

At this stage, the administrator can interact with the server remotely.

## 6. Remote Administration Activities

Once connected, authorised ICT personnel can perform the following activities:

| Activity | Description |
|---|---|
| Shared Folder Management | Create, modify and organise shared folders. |
| User Administration | Manage authorised user accounts and access permissions. |
| Server Monitoring | Monitor CPU, memory, disk and network utilisation. |
| Backup Management | Monitor and verify backup operations. |
| Software Management | Install, update and troubleshoot applications. |
| Windows Updates | Review and install server updates. |
| Service Management | Monitor and restart Windows services where necessary. |
| Troubleshooting | Investigate server-related incidents remotely. |

## 7. Security Considerations

Remote access introduces additional security considerations. The following safeguards should be observed:

- Restrict RDP access to authorised ICT personnel.
- Use strong, unique passwords.
- Keep Network Level Authentication enabled.
- Do not expose TCP port 3389 directly to the public internet.
- Use the organisation's approved VPN when accessing the server from outside the office.
- Restrict firewall rules to trusted networks and devices.
- Maintain appropriate access permissions.
- Monitor successful and unsuccessful login attempts.
- Log out after completing administrative activities.
- Keep Windows Server security updates current.

## 8. Troubleshooting

| Problem | Possible Cause | Recommended Action |
|---|---|---|
| Remote Desktop connection fails | Server is unreachable | Verify network connectivity and server IP address. |
| Connection refused | RDP is disabled | Enable Remote Desktop on the server. |
| Credentials rejected | Incorrect credentials or insufficient permissions | Verify the account and Remote Desktop access rights. |
| Firewall blocks connection | Firewall rule disabled | Review Remote Desktop firewall rules. |
| Connection times out | Network routing or connectivity issue | Check LAN connectivity, VPN and network configuration. |
| Remote access unavailable after restart | Network or RDP service issue | Verify server network connectivity and Remote Desktop Services status. |

## 9. PowerShell Connectivity Checks

The following commands can help troubleshoot Remote Desktop connectivity.

**Check whether the server responds to network requests:**

```powershell
ping SERVER_IP_ADDRESS
```

**Check whether the RDP port is reachable:**

```powershell
Test-NetConnection SERVER_IP_ADDRESS -Port 3389
```

A successful test should return:

```text
TcpTestSucceeded : True
```

**Check Remote Desktop Services:**

```powershell
Get-Service TermService
```

The service should normally be running for incoming RDP connections.

## 10. Conclusion

Remote Desktop provides a practical way to administer Windows Server 2019 without physically accessing the server room.

Once configured correctly, it improves the efficiency of ICT operations by allowing authorised personnel to manage server resources, troubleshoot incidents and perform routine maintenance from their workstations.

**Documentation Status:** Remote access procedure documented.  
**Implementation Status:** Initial configuration and actual connectivity should be verified and recorded.

---

## 11. Implementation Record

Complete this section after the configuration has been implemented.

| Item | Details |
|---|---|
| Server Operating System | Windows Server 2019 |
| Server Hostname | To be recorded |
| Server IP Address | To be recorded |
| Remote Access Method | Remote Desktop (RDP) |
| RDP Port | TCP 3389 |
| Authorised ICT Account | To be recorded |
| Configuration Date | To be recorded |
| Connectivity Test | Pending verification |
| Administrator | ICT Department |

**Important:** Do not publish actual server IP addresses, usernames, passwords, public IPs or other sensitive infrastructure information in a public GitHub repository. Store operational details in an appropriately restricted location.
