# MS-740: Teams Support Engineer Labs

This document contains hands-on labs for the MS-740 certification.

## Table of Contents
1. [Lab 1: Troubleshoot Teams Sign-In Issues](#lab-1-troubleshoot-teams-sign-in-issues)
2. [Lab 2: Resolve Meeting and Call Quality Issues](#lab-2-resolve-meeting-and-call-quality-issues)
3. [Lab 3: Troubleshoot Messaging Issues](#lab-3-troubleshoot-messaging-issues)
4. [Lab 4: Investigate Teams Device Issues](#lab-4-investigate-teams-device-issues)
5. [Lab 5: Analyze Teams Network Connectivity](#lab-5-analyze-teams-network-connectivity)
6. [Lab 6: Troubleshoot Teams App Issues](#lab-6-troubleshoot-teams-app-issues)
7. [Lab 7: Investigate Compliance and Retention Issues](#lab-7-investigate-compliance-and-retention-issues)
8. [Lab 8: Troubleshoot Teams Voice and Calling](#lab-8-troubleshoot-teams-voice-and-calling)
9. [Lab 9: Monitor Teams Health and Service Status](#lab-9-monitor-teams-health-and-service-status)
10. [Lab 10: Escalate and Document Support Cases](#lab-10-escalate-and-document-support-cases)

---

## Lab 1: Troubleshoot Teams Sign-In Issues

**Objective**: Diagnose and resolve Teams authentication problems.

**Steps**:
1. Enable verbose logging on a Teams client: Set environment variable `HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Teams` with `LogLevel` = 1
2. Attempt to sign in to Teams and observe login failure
3. Go to **%appdata%\Microsoft\Teams** and collect the Teams debug logs
4. Review logs for authentication errors (look for 401, 403 errors)
5. Check if user account is licensed and active in Azure AD
6. Test sign-in with another user to isolate user vs. tenant issue
7. Check for cached credentials: Delete **%appdata%\Microsoft\Teams\Local Storage**
8. Clear Teams cache and attempt sign-in again
9. If MFA is required, verify user has MFA device registered
10. Document root cause and resolution steps

---

## Lab 2: Resolve Meeting and Call Quality Issues

**Objective**: Diagnose and fix Teams meeting and calling quality problems.

**Steps**:
1. Go to https://admin.teams.microsoft.com and navigate to **Analytics & reports** > **Call Quality Dashboard**
2. Search for a user experiencing meeting quality issues
3. Review their meeting history and identify poor quality sessions
4. Click on a meeting to view detailed diagnostics:
   - Codec used
   - Network latency
   - Packet loss
   - Jitter
5. Check audio/video device information
6. Go to **Advanced diagnostics** for packet-level analysis
7. Identify common issues:
   - High packet loss (>1%)
   - High jitter (>30ms)
   - High latency (>150ms)
8. Provide recommendations:
   - Upgrade network connection
   - Move closer to WiFi router
   - Close bandwidth-consuming applications
9. Re-test after implementing recommendations
10. Document baseline and improved metrics

---

## Lab 3: Troubleshoot Messaging Issues

**Objective**: Diagnose and resolve Teams chat and messaging delivery problems.

**Steps**:
1. Go to https://teams.microsoft.com and attempt to send a message to a user
2. If delivery fails, note the error message
3. Check if recipient is online in Teams
4. Go to https://admin.teams.microsoft.com and verify recipient user is active
5. Check if there are any channel or team message policies restricting messaging
6. Navigate to **Messaging** > **Messaging policies** and review settings
7. Test messaging in different channels to isolate the issue
8. Check Teams client logs: **%appdata%\Microsoft\Teams\logs.txt**
9. Look for message delivery errors or network timeouts
10. Document the issue, troubleshooting steps, and resolution

---

## Lab 4: Investigate Teams Device Issues

**Objective**: Troubleshoot Teams hardware device problems.

**Steps**:
1. Go to https://admin.teams.microsoft.com and navigate to **Devices** > **IP phones**
2. Identify a device with connectivity issues
3. Click on the device to view status and logs
4. Check device connectivity:
   - Is device online or offline?
   - Last check-in time
5. Review device firmware version
6. If device is offline, check network connectivity:
   - Ping device IP address
   - Check network cables
   - Verify DHCP configuration
7. Check device logs for error messages
8. If needed, restart the device via admin center
9. Verify device comes back online
10. Document troubleshooting steps and resolution

---

## Lab 5: Analyze Teams Network Connectivity

**Objective**: Assess Teams network requirements and identify connectivity issues.

**Steps**:
1. Go to https://admin.teams.microsoft.com and navigate to **Analytics & reports** > **Call Quality Dashboard**
2. Check network health metrics across all users
3. Identify subnets or locations with poor connectivity
4. Run the **Network Assessment Tool** on a test machine
5. The tool will test bandwidth, latency, and jitter to Teams services
6. Review results:
   - Minimum bandwidth requirements
   - Recommended bandwidth
   - Network performance metrics
7. Check for WiFi vs. wired connection differences
8. Analyze network performance at different times of day
9. Create a network baseline report
10. Document network recommendations for Teams deployment

---

## Lab 6: Troubleshoot Teams App Issues

**Objective**: Diagnose and resolve problems with Teams apps and integrations.

**Steps**:
1. In Teams, go to **...** (More) > **Apps**
2. Search for an app you want to troubleshoot
3. Try to launch the app and note any error messages
4. Go to **Admin center** > **Manage apps** to verify app is installed
5. Check app permission policies to ensure user has access
6. Go to **Org-wide app settings** and verify app is allowed
7. Check if app has any system messages or known issues
8. Try to reload the app in Teams (F5 refresh)
9. Clear Teams cache if issues persist
10. Document any third-party app errors or limitations

---

## Lab 7: Investigate Compliance and Retention Issues

**Objective**: Troubleshoot retention and compliance policy issues.

**Steps**:
1. Go to https://compliance.microsoft.com and navigate to **Data lifecycle management** > **Retention**
2. Review your organization's retention policies
3. Check which policies apply to Teams
4. Go to a Team and check message retention:
   - Are old messages being deleted per policy?
5. Navigate to **Content search** and search for Teams messages
6. Look for discrepancies between retention policy and actual content
7. Go to **eDiscovery** > **Core eDiscovery** to create a case
8. Search for specific Teams messages on hold
9. Verify messages are preserved correctly
10. Document any retention policy issues and fixes

---

## Lab 8: Troubleshoot Teams Voice and Calling

**Objective**: Diagnose and resolve Teams voice and calling failures.

**Steps**:
1. Go to https://admin.teams.microsoft.com and navigate to **Analytics & reports** > **Call Analytics**
2. Search for a user with calling issues
3. Find a failed call in their history
4. Click on the call to view diagnostics
5. Check the call state (connected, failed, etc.)
6. Review session initiation protocol (SIP) response codes
7. Identify failure reason (poor network, registration issue, etc.)
8. Go to **Direct Routing** and verify SBC health if applicable
9. Check if user is assigned a calling plan or Direct Routing policy
10. Document the call failure reason and resolution steps

---

## Lab 9: Monitor Teams Health and Service Status

**Objective**: Monitor Teams service health and respond to incidents.

**Steps**:
1. Go to https://admin.microsoft.com and navigate to **Health** > **Service health**
2. Check the status of all Microsoft 365 services
3. Look for any Teams-related incidents or advisories
4. Click on an incident to view details:
   - Affected services
   - Start time
   - Expected resolution time
5. Go to **Message center** to see service announcements
6. Set up **Notification preferences** to receive alerts
7. Go back to Service health and check **Health history**
8. Review past incidents and their impact
9. Create a health dashboard for monitoring
10. Document your organization's service health baseline

---

## Lab 10: Escalate and Document Support Cases

**Objective**: Create and manage support cases with proper documentation.

**Steps**:
1. Go to https://admin.microsoft.com and navigate to **Support** > **New service request**
2. Click **+ New service request**
3. Fill in service request details:
   - Title: Clear, concise description
   - Description: Detailed problem statement
   - Affected users: Specific users impacted
   - Severity: High, Medium, Low
4. Attach relevant diagnostics and logs
5. Include steps to reproduce the issue
6. Submit the support case
7. Go to **Your support tickets** to track the case
8. Monitor ticket status and responses
9. If needed, follow up with additional information
10. Document the complete case resolution for future reference
