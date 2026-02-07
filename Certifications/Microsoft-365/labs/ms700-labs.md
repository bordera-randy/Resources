# MS-700: Teams Administrator Labs

This document contains hands-on labs for the MS-700 certification.

## Table of Contents
1. [Lab 1: Create and Manage Teams](#lab-1-create-and-manage-teams)
2. [Lab 2: Configure Meeting Policies](#lab-2-configure-meeting-policies)
3. [Lab 3: Manage Messaging Policies](#lab-3-manage-messaging-policies)
4. [Lab 4: Set Up Teams Live Events](#lab-4-set-up-teams-live-events)
5. [Lab 5: Configure Teams Devices](#lab-5-configure-teams-devices)
6. [Lab 6: Manage Teams Apps](#lab-6-manage-teams-apps)
7. [Lab 7: Configure Voice Settings](#lab-7-configure-voice-settings)
8. [Lab 8: Monitor Teams Usage](#lab-8-monitor-teams-usage)
9. [Lab 9: Manage Teams Compliance](#lab-9-manage-teams-compliance)
10. [Lab 10: Troubleshoot Teams Issues](#lab-10-troubleshoot-teams-issues)

---

## Lab 1: Create and Manage Teams

**Objective**: Create a Teams environment and configure policies.

**Steps**:
1. Go to https://teams.microsoft.com and sign in
2. Click **+ Create or join a team**
3. Select **Create a team** > **From scratch**
4. Choose **Private** as the team type
5. Name the team "Project Alpha" and add description
6. Click **Create**
7. In the General channel, click **+ Add channel**
8. Create three channels: Resources, Announcements, and Updates
9. Click **Manage team** and then **Settings**
10. Configure guest access settings and member permissions

---

## Lab 2: Configure Meeting Policies

**Objective**: Create and apply Teams meeting policies.

**Steps**:
1. Go to https://admin.teams.microsoft.com and navigate to **Meetings** > **Meeting policies**
2. Click **+ Add**
3. Name the policy "Meeting Policy - Standard"
4. Configure the following settings:
   - **Allow scheduling private meetings**: On
   - **Allow Meet now**: On
   - **Allow channel meetings**: On
   - **Allow private meeting scheduling**: On
   - **Allow users to record**: On
5. Set **Who can present**: Everyone
6. Set **Require a watermark for video**: Off
7. Click **Save**
8. Go to **Users** and assign the policy to a test user group
9. Test meeting creation with the policy applied
10. Create a meeting and verify all configured settings are available

---

## Lab 3: Manage Messaging Policies

**Objective**: Create policies to control chat and messaging features.

**Steps**:
1. Go to https://admin.teams.microsoft.com and navigate to **Messaging** > **Messaging policies**
2. Click **+ Add**
3. Name the policy "Messaging Policy - Standard"
4. Configure the following settings:
   - **Owners can delete sent messages**: Yes
   - **Users can delete sent messages**: Yes
   - **Users can edit sent messages**: Yes
   - **Read receipts**: On
   - **Chat**: On
   - **Giphy in messages**: Moderate
   - **Sticker set in messages**: On
   - **Allow users to chat with external users**: On
5. Click **Save**
6. Assign the policy to test users
7. Test messaging features with the policy applied
8. Create a message and test edit and delete functionality
9. Test chat with external users to verify policy enforcement
10. Document all messaging features available under this policy

---

## Lab 4: Set Up Teams Live Events

**Objective**: Schedule and configure a Teams Live Event.

**Steps**:
1. Go to https://teams.microsoft.com and click **Calendar** on the left
2. Click **+ New event**
3. Fill in event details: Title, Date, Time, Description
4. Toggle **Make this a live event** to **On**
5. Set **Event type** to **Teams live event**
6. Configure **Presenter(s)** and **Event group**
7. Set **Audience**: Who can watch the live event?
8. Click **Save**
9. Go to **Live events** in Teams to see your scheduled event
10. 10 minutes before the event, start the live event and test streaming

---

## Lab 5: Configure Teams Devices

**Objective**: Manage Teams devices and firmware updates.

**Steps**:
1. Go to https://admin.teams.microsoft.com and navigate to **Devices** > **IP phones**
2. Review connected Teams phones and their status
3. Click on a device to view device details
4. Go to **Devices** > **Teams rooms** and review any Teams Rooms devices
5. Navigate to **Device management** > **Device firmware**
6. Review available firmware updates
7. If updates are available, select a test device and click **Update firmware**
8. Monitor the update progress
9. Go to **Device logs** to review device activity and logs
10. Document device health and any issues observed

---

## Lab 6: Manage Teams Apps

**Objective**: Add and configure third-party apps in Teams.

**Steps**:
1. Go to https://admin.teams.microsoft.com and navigate to **Manage apps**
2. Search for an app (e.g., "Trello")
3. Click on the app to view details
4. Toggle **Org-wide app settings** to allow the app for all users
5. Click the app again and configure any settings
6. Go to **Permission policies** and create a new policy
7. Name it "App Policy - Standard"
8. Select which apps are allowed
9. Assign the policy to test users
10. Go to Teams and verify users can access the apps per the policy

---

## Lab 7: Configure Voice Settings

**Objective**: Set up Teams calling plans and phone numbers.

**Steps**:
1. Go to https://admin.teams.microsoft.com and navigate to **Voice** > **Calling policies**
2. Click **+ Add**
3. Name the policy "Calling Policy - Standard"
4. Configure settings:
   - **Make private calls**: On
   - **Call recording**: User controlled
   - **Call forwarding**: On
   - **Simultaneous ringing**: On
5. Click **Save**
6. Go to **Phone numbers** and review available numbers
7. Assign a phone number to a test user
8. Test calling between users with the policy applied
9. Go to **Calling policies** > **Call transfer settings** and configure call routing
10. Test call forwarding and voicemail functionality

---

## Lab 8: Monitor Teams Usage

**Objective**: Review Teams analytics and usage reports.

**Steps**:
1. Go to https://admin.teams.microsoft.com and navigate to **Analytics & reports** > **Teams usage**
2. Review the overall usage dashboard
3. Check **Active users** and **Active teams**
4. Go to **User activity report** and review user engagement metrics
5. Filter by date range and department
6. Navigate to **Device usage** to see what devices users are using Teams on
7. Check **Meeting and call quality** for call metrics
8. Go to **App usage** to see which apps are most used
9. Export a usage report as CSV for analysis
10. Create a summary of top 5 active teams and users

---

## Lab 9: Manage Teams Compliance

**Objective**: Configure retention and DLP policies for Teams.

**Steps**:
1. Go to https://compliance.microsoft.com and navigate to **Data lifecycle management** > **Retention**
2. Click **+ Create retention policy**
3. Name the policy "Teams Data Retention - 1 Year"
4. Select **Teams channel messages** and **Teams chats**
5. Set retention period to **1 year**
6. Set action to **Delete content**
7. Assign to your organization
8. Click **Create**
9. Go to **Data loss prevention** > **Policies**
10. Create a DLP policy to prevent sensitive data sharing in Teams

---

## Lab 10: Troubleshoot Teams Issues

**Objective**: Use diagnostic tools to troubleshoot Teams problems.

**Steps**:
1. Go to https://admin.teams.microsoft.com and navigate to **Analytics & reports** > **Call analytics**
2. Search for a specific user to view their call history
3. Click on a call to view detailed analytics including latency, packet loss
4. Navigate to **Call quality dashboard** to analyze audio and video quality
5. Go to **Teams logs and diagnostics** and enable diagnostics for a test user
6. Have the user reproduce an issue while diagnostics are enabled
7. Download the diagnostic log
8. Review the log for error messages and warnings
9. Go to **Meeting diagnostics** and analyze meeting quality issues
10. Document troubleshooting steps and recommendations
