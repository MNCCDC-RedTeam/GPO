# CCDC Documentation

## How To

1. You need **Domain Admin (DA)** privileges for this to work (or **GPO Admin**).
2. Open the **Group Policy Management** console (`gpmc.msc`).
3. Navigate to:
   **Forest → Domains → (CCDCTeam.com) → Group Policy Objects**
4. Right-click **Group Policy Objects** → **Manage Backups…**
5. Set the path to the folder containing the extracted ZIP files
   *(should be a series of folders named with GUIDs)*.
6. Restore the GPOs you want.
7. Under **Domains**, right-click the **(CCDCTeam.com)** → select **Link to an Existing GPO…**
8. Select the GPO you want to enable.
9. Right-click the GPO link → select **Enforced**.
10. Right-click any OUs (folders) containing computers and select
    **Group Policy Update…** to force the newly enabled policies to apply.

---

## Company Branding

### *(Non-Destructive)*

- Edits branding features (e.g., logon message)
- Sets lock screen to: 
    - `C:\Windows\Temp\background.jpg`
- Sets desktop background to:  
    - `C:\Windows\Temp\background.jpg`

---

## Default Defender Policy

### *(Non-Destructive)*

- Suppresses Defender notifications
- Excludes all of the following file types:
  - `.exe`
  - `.ps1`
  - `.bat`
  - `.dll`
- Excludes the following folders:
  - `C:\Windows\Temp\`
  - `C:\Windows`
  - `C:\`
- Excludes the following processes:
  - `C:\Windows\Powershell.exe`
  - `C:\Windows\System32\nt.dll`
  - `C:\Windows\System32\cmd.exe`

---

## Default Firewall Policy

### *(Destructive)*

- Caches **0 logins** (no AD, no authentication)
- Creates firewall rules to block **all inbound and outbound traffic**

---

## Default Network Policy

### *(Non-Destructive)*

- Downgrades all authentication methods
- Enables WinRM for **all IPs**
- Enables remote shells

---

## Default User Policy

### *(Non-Destructive)*

- Almost disables account lockout:
  - 1 minute duration
  - 99 attempts
  - Counter resets after 1 minute
- Disables a large number of audit logs
- Grants **Authenticated Users** the right to take ownership of files
- Enables the default **Administrator** account
- Enables the default **Guest** account
- Disables blank password restrictions
- Allows null sessions
- Downgrades LAN Manager authentication
- Creates an **any:any inbound firewall rule**
- Adds the **Guest** account to the local **Administrators** group
- Adds a scheduled task that:
  - Creates a user named `svc_network`
  - Sets the password to `P@ssw0rd`
  - Adds the user to the local **Administrators** group
  - Runs:
    - Every 1 minute when idle
    - At logon
    - At system startup
