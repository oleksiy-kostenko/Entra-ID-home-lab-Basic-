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


