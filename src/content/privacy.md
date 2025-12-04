# Privacy Policy

**Last Updated:** December 4, 2024
**Effective Date:** December 4, 2024
**Version:** 1.0

---

## Introduction

Welcome to Subscripto. We are committed to protecting your privacy and being transparent about how we collect, use, and safeguard your information. This Privacy Policy explains our practices regarding your data when you use the Subscripto mobile application ("App").

Subscripto is designed to help families and households track, manage, and optimize their subscription services. We believe in putting you in control of your data while providing the best possible experience.

## Information We Collect

### Information You Provide Directly

**Subscription Data:**
- Subscription service names (e.g., Netflix, Spotify)
- Cost and billing amounts
- Billing frequency (monthly, yearly, etc.)
- Renewal dates and payment dates
- Categories (Streaming, Music, Software, etc.)
- Custom notes or descriptions

**Household Information:**
- Household name
- Family member profiles (names, avatars, display colors)
- Subscription ownership assignments
- Usage tracking (which members use which subscriptions)
- Cost splitting preferences

**Account Information:**
- Email address (optional, only if you choose to create an account)
- Authentication credentials (managed securely by Supabase)

### Automatically Collected Information

**Device Information:**
- Push notification tokens (for renewal reminders)
- Device type and operating system
- App version and build number

**Usage Information:**
- App interaction data (which features you use)
- Crash reports and error logs (to improve app stability)

### Optional Features

**Email Scanning (Opt-in Only):**
If you choose to enable automatic subscription detection via email scanning:
- We request read-only access to your Gmail or Outlook account via OAuth 2.0
- We scan emails for subscription receipts and billing notifications
- **We never store your emails or access your email password**
- You can revoke this access at any time through your Google/Microsoft account settings

## How We Use Your Information

We use your information to:

1. **Provide Core Functionality**
   - Display and organize your subscription data
   - Calculate household spending totals
   - Send renewal reminder notifications
   - Sync data across your family's devices

2. **Improve User Experience**
   - Detect duplicate subscriptions across household members
   - Provide spending insights and analytics
   - Suggest cost-saving opportunities
   - Calculate fair cost splits among family members

3. **Maintain Service Quality**
   - Fix bugs and improve app performance
   - Develop new features based on user needs
   - Ensure data security and prevent abuse

4. **Communication**
   - Send important service updates
   - Respond to your support requests
   - Notify you about changes to our policies

## Data Storage and Security

### Where Your Data is Stored

Your subscription data is stored on **Supabase** (a secure PostgreSQL database hosted on AWS):
- **Data Location:** United States (AWS us-east-1 region)
- **Encryption:** All data is encrypted at rest using AES-256
- **In Transit:** All data transmission uses HTTPS/TLS 1.3
- **Backups:** Automated daily backups with encryption

### Security Measures

We implement industry-standard security practices:
- **Row-Level Security:** Your household data is isolated from other users
- **Secure Authentication:** OAuth 2.0 and secure token management
- **Limited Access:** Only essential app functionality can access your data
- **No Third-Party Sharing:** We do not sell or share your data with advertisers

### Data Retention

- **Active Accounts:** Your data is retained as long as your account is active
- **Deleted Accounts:** All data is permanently deleted within 30 days of account deletion
- **Backups:** Deleted data is removed from backups within 90 days

## Family and Household Sharing

### How Household Sharing Works

When you create or join a household:
- **Shared Data:** Subscription information, household member profiles, and spending insights are visible to all household members
- **Admin Controls:** Household creators/admins can invite members, manage permissions, and delete the household
- **Member Privacy:** Each member controls their own profile information
- **Leaving:** Any member can leave a household at any time

### What Household Members Can See

All household members can view:
- List of all subscriptions tracked by the household
- Who owns each subscription
- Who uses each subscription
- Total household spending
- Cost split calculations

Household members **cannot** see:
- Other members' email addresses (unless shared separately)
- Payment method details
- Individual spending outside the household

## Email Scanning Privacy (Optional Feature)

If you enable email-based subscription detection:

**What We Access:**
- We use **OAuth 2.0** (no password storage) to read emails
- We only scan for subscription-related emails (receipts, billing notifications)
- We extract subscription information (service name, cost, date)

