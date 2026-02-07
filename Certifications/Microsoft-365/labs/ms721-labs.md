# MS-721: Collaboration Communications Systems Engineer Labs

This document contains hands-on labs for the MS-721 certification.

## Table of Contents
1. [Lab 1: Configure Direct Routing](#lab-1-configure-direct-routing)
2. [Lab 2: Set Up Session Border Controller (SBC)](#lab-2-set-up-session-border-controller-sbc)
3. [Lab 3: Configure Teams Phone System](#lab-3-configure-teams-phone-system)
4. [Lab 4: Monitor Call Quality](#lab-4-monitor-call-quality)
5. [Lab 5: Configure Emergency Calling](#lab-5-configure-emergency-calling)
6. [Lab 6: Integrate Teams with On-Premises PBX](#lab-6-integrate-teams-with-on-premises-pbx)
7. [Lab 7: Manage Teams Devices](#lab-7-manage-teams-devices)
8. [Lab 8: Configure Teams Rooms](#lab-8-configure-teams-rooms)
9. [Lab 9: Implement Compliance Recording](#lab-9-implement-compliance-recording)
10. [Lab 10: Troubleshoot Teams Voice Issues](#lab-10-troubleshoot-teams-voice-issues)

---

## Lab 1: Configure Direct Routing

**Objective**: Set up Direct Routing to connect on-premises PSTN networks to Teams.

**Steps**:
1. Go to https://admin.teams.microsoft.com and navigate to **Voice** > **Direct Routing**
2. Click **+ Add SBC** to add a Session Border Controller
3. Enter the SBC FQDN (e.g., sbc.contoso.com)
4. Configure SBC settings including Media Bypass
5. Click **Save**
6. Verify the SBC connectivity status
7. Go to **Voice routes** and click **+ New**
8. Create a voice route for phone number pattern (e.g., +1206*)
9. Select the SBC to route calls through
10. Test the voice route by making a call from a Teams user

---

## Lab 2: Set Up Session Border Controller (SBC)

**Objective**: Register and configure a Session Border Controller for Direct Routing.

**Steps**:
1. Obtain SBC hardware (physical or virtual) compatible with Microsoft Teams
2. Go to https://admin.teams.microsoft.com and navigate to **Voice** > **Direct Routing** > **SBCs**
3. Get the SBC configuration requirements from Microsoft documentation
4. Configure the SBC with the Teams environment details:
   - FQDN
   - Certificate
   - Media settings
5. Register the SBC in the Teams admin center
6. Configure transport settings (TLS)
7. Enable Media Bypass if applicable
8. Run connectivity tests from the SBC to Microsoft Teams
9. Review SBC logs for any connection errors
10. Document the complete SBC configuration

---

## Lab 3: Configure Teams Phone System

**Objective**: Set up phone numbers and auto attendants in Teams.

**Steps**:
1. Go to https://admin.teams.microsoft.com and navigate to **Voice** > **Phone numbers**
2. Click **+ Add** to acquire a new phone number
3. Select your country/region and number type
4. Choose an available number or port an existing one
5. Assign the number to a user or resource account
6. Go to **Auto attendants** and click **+ Add**
7. Name the auto attendant "Company Auto Attendant"
8. Configure call flow:
   - Greeting message
   - Menu options (Press 1 for Sales, Press 2 for Support)
   - Transfer routing
9. Set business hours and after-hours settings
10. Click **Save** and test the auto attendant by calling it

---

## Lab 4: Monitor Call Quality

**Objective**: Use Teams analytics tools to monitor and analyze call quality.

**Steps**:
1. Go to https://admin.teams.microsoft.com and navigate to **Analytics & reports** > **Call Quality Dashboard**
2. Review overall call quality metrics
3. Filter by date range to see trends
4. Go to **Call Analytics** and search for a specific user
5. Select a call from the user's history
6. Review detailed metrics:
   - Average latency
   - Packet loss
   - Jitter
   - Network performance
7. Identify any calls with poor quality
8. Navigate to **Advanced diagnostics** for detailed packet-level information
9. Create a quality report by exporting data
10. Document top 3 call quality issues and recommendations

---

## Lab 5: Configure Emergency Calling

**Objective**: Set up emergency locations and e911 policies.

**Steps**:
1. Go to https://admin.teams.microsoft.com and navigate to **Voice** > **Emergency policies**
2. Click **+ Add location** to define emergency locations
3. Enter location details:
   - Country
   - State/Province
   - City
   - Street address
4. Define emergency response locations
5. Go to **Emergency calling policies**
6. Create a new policy with emergency notification settings
7. Configure who should be notified in an emergency
8. Assign the policy to users
9. Test emergency calling by having a user dial emergency number
10. Review emergency call routing and confirmation of location

---

## Lab 6: Integrate Teams with On-Premises PBX

**Objective**: Configure hybrid voice connectivity between Teams and on-premises systems.

**Steps**:
1. Go to https://admin.teams.microsoft.com and navigate to **Voice** > **Hybrid voice**
2. Review hybrid voice configuration requirements
3. Configure the on-premises PBX to communicate with Teams
4. Set up SIP trunks between PBX and Direct Routing SBC
5. Configure call routing policies to determine when calls route to cloud or on-premises
6. Test calls between Teams users and PBX-based users
7. Verify call quality and routing
8. Configure number translation rules if needed
9. Set up failover routing for redundancy
10. Document the hybrid voice architecture

---

## Lab 7: Manage Teams Devices

**Objective**: Register and manage Teams phones and peripherals.

**Steps**:
1. Go to https://admin.teams.microsoft.com and navigate to **Devices** > **IP phones**
2. Review connected Teams phones
3. Click **+ Add devices** to provision new phones
4. Assign MAC addresses for the phones
5. Configure phone settings including firmware
6. Go to **Audio devices** to manage speakers and microphones
7. Register Teams peripherals
8. Set up device groups for bulk management
9. Monitor device health and status
10. Update firmware across device groups

---

## Lab 8: Configure Teams Rooms

**Objective**: Set up and manage Microsoft Teams Rooms devices.

**Steps**:
1. Go to https://admin.teams.microsoft.com and navigate to **Devices** > **Teams Rooms**
2. Click **+ Add device** to provision a new Teams Room
3. Assign resource account for the room
4. Assign a calendar for room bookings
5. Configure camera, microphone, and display settings
6. Set up dual display configuration
7. Configure room settings:
   - Room name
   - Location
   - Capacity
8. Test meeting joining from the Teams Room
9. Monitor room availability and usage
10. Review device logs for any issues

---

## Lab 9: Implement Compliance Recording

**Objective**: Enable and configure compliance recording for Teams calls.

**Steps**:
1. Go to https://admin.teams.microsoft.com and navigate to **Voice** > **Call recording policies**
2. Create a new call recording policy
3. Enable **Compliance recording**
4. Configure recording scope:
   - Record incoming calls only
   - Record all calls
5. Set recording notifications to inform users
6. Configure storage location for recordings
7. Set retention policy for recorded calls
8. Assign the policy to users who need compliance recording
9. Test by making a call with compliance recording enabled
10. Verify recording is created and stored according to policy

---

## Lab 10: Troubleshoot Teams Voice Issues

**Objective**: Diagnose and resolve Teams voice and calling problems.

**Steps**:
1. Go to https://admin.teams.microsoft.com and navigate to **Analytics & reports** > **Call Quality Dashboard**
2. Search for a user experiencing voice issues
3. Review their call history for failed or poor quality calls
4. Click on a problem call to view diagnostics
5. Analyze the diagnostics data:
   - Media codec used
   - Network metrics
   - Device information
6. Go to **Advanced diagnostics** for deeper packet analysis
7. Check **Call Analytics** for specific user journey
8. Review SBC logs if using Direct Routing
9. Create diagnostic logs from the user's Teams client
10. Document the issue, root cause, and resolution steps taken
