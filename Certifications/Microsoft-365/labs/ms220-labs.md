# MS-220: Exchange Support Engineer Labs

This document contains hands-on labs for the MS-220 certification.

## Table of Contents
1. [Lab 1: Troubleshoot Mail Flow](#lab-1-troubleshoot-mail-flow)
2. [Lab 2: Resolve Exchange Online Connectivity Issues](#lab-2-resolve-exchange-online-connectivity-issues)
3. [Lab 3: Investigate Spam and Phishing Issues](#lab-3-investigate-spam-and-phishing-issues)
4. [Lab 4: Troubleshoot Mobile Device Access](#lab-4-troubleshoot-mobile-device-access)
5. [Lab 5: Investigate Calendar Sharing Issues](#lab-5-investigate-calendar-sharing-issues)
6. [Lab 6: Analyze Exchange Online Protection (EOP)](#lab-6-analyze-exchange-online-protection-eop)
7. [Lab 7: Troubleshoot Hybrid Exchange Issues](#lab-7-troubleshoot-hybrid-exchange-issues)
8. [Lab 8: Investigate Retention and Compliance Issues](#lab-8-investigate-retention-and-compliance-issues)
9. [Lab 9: Troubleshoot Public Folders](#lab-9-troubleshoot-public-folders)
10. [Lab 10: Document and Escalate Support Cases](#lab-10-document-and-escalate-support-cases)

---

## Lab 1: Troubleshoot Mail Flow

**Objective**: Use mail flow tools to diagnose email delivery issues.

**Steps**:
1. Go to https://admin.exchange.microsoft.com and navigate to **Mail flow** > **Message trace**
2. Enter sender and recipient email addresses
3. Set date range to last 7 days
4. Click **Search**
5. Review the trace results showing message path
6. Click on a message to view detailed trace information:
   - Status (Delivered, Pending, Failed)
   - Events (Authentication, Filtering, Delivery)
   - Actions taken
7. For a failed message, note the error code and reason
8. Click **Message trace details** for complete information
9. Identify the failure point (spam filter, routing, connector, etc.)
10. Document the troubleshooting path and root cause

---

## Lab 2: Resolve Exchange Online Connectivity Issues

**Objective**: Diagnose and resolve client connectivity problems with Exchange Online.

**Steps**:
1. Go to https://admin.exchange.microsoft.com and navigate to **Recipients** > **Mailboxes**
2. Select a user experiencing connectivity issues
3. Check the mailbox details:
   - License status
   - Last activity
   - Email address
4. Go to the user's mailbox in **Outlook on the web** to verify access
5. If Outlook desktop client has issues, check connectivity:
   - Open **Control Panel** > **Mail** > **Show Profiles**
   - Select the profile and click **Properties**
   - Verify Exchange server connection
6. Check account authentication:
   - Go to https://myapps.microsoft.com to verify access
   - Check if MFA is configured properly
7. Test from a different device to isolate client issues
8. Review **Outlook client logs** for error details
9. If issues persist, reset user password and reconfigure Outlook
10. Document the troubleshooting steps and resolution

---

## Lab 3: Investigate Spam and Phishing Issues

**Objective**: Analyze and troubleshoot spam and phishing detection.

**Steps**:
1. Go to https://security.microsoft.com and navigate to **Email & collaboration** > **Threat policies** > **Spam filter**
2. Review the default spam filter policy
3. Check **High confidence spam actions** - set to Quarantine or Delete
4. Go to **Quarantine** and review quarantined messages
5. Look for false positives (legitimate emails marked as spam)
6. Click on a quarantined message to view details:
   - Sender
   - Subject
   - Detection rule
7. If it's a false positive, click **Release** and check **Should this have been filtered?**
8. Go to **Anti-phishing** policies and review settings
9. Check **User impersonation protection** is enabled
10. Go to **Threat & vulnerability management** > **Reports** > **Email security** to view threat analytics

---

## Lab 4: Troubleshoot Mobile Device Access

**Objective**: Diagnose mobile device mailbox access problems.

**Steps**:
1. Go to https://admin.exchange.microsoft.com and navigate to **Mobile** > **Mobile device mailbox policies**
2. Review your organization's mobile device policies
3. Check for any policies that restrict device access
4. Select a user having mobile access issues
5. Go to https://admin.exchange.microsoft.com > **Recipients** > **Mailboxes**
6. Select the user and check mobile device details
7. Look at **Mobile device access settings**
8. If access is blocked, verify the device meets policy requirements:
   - Device encryption enabled
   - Password meets complexity requirements
9. Use **Set-CasMailbox** PowerShell command to test access
10. Monitor device sync status and troubleshoot any remaining issues

---

## Lab 5: Investigate Calendar Sharing Issues

**Objective**: Troubleshoot calendar permission and sharing problems.

**Steps**:
1. Go to https://outlook.office.com and navigate to **Calendar**
2. Right-click on a calendar and select **Properties**
3. Check current sharing permissions
4. Try to share the calendar with another user
5. If sharing fails, verify the recipient is a valid user
6. Go back to mailbox in admin center and check **Calendar permissions**
7. Manually add sharing permissions using PowerShell if needed
8. Have the recipient accept the calendar invitation
9. Verify calendar appears in the recipient's Outlook
10. Test updating and modifying calendar entries between users

---

## Lab 6: Analyze Exchange Online Protection (EOP)

**Objective**: Review and test Exchange Online Protection policies.

**Steps**:
1. Go to https://security.microsoft.com and navigate to **Email & collaboration** > **Policies & rules** > **Threat policies**
2. Review all threat protection policies:
   - Spam filter
   - Malware filter
   - Anti-phishing
   - Advanced protection
3. Check **Outbound spam** policy for outbound message filtering
4. Go to **Reports** > **Email security** to view threat reports
5. Review **Malware detections** by date and type
6. Check **Phishing and spam detection** trends
7. Go to **Quarantine** and review quarantined messages
8. Analyze why specific messages were quarantined
9. Review administrator-only messages
10. Create a summary report of threat protection effectiveness

---

## Lab 7: Troubleshoot Hybrid Exchange Issues

**Objective**: Diagnose hybrid Exchange mail flow and connectivity.

**Steps**:
1. Go to https://admin.exchange.microsoft.com and navigate to **Mail flow** > **Connectors**
2. Review inbound and outbound connectors
3. Verify connector health and test connectivity:
   - Click on a connector
   - Click **Test** to validate settings
4. Review connector settings for:
   - Smart hosts
   - TLS configuration
   - Certificate validation
5. Go to **Message trace** and search for messages between on-premises and cloud
6. Verify mail is routing correctly
7. Check **Organization relationship** for federated organizations
8. Test calendar sharing between on-premises and cloud mailboxes
9. Review hybrid configuration settings
10. Document any mail flow issues and remediation steps

---

## Lab 8: Investigate Retention and Compliance Issues

**Objective**: Troubleshoot retention policies and compliance holds.

**Steps**:
1. Go to https://compliance.microsoft.com and navigate to **Data lifecycle management** > **Retention**
2. Review all retention policies in your organization
3. Check which policies apply to specific mailboxes
4. Select a user mailbox and verify retention tags applied
5. Go to **eDiscovery** > **Core eDiscovery** and create a case
6. Search for messages from a specific date range
7. Verify messages older than retention period are included
8. Place a hold on search results
9. Verify held messages are preserved
10. Search for messages that should have been deleted and verify they're removed

---

## Lab 9: Troubleshoot Public Folders

**Objective**: Diagnose and resolve public folder access and replication issues.

**Steps**:
1. Go to https://outlook.office.com and navigate to **Folders**
2. Look for **Public Folders** in the left panel
3. If public folders don't appear, check admin settings
4. Go to https://admin.exchange.microsoft.com and navigate to **Public folders**
5. Review public folder structure and permissions
6. Create a test public folder
7. Verify access to the public folder from multiple users
8. Check public folder mailbox status
9. Monitor public folder replication and health
10. Test adding and removing public folder items

---

## Lab 10: Document and Escalate Support Cases

**Objective**: Create and manage support cases with complete documentation.

**Steps**:
1. Go to https://admin.microsoft.com and navigate to **Support** > **New service request**
2. Click **+ New service request**
3. Fill in case details:
   - **Title**: Exchange connectivity issue - User mailbox
   - **Description**: Detailed explanation of the issue
   - **Affected services**: Exchange Online
   - **Severity**: Choose appropriate level
4. Attach supporting documentation:
   - Message trace results (screenshot or CSV export)
   - Mailbox configuration
   - Error logs
5. Include **Steps to reproduce** the issue
6. Click **Create** to submit the case
7. Note the case number for reference
8. Go to **Your support tickets** to track progress
9. Add follow-up information as needed
10. Document the final resolution and lessons learned