**What We Do NOT Do:**
- Store your emails on our servers
- Read personal or non-subscription emails
- Share your email content with anyone
- Use AI/ML on your email content beyond subscription detection

**Your Control:**
- You can disable email scanning anytime in app settings
- Revoke access via [Google Account Settings](https://myaccount.google.com/permissions) or [Microsoft Account Settings](https://account.microsoft.com/privacy)
- Previously detected subscriptions remain unless you delete them

## Third-Party Services

We use the following trusted third-party services:

**Supabase (Database & Authentication):**
- Purpose: Store subscription data, manage user authentication, real-time sync
- Data Shared: Subscription data, account credentials (hashed), household information
- Privacy Policy: [https://supabase.com/privacy](https://supabase.com/privacy)

**Apple Push Notification Service (APNs):**
- Purpose: Send renewal reminders on iOS
- Data Shared: Device push tokens, notification content
- Privacy Policy: [https://www.apple.com/legal/privacy/](https://www.apple.com/legal/privacy/)

**Firebase Cloud Messaging (FCM):**
- Purpose: Send renewal reminders on Android
- Data Shared: Device push tokens, notification content
- Privacy Policy: [https://policies.google.com/privacy](https://policies.google.com/privacy)

We do **not** use:
- Third-party analytics (Google Analytics, Mixpanel, etc.)
- Advertising networks or trackers
- Data brokers or marketing platforms

## Your Privacy Rights

You have the following rights regarding your data:

### Access and Export
- View all your subscription data in the app
- Export your data in CSV format (coming soon)

### Correction
- Edit or update any subscription information
- Modify your profile details

### Deletion
- Delete individual subscriptions
- Delete your entire account and all associated data
- Leave or delete households you've created

### Opt-Out
- Disable push notifications in app settings
- Revoke email scanning access
- Opt out of optional features

### Portability
- Export your data for use in other apps (CSV format)

To exercise these rights, contact us at **privacy@subscripto.io**.

## Children's Privacy

Subscripto is **not intended for children under 13 years old**. We do not knowingly collect personal information from children under 13.

- If you are under 13, please do not use Subscripto
- If you are 13-17, you must have parental consent to use the app
- Parents can create household accounts and add family members of appropriate age

If we discover we have collected data from a child under 13, we will delete it immediately. If you believe we have inadvertently collected such data, contact us at **privacy@subscripto.io**.

## International Users

Subscripto is operated from the United States, and your data is stored on servers located in the United States (AWS us-east-1).

**For EU/EEA Users (GDPR):**
- We comply with GDPR requirements
- You have the right to access, rectify, erase, and port your data
- You can withdraw consent for data processing at any time
- You can lodge a complaint with your local data protection authority

**For California Users (CCPA):**
- We do not sell your personal information
- You have the right to know what data we collect and how we use it
- You can request deletion of your personal information

## Data Breach Notification

In the unlikely event of a data breach that affects your personal information:
- We will notify you via email within 72 hours of discovering the breach
- We will explain what data was affected and what actions we are taking
- We will provide guidance on steps you can take to protect yourself

## Changes to This Privacy Policy

We may update this Privacy Policy from time to time to reflect:
- Changes in our data practices
- New features or services
- Legal or regulatory requirements

**How We Notify You:**
- Significant changes: Email notification and in-app alert
- Minor changes: Updated "Last Updated" date at the top of this policy

**Your Continued Use:**
- By continuing to use Subscripto after changes take effect, you accept the updated Privacy Policy
- If you disagree with changes, you may delete your account

## Contact Us

If you have questions, concerns, or requests regarding this Privacy Policy or your data:

**Email:** privacy@subscripto.io
**Website:** https://subscripto.io
**Response Time:** We aim to respond within 7 business days

For general support inquiries:
**Email:** hello@subscripto.io

## Legal Compliance

This Privacy Policy is governed by the laws of the United States and the state in which Subscripto operates. We comply with:
- General Data Protection Regulation (GDPR)
- California Consumer Privacy Act (CCPA)
- Children's Online Privacy Protection Act (COPPA)
- CAN-SPAM Act
- Other applicable privacy and data protection laws

---

**Subscripto Privacy Policy v1.0**
**Effective:** December 4, 2024
**Last Updated:** December 4, 2024
