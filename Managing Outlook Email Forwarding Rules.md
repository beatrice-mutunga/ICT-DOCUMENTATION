# Managing Outlook Email Forwarding Rules – Bank Transaction Notifications

## 1. Overview

This documentation covers the investigation and modification of an existing Microsoft Outlook email forwarding configuration used to distribute Bank transaction notification emails to the firm's Accounts department and an additional recipient named ****.

The original configuration had been established before I took over the task. The objective was to understand how the forwarding arrangement worked, identify where the recipients were configured, and remove *** without interrupting the automatic delivery of transaction notifications to the Accounts email address.

### Objectives

- Understand how automatic email forwarding works in Microsoft Outlook.
- Identify the existing forwarding configuration.
- Establish how Bank transaction notifications are identified.
- Remove *** from the forwarding arrangement.
- Retain the Accounts email address as a recipient.
- Preserve the existing forwarding conditions.
- Understand how to manage and troubleshoot similar configurations in future.

## 2. Understanding Email Forwarding in Microsoft Outlook

Microsoft Outlook provides different ways of automatically distributing incoming emails.

Before making changes, it is important to understand the available methods.

### 2.1 Inbox Rules

Inbox rules allow Outlook to automatically perform actions on incoming emails based on specified conditions.

For example:

**Condition:**
- The incoming email is from  x Bank.
- The subject contains a specified transaction-related keyword.

**Action:**
- Forward the email to another recipient.
- Redirect the email to another recipient.
- Move the email to a folder.
- Apply other automated actions.

Rules can be configured to apply to specific emails instead of forwarding every message received in the mailbox.

### 2.2 Automatic Forwarding

This setting forwards incoming emails to another email address automatically.

Unlike inbox rules, automatic forwarding can apply to all incoming emails, depending on the configuration.

This option is generally found under:

Settings → Mail → Forwarding.

### 2.3 Microsoft 365 Exchange Mail Flow Rules

An administrator can also configure forwarding through the Exchange Admin Centre.

These are commonly called mail flow rules or transport rules.

They operate at the Microsoft Exchange organisation level and can apply to messages based on sender, recipient, subject, or other conditions.

Location:

Microsoft 365 Admin Centre → Exchange Admin Centre → Mail flow → Rules.

**Important:** These three methods are different. When investigating an existing forwarding arrangement, the actual configuration must be identified before making changes.

## 3. Procedure: Investigating Outlook Forwarding Rules

### Step 1: Access Outlook

1. Open a web browser.
2. Navigate to https://outlook.office.com.
3. Sign in using the relevant company email account.
4. Open the Outlook mailbox.

Using Outlook on the web allows mailbox settings to be inspected independently of the local Outlook desktop installation.

### Step 2: Access Mail Settings

1. Click the Settings (gear) icon in the top-right corner.
2. Navigate to Mail.
3. Select Rules.

### Step 3: Identify the Relevant Rule

Inspect the available rules and identify the one responsible for distributing Bank transaction notifications.

Look for rules containing references to:

- X Bank.
- Transaction notifications.
- Bank alerts.
- Accounts email address.
- Automatic forwarding or redirection.

Open the relevant rule to inspect its conditions and actions.

### Step 4: Understand the Rule Components

A typical forwarding rule contains two main components.

**A. Conditions**

These determine which emails trigger the rule.

Examples:

- Sender is X Bank.
- Subject contains a transaction notification keyword.
- Message meets another specified condition.

**B. Actions**

These determine what Outlook does when an email meets the conditions.

Examples:

- Forward to a specified email address.
- Redirect to a specified email address.
- Move the message to a designated folder.

Understanding these components is important because changing a condition could affect which bank notifications are distributed.

## 4. Procedure: Removing an Unwanted Recipient

### Objective

Remove *** from the existing Bank transaction notification forwarding arrangement while retaining the Accounts email address.

### Steps

1. Open the relevant forwarding rule.
2. Inspect the configured forwarding recipients.
3. Identify ***'s email address.
4. Remove ***'s address from the recipient list.
5. Confirm that the Accounts email address remains configured.
6. Ensure the existing Bank conditions remain unchanged.
7. Save the modified rule.

### Important Precautions

- Do not delete the entire rule.
- Do not remove the Accounts email address.
- Do not modify the Bank sender or subject conditions unnecessarily.
- Do not disable general mailbox forwarding unless it is confirmed to be part of the unwanted arrangement.
- Do not modify Exchange organisation-wide mail flow rules without understanding their impact.

