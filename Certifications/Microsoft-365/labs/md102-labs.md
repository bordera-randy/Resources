# MD-102: Endpoint Administrator Labs

This document contains hands-on labs for the MD-102 certification.

## Table of Contents
- [MD-102: Endpoint Administrator Labs](#md-102-endpoint-administrator-labs)
  - [Table of Contents](#table-of-contents)
  - [Lab 1: Enroll Windows Devices in Intune](#lab-1-enroll-windows-devices-in-intune)
  - [Lab 2: Configure Device Compliance Policies](#lab-2-configure-device-compliance-policies)
  - [Lab 3: Deploy Applications via Intune](#lab-3-deploy-applications-via-intune)
  - [Lab 4: Configure Windows Autopilot](#lab-4-configure-windows-autopilot)
  - [Lab 5: Manage Device Security](#lab-5-manage-device-security)
  - [Lab 6: Set Up Windows Update Rings](#lab-6-set-up-windows-update-rings)
  - [Lab 7: Configure Endpoint Protection](#lab-7-configure-endpoint-protection)
  - [Lab 8: Manage Mobile Devices](#lab-8-manage-mobile-devices)
  - [Lab 9: Use Remote Actions](#lab-9-use-remote-actions)
  - [Lab 10: Monitor and Report on Devices](#lab-10-monitor-and-report-on-devices)

---

## Lab 1: Enroll Windows Devices in Intune

**Objective**: Enroll a Windows 10/11 device into Microsoft Intune for management.

**Steps**:
1. Go to https://intune.microsoft.com and sign in as an admin
2. Navigate to **Devices** > **Windows** > **Windows enrollment**
3. Review the enrollment methods available
4. On a test Windows device, go to **Settings** > **Accounts** > **Access work or school**
5. Click **+ Connect** and enter your Microsoft 365 work account
6. Follow the enrollment prompts to add the device to Azure AD
7. Complete any MFA challenges if prompted
8. Once enrolled, go back to Intune and navigate to **Devices** > **Windows** > **All devices**
9. Verify your test device appears in the device list
10. Click on the device and review the device properties including name, OS version, and enrollment status

---

## Lab 2: Configure Device Compliance Policies

**Objective**: Create and assign device compliance policies to ensure devices meet security requirements.

**Steps**:
1. Go to https://intune.microsoft.com and navigate to **Devices** > **Compliance** > **Policies**
2. Click **+ Create policy**
3. Select **Windows 10 and later** as the platform
4. Name the policy "Compliance Policy - Windows"
5. Configure the following compliance rules:
   - Set **Require a minimum OS version** to Windows 10 (Build 19041)
   - Set **Maximum OS version** to current version
   - Enable **Require BitLocker**
   - Enable **Require Windows Defender Antimalware**
6. Click **Next** and select your test device group under **Assignments**
7. Click **Review + Create** to finalize the policy
8. After deployment, go to **Devices** > **All devices** and select your test device
9. Check the **Compliance** tab to see the device's compliance status
10. Review any non-compliant items and document remediation steps

---

## Lab 3: Deploy Applications via Intune

**Objective**: Deploy a Win32 application to managed devices through Intune.

**Steps**:
1. Go to https://intune.microsoft.com and navigate to **Apps** > **All apps**
2. Click **+ Add** and select **Windows app (Win32)**
3. Click **Select app package file** and upload a sample .intunewin file (create one using the Win32 Content Prep Tool if needed)
4. Fill in the app information:
   - **Display name**: Test Application
   - **Description**: A test app for learning purposes
5. Configure the installation behavior:
   - **Install command**: msiexec /i "application.msi"
   - **Uninstall command**: msiexec /x "application.msi"
6. Click **Next** and set **Assignment type** to **Available** or **Required**
7. Select your test device group under **Assignments**
8. Click **Create** to deploy the app
9. Go to **Devices** > **All devices** and select your test device
10. Navigate to the **Managed apps** tab to verify the app assignment appears

---

## Lab 4: Configure Windows Autopilot

**Objective**: Set up Windows Autopilot for zero-touch device provisioning.

**Steps**:
1. Go to https://intune.microsoft.com and navigate to **Devices** > **Windows** > **Windows Autopilot**
2. Click **+ Import devices** to register devices for Autopilot
3. Upload a CSV file with device serial numbers and hardware identifiers
4. Click **Import** to add the devices
5. Navigate to **Deployment profiles** and click **+ Create profile**
6. Select **Windows 10 and later** as the platform
7. Name the profile "Autopilot Profile - Test"
8. Configure the following settings:
   - **Deployment mode**: User-driven (Azure AD join)
   - **Language**: English (United States)
   - **Skip EULA acceptance**: Yes
   - **Skip privacy settings**: Yes
9. Click **Next** and assign the profile to your test device group
10. Click **Create** to finalize the profile

---

## Lab 5: Manage Device Security

**Objective**: Configure BitLocker encryption through Intune.

**Steps**:
1. Go to https://intune.microsoft.com and navigate to **Devices** > **Configuration profiles**
2. Click **+ Create profile**
3. Select **Windows 10 and later** and choose **Templates** > **Endpoint protection**
4. Name the profile "Endpoint Protection - Encryption"
5. In the configuration settings, find the **Windows Encryption** section
6. Set **Encrypt devices** to **Yes**
7. Set **BitLocker OS drive protection** to **Enabled**
8. Set **BitLocker fixed data-drive protection** to **Enabled**
9. Configure recovery key storage and backup options
10. Click **Next** and assign the profile to your test device group

---

## Lab 6: Set Up Windows Update Rings

**Objective**: Create update rings to manage Windows updates across device groups.

**Steps**:
1. Go to https://intune.microsoft.com and navigate to **Devices** > **Windows** > **Windows updates for business**
2. Click **+ Create profile** under **Update rings**
3. Name the profile "Update Ring - Early Adopters"
4. Configure the following update settings:
   - **Feature updates deferral**: 0 days
   - **Quality updates deferral**: 7 days
   - **Update deadline**: 30 days
5. Click **Next** and assign to your test device group
6. Click **Create** to finalize
7. Create a second update ring named "Update Ring - Standard"
8. For this ring, set Feature updates deferral to 30 days
9. Assign this ring to a different device group
10. Review and compare the two update rings in the Windows updates dashboard

---

## Lab 7: Configure Endpoint Protection

**Objective**: Deploy Defender Antivirus policies to protect against threats.

**Steps**:
1. Go to https://intune.microsoft.com and navigate to **Devices** > **Configuration profiles**
2. Click **+ Create profile**
3. Select **Windows 10 and later** and choose **Endpoint protection**
4. Name the profile "Endpoint Protection - Antivirus"
5. Scroll to **Windows Defender Antivirus** section and configure:
   - **Cloud protection**: Enabled
   - **Sample submission**: Enabled
   - **Real-time monitoring**: Enabled
   - **Potentially unwanted app protection**: Block
6. Set **Scan type** to **Quick scan**
7. Set **Scan frequency** to **Daily**
8. Click **Next** and assign to your test device group
9. Click **Create**
10. Monitor threat reports by going to **Devices** > **Monitor** > **Endpoint protection status**

---

## Lab 8: Manage Mobile Devices

**Objective**: Enroll and manage iOS and Android mobile devices.

**Steps**:
1. Go to https://intune.microsoft.com and navigate to **Devices** > **iOS/iPadOS** > **Enroll**
2. Review the iOS enrollment methods available
3. On an iOS device, open Safari and go to https://portal.manage.microsoft.com
4. Sign in with your Microsoft 365 account
5. Follow the enrollment prompts to install the Company Portal app
6. Complete the iOS enrollment process
7. Go back to Intune and navigate to **Devices** > **Android** > **Enroll**
8. On an Android device, open a browser and go to https://portal.manage.microsoft.com
9. Follow the enrollment prompts to install the Intune Company Portal
10. Complete Android enrollment and verify both devices appear in **All devices**

---

## Lab 9: Use Remote Actions

**Objective**: Execute remote actions on managed devices for troubleshooting and security.

**Steps**:
1. Go to https://intune.microsoft.com and navigate to **Devices** > **All devices**
2. Select a test device from your enrolled devices
3. Click **...** (more options) to see available remote actions
4. Click **Lock** to remotely lock the device
5. Verify the device is locked from the device itself
6. Go back and click **Unlock** to unlock the device
7. Use **Restart** to remotely restart the device
8. Click **Reset Passcode** to reset the device passcode
9. Navigate to **Devices** > **Audit logs** to review the remote actions performed
10. Document all remote actions taken and their timestamps from the audit log

---

## Lab 10: Monitor and Report on Devices

**Objective**: Generate and analyze device compliance and inventory reports.

**Steps**:
1. Go to https://intune.microsoft.com and navigate to **Devices** > **Monitor**
2. Click **Device compliance** to view compliance status across all devices
3. Review the compliance dashboard showing percentage of compliant devices
4. Click **Export** to download compliance data as a CSV file
5. Navigate to **Devices** > **Monitor** > **Device inventory**
6. Review device information including OS, manufacturer, and enrollment status
7. Go to **Reports** > **Device compliance** to generate detailed compliance reports
8. Run a report for the last 30 days
9. Click **Device health** to view device health trends
10. Create a summary document with key metrics: total devices, compliance rate, and top non-compliant issues
