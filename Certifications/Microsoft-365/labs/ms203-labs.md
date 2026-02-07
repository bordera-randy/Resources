# MS-203: Messaging Administrator Labs

This document contains hands-on labs for the MS-203 certification.

## Table of Contents
1. [Lab 1: Create and Manage Mailboxes](#lab-1-create-and-manage-mailboxes)
2. [Lab 2: Configure Anti-Phishing Policies](#lab-2-configure-anti-phishing-policies)
3. [Lab 3: Manage Distribution Groups](#lab-3-manage-distribution-groups)
4. [Lab 4: Set Up Email Flow Rules](#lab-4-set-up-email-flow-rules)
5. [Lab 5: Configure Retention Policies](#lab-5-configure-retention-policies)
6. [Lab 6: Enable Litigation Hold](#lab-6-enable-litigation-hold)
7. [Lab 7: Manage Mobile Device Access](#lab-7-manage-mobile-device-access)
8. [Lab 8: Monitor Message Trace](#lab-8-monitor-message-trace)
9. [Lab 9: Set Up Shared Mailboxes](#lab-9-set-up-shared-mailboxes)
10. [Lab 10: Configure Outbound Spam Policies](#lab-10-configure-outbound-spam-policies)

---

## Lab 1: Create and Manage Mailboxes

**Objective**: Create and configure user and shared mailboxes in Exchange Online.

**Steps**:
1. Go to https://admin.microsoft.com and navigate to **Users** > **Active users**
2. Click **+ Add a user** to create a new user mailbox
3. Fill in user information (name, email, password)
4. Assign an Exchange license and click **Finish**
5. Go to https://admin.exchange.microsoft.com and navigate to **Recipients** > **Mailboxes**
6. Verify the new user mailbox appears in the list
7. Click **+ Add a shared mailbox** to create a shared mailbox
8. Name the shared mailbox (e.g., "Support Team Inbox")
9. Assign owners and members to the shared mailbox
10. Send a test email to the shared mailbox and verify all members can access it

---

## Lab 2: Configure Anti-Phishing Policies

**Objective**: Set up anti-phishing policies in Microsoft Defender for Office 365.

**Steps**:
1. Go to https://security.microsoft.com and navigate to **Email & collaboration** > **Policies & rules** > **Threat policies**
2. Click **Anti-phishing** under Threat protection policies
3. Click **+ Create** to create a new anti-phishing policy
4. Name the policy "Anti-Phishing Policy - Standard"
5. Configure the following settings:
   - **Phishing threshold**: Aggressive (level 3 or 4)
   - **Enable spoof intelligence**: On
   - **User impersonation protection**: Enabled
   - **Domain impersonation protection**: Enabled
6. Under **If the message is detected as phishing**, select **Quarantine the message**
7. Configure user settings and click **Next**
8. Select recipients or groups to apply the policy
9. Click **Create** to save the policy
10. Test the policy by sending a simulated phishing email and verify it's detected

---

## Lab 3: Manage Distribution Groups

**Objective**: Create and manage distribution groups with membership controls.

**Steps**:
1. Go to https://admin.exchange.microsoft.com and navigate to **Recipients** > **Groups**
2. Click **+ Add a group** and select **Distribution**
3. Name the group "Engineering Team"
4. Add an email address for the group
5. Add group owners (approvers) and members
6. Enable **Require all senders to be authenticated before sending to this group**
7. Set **Who can send emails to this group** to **Only senders inside my organization**
8. Click **Create**
9. To manage membership, click on the group and select **Members**
10. Add additional members and remove test members to understand group management

---

## Lab 4: Set Up Email Flow Rules

**Objective**: Create transport rules to manage email flow and compliance.

**Steps**:
1. Go to https://admin.exchange.microsoft.com and navigate to **Mail flow** > **Rules**
2. Click **+ Add a rule** and select **Create a new rule**
3. Name the rule "Compliance Rule - External Email Disclaimer"
4. Under **Apply this rule if**, select **The recipient is located**
5. Choose **Outside the organization**
6. Under **Do the following**, select **Prepend the subject with**
7. Enter text: "[EXTERNAL EMAIL]"
8. Click **Next** and review the rule configuration
9. Create a second rule to **Redirect messages** with specific keywords to a compliance mailbox
10. Test both rules by sending emails and verify they behave as expected

---

## Lab 5: Configure Retention Policies

**Objective**: Create and apply retention policies to control how long emails are kept.

**Steps**:
1. Go to https://compliance.microsoft.com and navigate to **Data lifecycle management** > **Retention**
2. Click **+ Create retention label** to create a retention tag
3. Name the label "Archive After 1 Year"
4. Set the retention period to **1 year**
5. Configure the action as **Delete the content**
6. Click **Create**
7. Go back and click **+ Create retention policy**
8. Name the policy "Default Retention Policy"
9. Configure to apply the retention label automatically
10. Select mailboxes to apply the policy and click **Create**

---

## Lab 6: Enable Litigation Hold

**Objective**: Place a mailbox on litigation hold to preserve content.

**Steps**:
1. Go to https://admin.exchange.microsoft.com and navigate to **Recipients** > **Mailboxes**
2. Select a test user mailbox
3. In the mailbox details, find the **Litigation Hold** option
4. Toggle **Litigation Hold** to **Enabled**
5. Set the hold duration (e.g., 365 days)
6. Click **Save**
7. Verify the hold is applied by checking the mailbox status
8. With litigation hold enabled, delete an email from the mailbox
9. Go to **Search** in compliance.microsoft.com and search for the deleted email
10. Verify the deleted email appears in search results (it's being held)

---

## Lab 7: Manage Mobile Device Access

**Objective**: Configure mobile device mailbox policies.

**Steps**:
1. Go to https://admin.exchange.microsoft.com and navigate to **Mobile** > **Mobile device mailbox policies**
2. Click **+ Add policy**
3. Name the policy "Mobile Device Policy - Secure"
4. Configure the following security settings:
   - **Require a password**: Yes
   - **Allow simple passwords**: No
   - **Minimum password length**: 8
   - **Enable device encryption**: Yes
   - **Require encrypted S/MIME messages**: Yes
5. Set **Device password expiration**: 60 days
6. Under **Device access rules**, select **Block** for non-compliant devices
7. Click **Create**
8. Assign the policy to a test user mailbox
9. Send a test access notification to the user
10. Review the mobile device compliance status

---

## Lab 8: Monitor Message Trace

**Objective**: Use message trace to troubleshoot mail flow issues.

**Steps**:
1. Go to https://admin.exchange.microsoft.com and navigate to **Mail flow** > **Message trace**
2. Enter a sender email address in the **Sender** field
3. Enter a recipient email address in the **Recipient** field
4. Set the date range to the last 7 days
5. Click **Search**
6. Review the trace results showing the message path
7. Click on a message to view detailed trace information including status, event, and action
8. Send a test email to troubleshoot and then trace it
9. Look for any delivery issues or delays in the trace
10. Document the complete message journey from sender to recipient

---

## Lab 9: Set Up Shared Mailboxes

**Objective**: Create shared mailboxes and configure access permissions.

**Steps**:
1. Go to https://admin.exchange.microsoft.com and navigate to **Recipients** > **Shared mailboxes**
2. Click **+ Add a shared mailbox**
3. Name the mailbox "HR Support"
4. Add an email address
5. Assign multiple users as owners
6. Add team members who should have access
7. Click **Create**
8. Go to https://outlook.office.com and add the shared mailbox to your Outlook
9. Access the shared mailbox and send/read emails from it
10. Go back to the admin center and verify all users can access the shared mailbox

---

## Lab 10: Configure Outbound Spam Policies

**Objective**: Set up policies to manage outbound spam and protect against abuse.

**Steps**:
1. Go to https://security.microsoft.com and navigate to **Email & collaboration** > **Threat policies** > **Outbound spam**
2. Review the default outbound spam policy
3. Click **+ Create policy**
4. Name the policy "Outbound Spam Policy - Strict"
5. Configure the following settings:
   - **Outbound spam filter policy**: Enabled
   - **Recipient rate limit**: Limit to 500 recipients per hour
   - **Daily message limit**: 1000 messages per day
   - **Alert admins**: Yes
   - **Alert users**: Yes
6. Set actions for suspicious outbound emails to **Restrict user ability to send until it is reviewed**
7. Click **Create**
8. Send a bulk test email to monitor policy enforcement
9. Check **Email & collaboration** > **Reports** > **Outbound spam** for outbound protection reports
10. Review quarantined outbound emails and remediate if necessary