The objective is to remove one recipient, not disrupt the existing notification distribution process.

## 5. Testing and Verification

After modifying the rule, verify that the configuration is working as intended.

### Recommended verification procedure

1. Reopen Outlook Settings → Mail → Rules.
2. Confirm that the relevant rule is still enabled.
3. Open the rule and inspect its forwarding recipients.
4. Confirm that the Accounts email address is still present.
5. Confirm that ***'s address is no longer included.
6. Obtain or wait for a legitimate Bank transaction notification.
7. Confirm that the notification reaches the intended Accounts mailbox.

Where possible, check the original mailbox and the Accounts mailbox to establish that the notification was delivered successfully.

Do not use a live financial transaction merely to test email forwarding without the appropriate approval.

**Expected result:**

- Bank transaction notification emails continue to be distributed to Accounts.
- *** is no longer included in the forwarding arrangement.
- The original forwarding conditions remain intact.

## 6. Troubleshooting

| Problem | Possible cause | Recommended action |
|---|---|---|
| Accounts stops receiving notifications | Forwarding rule was disabled or modified incorrectly | Inspect the rule and restore the correct recipient and conditions |
| *** continues receiving notifications | Another forwarding mechanism may exist | Inspect mailbox forwarding settings and Exchange mail flow rules |
| No X Bank notifications are forwarded | Rule conditions may not match incoming emails | Inspect sender and subject conditions |
| Rule cannot be edited | Permissions or organisation-level configuration | Consult the Microsoft 365 administrator |
| Duplicate notifications are received | Multiple rules or forwarding mechanisms may be active | Inspect all relevant rules and forwarding settings |

## 7. Understanding Forward vs Redirect

These two actions are related but behave differently.

**Forward:**
- Outlook sends the original email as a forwarded message.
- The forwarded message may show that it was forwarded by the mailbox owner.
- The original sender's message is included in the forwarded content.

**Redirect:**
- The message is delivered to another recipient while retaining the original sender information.
- The recipient generally sees the message as originating from the original sender.

This distinction is useful when dealing with financial notifications because the receiving department may need to identify the original sender easily.

## 8. Security and Access Considerations

Bank transaction notifications contain potentially confidential financial information.

The following practices should be observed:

- Only authorised employees should receive transaction notifications.
- Periodically review forwarding recipients.
- Remove recipients who no longer require access.
- Avoid forwarding financial notifications to personal email accounts without authorisation.
- Maintain records of changes to email forwarding configurations.
- Ensure that forwarding arrangements comply with the firm's information security and confidentiality requirements.

## 9. Final Outcome

The existing Outlook forwarding arrangement for X Bank transaction notifications was reviewed and updated.

The unwanted recipient, ***, was removed while retaining the Accounts email address.

The objective was to maintain the existing automated distribution of bank transaction notifications without disrupting the Accounts department's access to the emails.

## 10. ICT Lessons Learned

This task provided practical exposure to Microsoft Outlook email management and automated email distribution.

Key lessons:

1. Outlook rules can automate the distribution of specific incoming emails.
2. Rules consist of conditions and actions.
3. Multiple recipients can be included in a forwarding arrangement.
4. Removing a recipient does not necessarily require deleting the entire rule.
5. Automatic forwarding, inbox rules, and Exchange mail flow rules are separate mechanisms.
6. Changes to email forwarding should be made carefully, particularly where financial information is involved.
7. Configuration changes should be verified after implementation.

## 11. Microsoft Documentation and Reference Links

- Outlook Rules: https://support.microsoft.com/en-us/outlook/mail/use-rules-to-automatically-forward-messages
- Outlook on the web: https://outlook.office.com
- Microsoft Exchange Admin Centre: https://admin.exchange.microsoft.com
- Microsoft 365 Admin Centre: https://admin.microsoft.com

---

## 12. Change Record

| Item | Details |
|---|---|
| System | Microsoft Outlook / Microsoft 365 |
| Function | Automatic email forwarding |
| Source | X Bank transaction notifications |
| Original recipients | Accounts and *** |
| Change implemented | Removed *** |
| Retained recipient | Accounts email address |
| Configuration objective | Maintain automated transaction notification distribution |
| Change type | Email rule modification |
| Documentation | ICT Technical Procedure |

**Note:** The exact mailbox address, rule name, sender conditions, and forwarding action should be recorded in the internal ICT configuration register if they are needed for future troubleshooting. The actual configuration method should also be confirmed from the mailbox before treating it as an Exchange or Outlook-specific rule.
