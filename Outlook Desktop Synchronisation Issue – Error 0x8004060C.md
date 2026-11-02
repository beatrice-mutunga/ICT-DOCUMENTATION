# Outlook Desktop Synchronisation Issue – Error 0x8004060C

## 1. Incident Overview

**Incident:** Outlook Desktop 2 failing to synchronise emails.

**Application:** Microsoft Outlook – Classic Outlook

**Email Platform:** Microsoft 365 – Exchange Online

**Affected Device:** Desktop 2

**Unaffected Device:** Desktop 1

**Error Code:** `0x8004060C`

**Error Message:**

> The message store has reached its maximum size. To reduce the amount of data in this message store, select some items that you no longer need and permanently delete them.

**Status:** Under investigation – resolution pending.

---

## 2. Background

The organisation uses Microsoft 365 Exchange Online for email services.

The same email accounts are configured on two different computers:

- Desktop 1 – Outlook Classic.
- Desktop 2 – Outlook Classic.

Although both computers access the same Microsoft 365 email accounts, each Outlook installation maintains its own local data file.

These files are known as Offline Storage Table (OST) files.

The OST file stores a locally cached copy of mailbox information, allowing Outlook to display emails more quickly and provide offline access.

The two computers therefore maintain separate local copies of the same online mailbox.

---

## 3. Problem Identified

Outlook on Desktop 2 was not synchronising emails consistently with Desktop 1.

When attempting to synchronise using:

**Send/Receive → Send/Receive All Folders**

Outlook returned error `0x8004060C`.

The error indicated that the Outlook message store had reached its maximum permitted size.

### Initial investigation findings

| Item | Finding |
|---|---|
| Email accounts | Same accounts configured on both computers |
| Outlook version | Classic Outlook |
| Affected computer | Desktop 2 |
| Data files identified | One OST file |
| OST file size | 47.5 GB |
| Initial offline synchronisation setting | 1 year |
| Reported error | 0x8004060C |
| Other computer | Desktop 1 unaffected |

---

## 4. Technical Explanation

### 4.1 What is an OST file?

OST stands for Offline Storage Table.

It is a local Outlook data file that stores a synchronised copy of mailbox information from Microsoft Exchange Online.

In simple terms:

- Microsoft 365 holds the central online mailbox.
- Desktop 1 downloads and maintains its own local copy.
- Desktop 2 downloads and maintains another local copy.

The OST files are independent of each other.

This explains why Desktop 1 can continue working even when Desktop 2 experiences a synchronisation problem.

### 4.2 Why did the error occur?

The OST file on Desktop 2 was found to be 47.5 GB.

Modern Outlook installations generally have a default OST/PST maximum size of 50 GB.

The identified file was therefore operating close to its configured maximum.

When Outlook attempted to process additional mailbox data, it returned error `0x8004060C`.

The large OST file is a strong indication of a local message-store capacity problem. Further checks are required to establish whether there are additional mailbox or synchronisation issues.

### 4.3 Why was Desktop 1 unaffected?

Each computer maintains its own OST file.

The file on Desktop 1 has its own size and storage allocation, independent of the 47.5 GB file on Desktop 2.

Consequently, an issue affecting Desktop 2's local Outlook data file does not automatically affect Desktop 1.

---

## 5. Troubleshooting Performed

### Step 1: Identified the Outlook synchronisation error

Opened Outlook on Desktop 2.

Navigated to:

**Send/Receive → Send/Receive All Folders**

Observed error:

`0x8004060C – The message store has reached its maximum size.`

### Step 2: Inspected Outlook data files

Navigated to:

**File → Account Settings → Account Settings → Data Files**

Findings:

- Only one data file was listed.
- The file was an OST file.
- No PST archive file was identified in the Data Files list.

### Step 3: Checked the OST file size

Opened the OST file location through the Data Files tab.

Inspected the file properties.

**Recorded file size: 47.5 GB.**

### Step 4: Checked Cached Exchange Mode settings

Navigated to:

**File → Account Settings → Account Settings → Change**

Found that:

**Mail to keep offline: 1 year**

This setting determines how much mailbox data Outlook keeps locally available for offline access.

### Step 5: Reduced the offline synchronisation period

Changed the setting from:

- Previous setting: 1 year.
- New setting: 3 months.

The intention was to reduce the amount of mailbox data maintained locally on Desktop 2.

