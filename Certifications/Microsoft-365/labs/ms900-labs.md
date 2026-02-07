# MS-900: Microsoft 365 Fundamentals Labs

This document contains hands-on labs for the MS-900 certification.

## Table of Contents
1. [Lab 1: Explore Microsoft 365 Admin Center](#lab-1-explore-microsoft-365-admin-center)
2. [Lab 2: Configure Security Defaults](#lab-2-configure-security-defaults)
3. [Lab 3: Assign Microsoft 365 Licenses](#lab-3-assign-microsoft-365-licenses)
4. [Lab 4: Explore Microsoft 365 Apps](#lab-4-explore-microsoft-365-apps)
5. [Lab 5: Set Up Microsoft Teams](#lab-5-set-up-microsoft-teams)
6. [Lab 6: Configure Exchange Online Mailboxes](#lab-6-configure-exchange-online-mailboxes)
7. [Lab 7: Use OneDrive for Business](#lab-7-use-onedrive-for-business)
8. [Lab 8: Explore Compliance Center](#lab-8-explore-compliance-center)
9. [Lab 9: Set Up Conditional Access](#lab-9-set-up-conditional-access)
10. [Lab 10: Explore Microsoft 365 Security Center](#lab-10-explore-microsoft-365-security-center)

---

## Lab 1: Explore Microsoft 365 Admin Center

**Objective**: Understand the Microsoft 365 Admin Center interface and key management functions.

**Steps**:
1. Go to https://admin.microsoft.com and sign in with your Microsoft 365 admin account
2. Review the Home dashboard and familiarize yourself with the navigation menu on the left
3. Click **Users** > **Active users** to view all users in your organization
4. Click **Billing** > **Licenses** to see your subscription details
5. Click **Health** > **Service health** to check the status of Microsoft 365 services
6. Navigate to **Settings** > **Organization settings** to review tenant configuration
7. Document three key metrics you find on the Home dashboard

---

## Lab 2: Configure Security Defaults

**Objective**: Enable and test multi-factor authentication using Security Defaults.

**Steps**:
1. Go to https://admin.microsoft.com and navigate to **Azure Active Directory** > **Properties**
2. Click on **Manage security defaults**
3. Read the overview of what security defaults provide
4. Toggle **Enable security defaults** to **On**
5. Click **Save** to apply the policy
6. Sign out and sign back in from a private/incognito window
7. You will be prompted to set up MFA—follow the wizard to add an authenticator app or phone number
8. Complete the MFA setup and verify you can successfully re-authenticate
9. Test accessing Microsoft 365 apps (Word Online, Teams, etc.) with MFA enabled

---

## Lab 3: Assign Microsoft 365 Licenses

**Objective**: Assign and manage Microsoft 365 licenses for users.

**Steps**:
1. Go to https://admin.microsoft.com and navigate to **Users** > **Active users**
2. Select a test user from the list
3. In the user details pane, click the **Licenses and apps** tab
4. Click **Manage product licenses**
5. Toggle on a Microsoft 365 product license (e.g., Microsoft 365 Business Standard)
6. Deselect any unwanted services and click **Save changes**
7. Go back and select a second user
8. Assign a different license product to this user
9. Verify both users have their licenses in the Active users list
10. Remove the license from one user and confirm it's no longer assigned

---

## Lab 4: Explore Microsoft 365 Apps

**Objective**: Access and collaborate using Office 365 web applications.

**Steps**:
1. Go to https://www.office.com and sign in
2. Click on **Word** to open Word Online
3. Create a new blank document and type some content
4. Click **Share** and invite a colleague to collaborate
5. Open **Excel** and create a simple spreadsheet with sample data
6. Add a chart to your spreadsheet
7. Open **PowerPoint** and create a slide with a title and bullet points
8. Go back to office.com and open **OneDrive**
9. Upload a document from your computer
10. Create a folder named "Shared Docs" and move your uploaded file into it

---

## Lab 5: Set Up Microsoft Teams

**Objective**: Create and configure a Teams environment with channels and members.

**Steps**:
1. Go to https://teams.microsoft.com and sign in
2. Click **+ Create or join a team**
3. Select **Create a team** and choose **From scratch**
4. Select **Private** as the team type
5. Name your team (e.g., "Training Team") and add a description
6. Click **Create**
7. Once created, you should see a **General** channel
8. Click **+ Add channel** to create a new channel (e.g., "Announcements")
9. Add a second channel (e.g., "Resources")
10. Click **Manage team** and then **Members** to invite other users to the team

---

## Lab 6: Configure Exchange Online Mailboxes

**Objective**: Create and manage different types of mailboxes in Exchange Online.

**Steps**:
1. Go to https://admin.microsoft.com and navigate to **Users** > **Active users**
2. Click **+ Add user** to create a new test user
3. Fill in the user details and assign a license
4. After the user is created, go to **Exchange admin center** (via the settings menu)
5. Navigate to **Recipients** > **Mailboxes**
6. Verify the new user mailbox appears in the list
7. Click **+ Add mailbox** and create a **Shared mailbox** named "Department Inbox"
8. Assign permissions to the shared mailbox for your new user
9. Click on the shared mailbox and verify the **Members** tab shows the assigned user
10. Go back to the user mailbox and configure **Forwarding** to forward to the shared mailbox

---

## Lab 7: Use OneDrive for Business

**Objective**: Upload, share, and manage files in OneDrive for Business.

**Steps**:
1. Go to https://office.com and click on **OneDrive**
2. Click **+ New** and select **Folder** to create a new folder named "Project Files"
3. Click **Upload** and select a document from your computer
4. Right-click the uploaded file and select **Share**
5. Choose **Specific people** and enter a colleague's email address
6. Set permissions to **Edit** and click **Share**
7. The recipient should receive an email notification
8. Click on the uploaded file to open it in the web preview
9. In the file menu, click **Version history** to view file versions
10. Make a change to the document, save it, and verify a new version appears in the history

---

## Lab 8: Explore Compliance Center

**Objective**: Understand compliance features and assess your organization's compliance posture.

**Steps**:
1. Go to https://compliance.microsoft.com and sign in
2. Click on **Compliance Manager** in the left navigation
3. Review the overall compliance score displayed on the dashboard
4. Click on a recommendation to view details and improvement actions
5. Look at the **Assessment** tab to see your organization's compliance across different standards
6. Click **+ Add assessment** to see available compliance frameworks (e.g., ISO 27001, HIPAA)
7. Go to **Data retention** policies and review any existing retention rules
8. Document three ways you can improve your compliance score
9. Check the **Alerts** page for any compliance-related notifications
10. Review the **Reports** to understand your compliance metrics

---

## Lab 9: Set Up Conditional Access

**Objective**: Create a basic conditional access policy to control access based on specific conditions.

**Steps**:
1. Go to https://admin.microsoft.com and navigate to **Azure Active Directory** > **Security** > **Conditional Access**
2. Click **+ Create new policy**
3. Name the policy "Test Conditional Access Policy"
4. Under **Assignments**, click **Users or workload identities**
5. Select **Specific users** and choose a test user
6. Click **Cloud apps or actions** and select **Office 365 Exchange Online**
7. Under **Conditions**, click **Add condition** and select **Device platforms**
8. Choose **Windows** as the device platform
9. Under **Access controls** > **Grant**, select **Require multi-factor authentication**
10. Set the policy to **Report-only** mode and click **Create**

---

## Lab 10: Explore Microsoft 365 Security Center

**Objective**: Review security features and threat protection capabilities.

**Steps**:
1. Go to https://security.microsoft.com and sign in
2. Review the main dashboard to see security status overview
3. Click on **Incidents** to view any security incidents
4. Look at **Alerts** to see recent security alerts
5. Navigate to **Secure Score** to see your organization's security score
6. Click on a security recommendation to understand improvement actions
7. Go to **Email & collaboration** > **Policies & rules** to review threat protection policies
8. Check **Reports** > **Email security** to view email threat reports
9. Review **Advanced hunting** to understand query capabilities
10. Document your organization's current Secure Score and three top improvement areas
