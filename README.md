# Microsoft Entra ID Home Lab

### CompTIA A+ · Aspiring IT Helpdesk / Service Desk (L1)

Hi, I'm **Oleksiy Kostenko**. This is the cloud side of my [Active Directory home lab](https://github.com/oleksiy-kostenko/ad-lab). I'm using the free version of Microsoft Entra ID to practise managing users, groups and sign-in security. Later, I'll connect the two labs.

## What I've done so far(in progress)

| Task | What I did |
|---|---|
| **Create users** | 4 by hand, then 20 at once with a CSV file |
| **Create groups** | 7 security groups, matching the departments in my AD lab |
| **Separate admin work** | Created a cloud-only admin account |
| **Secure sign-in** | Checked security defaults and set up MFA for the admin account |

**Jump to:** [Users](#1-creating-users) · [Groups](#2-creating-groups) · [Admin account](#3-creating-an-admin-account) · [Security and MFA](#4-security-defaults-and-mfa) · [What's next](#whats-next)

## 1. Creating users

I started off by creating 4 test users by hand, to understand how accounts are set up. The fifth account in the list is my original admin account.

<img width="1915" height="622" alt="1-first-users" src="https://github.com/user-attachments/assets/6b4099f5-93b0-43a7-848e-803031e52e65" />


Next, I practised bulk creating with a CSV file. When several people start at once, this is much quicker than adding them one by one. 

For security reasons I won't show the original file. This is an example copy of it, with an example domain and hidden passwords:

<img width="750" alt="Example copy of the CSV file with 20 users, an example domain and hidden passwords" src="https://github.com/user-attachments/assets/d5da9a73-61d1-4437-898b-19fbfa802640" />

Uploading the file:

<img width="317" height="394" alt="2-bulk-upload" src="https://github.com/user-attachments/assets/081bad91-4042-4639-8574-f7b6b1ffae04" />


**Result:** all 20 new users appeared in Entra ID, bringing the list to 25 accounts, including my original admin account.

<img width="750" alt="Users list showing 25 users found" src="https://github.com/user-attachments/assets/6c50123d-a8dd-4150-b0d0-c747b311ffba" />

## 2. Creating groups

The difference between Assigned and Dynamic User is quite simple: with Assigned, we add and remove users by hand. With Dynamic User, users are added and removed automatically, as long as their profile fits the group's rules (for example, their department). This cuts down on boring, repetitive work.

I used Assigned, because dynamic groups need a paid licence (Entra ID P1) and I'm using the free version. Even though I haven't practised with dynamic groups, I've read extensively about them to learn how they work.

<img width="750" alt="New group screen showing the Assigned and Dynamic membership types" src="https://github.com/user-attachments/assets/77b70e63-b13d-46ac-8ded-c8cb3145d79e" />

I created 7 groups to match the 7 departments in my AD lab: Sales, Support, Operations, Finance, Marketing, HR and IT. I used the same names so both labs follow the same company structure, and it's easier to understand how they relate.

They are all security groups, which are normally used to control what people can access. Instead of giving access to each person one by one, you give it to the group, and its members get it.

<img width="750" alt="List of 7 security groups with assigned membership" src="https://github.com/user-attachments/assets/4f7bb866-3af6-4951-92d2-533b16a20635" />

## 3. Creating an admin account

**What I did:** I created a separate cloud-only account called `lab.admin` and assigned it the Global Administrator role.

**Why:** I didn't want to use my personal sign-up account for everyday admin work. Microsoft also recommends cloud-only accounts for cloud admin roles, so a problem in a local AD doesn't reach them through sync.

**What for:** To manage the lab, including users, groups, admin roles and security settings. My original account stays as a backup in case I can't get into `lab.admin`.

**Security note:** Global Administrator has very broad control, so it should be protected with MFA. In a real company, only a few people should have it, and other staff should get a role with only the access they need.

<img width="750" alt="Creating lab.admin with the Global Administrator role" src="https://github.com/user-attachments/assets/8f0b3c54-a6e5-4dc0-b6a0-cd95c3f02ca3" />

## 4. Security defaults and MFA

I checked that security defaults were enabled. They require users to register for multifactor authentication (MFA), which adds a second step to protect accounts.

<img width="750" alt="Security defaults set to Enabled" src="https://github.com/user-attachments/assets/ec845d74-88ac-4671-9e59-6ba0e0236b7b" />

When signing in with `lab.admin` for the first time, I was asked to change the password before continuing.

<img width="420" alt="lab.admin asked to update the password at first sign-in" src="https://github.com/user-attachments/assets/02b572b9-5b72-44fa-8cb3-de278cddcd98" />

Because security defaults were enabled, `lab.admin` was then required to set up MFA.

<img width="490" height="477" alt="3-mfa-required" src="https://github.com/user-attachments/assets/d29f6e69-6b94-4761-9f24-3f1107860f64" />


I set up Microsoft Authenticator, and it became the default sign-in method. This completed the MFA registration.

<img width="350" alt="Microsoft Authenticator added for lab.admin" src="https://github.com/user-attachments/assets/8dee98da-d77b-4c5d-a747-e17c6329baa4" />

## Why connect AD to Entra ID?

The goal is one account for each person, for both the office network and the cloud.

- **Without sync,** a new employee needs two separate accounts. When they leave, both have to be disabled. If one is forgotten, they may still be able to get in.
- **With sync,** the user is created once in AD and also appears in Entra ID. With password hash sync, they use the same password for both. If the account is disabled in AD, the cloud account gets disabled too after it syncs.

For synced users, AD is the main copy. Details like name, job title, department and synced group members are changed in AD. In Entra ID, they can still be added to cloud groups and given admin roles, and their sign-in logs can be checked. Microsoft 365 licences can also be assigned with a subscription.

The cloud groups I made won't be filled with my AD users automatically. Synced AD groups show up as separate groups, which are still managed in AD.

This part is what I've learned so far. Syncing my AD is a later step in this lab.

## What's next

- Connect my AD lab to Entra ID with Cloud Sync, starting with the IT users in Europe
- Practise helpdesk tasks: password resets, offboarding, restoring users and checking sign-in logs
- Test what a Helpdesk Administrator can and can't do
- Practise Microsoft 365: licences, mailboxes and Teams


I added the Hybrid Identity Administrator role to lab.admin to prepare for connecting my AD with Cloud Sync.
<img width="1910" height="779" alt="{285D83EB-931E-497A-AC9F-2462368EDDFB}" src="https://github.com/user-attachments/assets/85f2ea45-8e2d-42b7-8236-33a4a8dad9f2" />

<img width="1910" height="779" alt="{285D83EB-931E-497A-AC9F-2462368EDDFB}" src="https://github.com/user-attachments/assets/b362a317-6148-4e09-97d3-847598c69388" />

Before syncing: I signed in to Entra ID from my domain controller as lab.admin. This also confirms that the admin account I set up works, and that it has the Global Administrator role. At this point, the directory had 26 users and 7 groups.

<img width="1025" height="769" alt="image" src="https://github.com/user-attachments/assets/429af51a-0f73-430a-a2d4-7f4ecd646d54" />

Step: Downloading the Cloud Sync agent

What I did: On my domain controller, I went to Cloud Sync in Entra ID to download the provisioning agent.

Why: The agent is the link between my local Active Directory and Entra ID. It's needed before I can sync my users to the cloud. At this point, no agents were registered yet.

<img width="1025" height="769" alt="image" src="https://github.com/user-attachments/assets/14764cef-be60-4a03-82ca-3864cc6b60c3" />


## Setting up the Cloud Sync agent

The agent is the link between my local Active Directory and Entra ID. I installed it on my domain controller (DC01), and during setup it asked for a service account.

**What's a service account?**
It's an account used by a program, not a person.

**What's a gMSA?**
A group Managed Service Account (gMSA) is a special type of service account. Windows creates and changes its password automatically, so I don't have to manage it myself.

**What I did:** I chose "Create gMSA" in the setup wizard. Creating it needs domain admin permission.

**The accounts involved:**

| Account | What it's for |
|---|---|
| lab.admin | Signing in to Entra ID during setup |
| Domain Administrator | Giving permission to create the gMSA in AD |
| gMSA | The account the agent runs under |

This was part of setting up the agent. It doesn't start syncing users yet.
<img width="1642" height="959" alt="{EF497782-AA09-40D6-BDCD-7843E492EE22}" src="https://github.com/user-attachments/assets/32fff42c-53ec-42a3-b959-6b0d8937ee2a" />

<img width="1133" height="814" alt="{750C919C-1009-40E6-89EB-1F493714B40E}" src="https://github.com/user-attachments/assets/d9f0dd3e-10d9-4281-b1f2-20def780e637" />

<img width="815" height="290" alt="{512CFF4F-31C5-4E91-B9DA-1DE176BE6DA4}" src="https://github.com/user-attachments/assets/f9663795-983d-4e08-97a0-3da5c029ead0" />
## Troubleshooting: Cloud Sync agent registration (not resolved yet)

**Problem:** The agent setup created the gMSA, but failed when registering with Microsoft: "Connector registration failed".

**What was checked (with AI help):**
- The registration address resolved in DNS.
- DC01 could connect to it on port 443.
- Event Viewer showed a more detailed error: "There was no endpoint listening" at the registration address.
- The same error was publicly reported on 21 November 2026. There was no confirmed fix when it was checked on 28 November 2026.

**Status:** The cause is still unknown and sync is not set up yet.

I used AI to help troubleshoot. It guided the checks, ran the final connection tests and log searches on DC01, and helped explain the results.