However, this change did not resolve the synchronisation error.

**Technical observation:** Reducing the cache period does not guarantee that an existing OST file will immediately shrink in physical size.

---

## 6. Proposed Solution – Relocating/Rebuilding the OST File

The next proposed intervention is to configure Outlook to use a new local data-file location.

The intended destination is a separate drive, such as D:, rather than the default Windows user profile location.

Example destination:

`D:\Outlook Data\`

### Important technical consideration

Moving an existing OST file manually does not automatically configure Outlook to use the new location.

The location must be configured using a supported Outlook profile/data-file method.

The proposed approach is to:

1. Verify that the online Microsoft 365 mailbox contains all important emails.
2. Check for unsent messages and unsynchronised local changes.
3. Confirm the destination drive has sufficient free space.
4. Close Outlook completely.
5. Preserve the original OST file as a precaution.
6. Configure the new OST location using an appropriate supported method.
7. Reopen Outlook.
8. Allow Outlook to create or initialise the local cache.
9. Allow mailbox synchronisation to complete.
10. Verify that emails and folders are accessible.

### Why rebuild instead of simply moving?

The current OST file is already 47.5 GB.

Simply moving it to another drive would change its storage location but would not resolve the message-store size limit.

Rebuilding the local cache provides an opportunity to create a fresh OST file and address the existing local data-store problem.

---

## 7. Proposed Storage Structure

If a separate internal drive is available, the following folder arrangement can be used:

```text
D:\
   Outlook Data\
      [New Outlook OST file]
```

The destination drive should have adequate free space for the OST file and future growth.

A separate internal drive is preferable to a removable external drive for an actively used Outlook OST file.

---

## 8. Safety Precautions

Before implementing the proposed solution:

- Confirm that all important emails are accessible through Outlook Web.
- Verify Inbox, Sent Items, Archive and custom folders.
- Check the Outbox for unsent emails.
- Confirm that there are no unsynchronised changes.
- Preserve the original OST file until the new Outlook configuration is verified.
- Do not permanently delete the original OST prematurely.
- Do not interfere with Desktop 1.
- Do not assume that locally stored PST archives are included in the online mailbox.

**Important:** An OST file is normally a synchronised cache, but it may contain changes that have not yet reached Exchange Online. Such changes must be protected before rebuilding.

---

## 9. Expected Outcome

Following successful implementation:

1. Outlook on Desktop 2 should initialise a fresh local data file.
2. The mailbox should synchronise with Microsoft 365 Exchange Online.
3. Recent emails should download according to the configured offline period.
4. Older emails should remain accessible online, provided they are stored in the mailbox.
5. The synchronisation error should no longer occur if the local message-store capacity issue was the cause.
6. Desktop 1 should remain unaffected.

---

## 10. Outstanding Tasks

- [ ] Verify all historical emails through Outlook Web.
- [ ] Verify Sent Items and custom folders.
- [ ] Check for unsent emails and unsynchronised changes.
- [ ] Identify the destination drive on Desktop 2.
- [ ] Check available storage capacity.
- [ ] Create the `Outlook Data` destination folder.
- [ ] Determine the appropriate supported OST relocation method.
- [ ] Preserve the existing 47.5 GB OST file.
- [ ] Configure the new OST location.
- [ ] Reinitialise Outlook and synchronise the mailbox.
- [ ] Confirm that error `0x8004060C` is resolved.
- [ ] Confirm that Desktop 1 remains unaffected.
- [ ] Update this documentation with the final implementation results.

---

## 11. Lessons Learnt

1. Two computers accessing the same Microsoft 365 mailbox maintain independent local OST files.
2. An OST file can grow considerably depending on mailbox size and cached data.
3. Outlook's default OST/PST size limit is generally 50 GB.
4. Cached Exchange Mode controls how much mailbox information is stored locally.
5. Changing the offline synchronisation period does not necessarily reduce an existing OST file's physical size immediately.
6. Rebuilding an OST file can resolve local cache problems, provided unsynchronised information is protected.
7. Outlook Web is an important diagnostic tool for distinguishing server-side mailbox issues from local Outlook problems.

---

**Documentation Status:** Troubleshooting documented; implementation and final verification pending.

**Environment:** Microsoft 365 Exchange Online / Classic Outlook / Windows Desktop.

**Incident Reference:** Outlook Error 0x8004060C.
