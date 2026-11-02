# How to Mount and Access a VHDX Backup Image in Windows Server

## 1. Purpose
This procedure explains how to attach an existing `.VHDX` backup image in Windows Server, assign it a drive letter and access the backed-up files through File Explorer.

## 2. Environment
- Operating System: Windows Server 2019
- Backup Storage: External backup drive
- Backup Format: Virtual Hard Disk (VHDX)
- Tool Used: Windows Disk Management and DiskPart
- Objective: Access existing backup files without restoring the entire server.

## 3. Procedure

### Step 1: Locate the VHDX Backup File
1. Connect the external backup drive to the server.
2. Open File Explorer.
3. Navigate to the external backup drive.
4. Locate the `.VHDX` backup image.
5. Confirm that the backup file exists.

### Step 2: Open Disk Management
1. Press `Windows + X`.
2. Select Disk Management.
3. Alternatively, press `Windows + R`.
4. Type `diskmgmt.msc`.
5. Press Enter.

### Step 3: Check Whether the VHDX Is Already Attached
1. In Disk Management, click **Action**.
2. Select **Attach VHD**.
3. Click Browse and locate the VHDX file.
4. If Windows reports that the disk is already attached, do not attempt to attach it again.
5. Proceed to identify the existing virtual disk.

### Step 4: Open Command Prompt as Administrator
1. Press `Windows + R`.
2. Type `cmd`.
3. Press `Ctrl + Shift + Enter`.
4. Approve the administrator prompt.

### Step 5: Launch DiskPart
Enter:

```cmd
diskpart
```

Press Enter.

### Step 6: Identify the Attached Virtual Disk
Enter:

```cmd
list vdisk
```

This displays the virtual disks known to DiskPart.

Next, enter:

```cmd
list disk
```

Identify the virtual disk among the listed disks.

In this procedure, the attached VHDX was identified as **Disk 2**.

### Step 7: Select the Virtual Disk
Enter:

```cmd
select disk 2
```

Press Enter.

Expected result:

`Disk 2 is now the selected disk.`

### Step 8: Identify the Partitions
Enter:

```cmd
list partition
```

Press Enter.

This displays the partitions available on the selected virtual disk.

### Step 9: Identify the Corresponding Volume
Enter:

```cmd
list volume
```

Press Enter.

Identify the volume belonging to Disk 2 by checking its capacity, partition information and filesystem.

**Important:** Do not select a volume based on its number alone. Confirm that it belongs to the VHDX.

### Step 10: Select the Correct Volume
For example, if the corresponding volume is Volume 4, enter:

```cmd
select volume 4
```

Replace `4` with the actual volume number.

### Step 11: Assign a Drive Letter
Assign an available drive letter, for example V:

```cmd
assign letter=V
```

Expected result:

`DiskPart successfully assigned the drive letter or mount point.`

### Step 12: Access the Backup Files
1. Type:

```cmd
exit
```

2. Open File Explorer using `Windows + E`.
3. Select This PC.
4. Locate the newly assigned drive (V:).
5. Open the drive.
6. Browse the backed-up folders and files.
7. Identify and retrieve the required files.

## 4. Verification
Confirm the following:
- The VHDX is recognised by Windows.
- The virtual disk appears in Disk Management.
- The correct volume has a drive letter.
- The backed-up folders and files are accessible.
- Required files can be opened and checked.

## 5. Safety Precautions
- Do not format the virtual disk.
- Do not initialise the virtual disk.
- Do not use the `clean` command in DiskPart.
- Do not overwrite or delete existing backup files.
- Use read-only access wherever possible.
- Confirm the correct volume before assigning a drive letter.
- Do not modify the original backup image.

## 6. Detaching the Virtual Disk After Use
After completing the file retrieval:

1. Open Disk Management.
2. Locate the attached virtual disk.
3. Right-click the disk label (for example, Disk 2).
4. Select **Detach VHD**.
5. Confirm the action.

Do not select Delete the virtual hard disk file.

## 7. Final Outcome
The existing VHDX backup image was successfully recognised by Windows, identified as Disk 2, and made accessible by assigning an available drive letter to its corresponding volume.

This allowed access to the backed-up files through File Explorer without performing a full server restoration.
