# Entra-ID-home-lab-Basic-




## 1. Creating users

**What I did:** I created 4 test users by hand, then added 15 more at once with a CSV import file using Bulk create.

**Why:** Creating a few by hand helped me understand how accounts are set up. When several people start at once, an import file is much quicker than adding them one by one.

<img width="1915" height="664" alt="{E9EC2B1F-FF5E-422E-AF9C-DBEB4088AB23}" src="https://github.com/user-attachments/assets/d776c88c-91e6-40b1-9e99-483005157345" />


**Result:** The Users list went from 5 accounts to 20: 19 test users and my original admin account.

Then I proceeded to create groups. The difference between Assigned and Dynamic User is quite simple: with Assigned, we add and remove users by hand. With Dynamic User, users are added and removed automatically, as long as their profile fits the group's rules (for example, their department). This cuts down on boring, repetitive work.

I used Assigned, because dynamic groups need a paid licence (Entra ID P1) and I'm using the free version.

Even though I haven't practised with dynamic groups, I've read extensively about them to learn how they work.
<img width="1466" height="913" alt="{88BB74F2-E719-4DCC-948F-CF95701F3DEB}" src="https://github.com/user-attachments/assets/77b70e63-b13d-46ac-8ded-c8cb3145d79e" />


I created 7 groups to match the 7 departments in my AD lab: Sales, Support, Operations, Finance, Marketing, HR and IT. I used the same names so both labs follow the same company structure, and it's easier to understand how they relate.

They are all security groups, which are normally used to control what people can access. Instead of giving access to each person one by one, you give it to the group, and its members get it.

This is preparation for connecting my AD to the cloud. These cloud groups won't be filled with my AD users automatically. When I sync my AD groups, they will show up as separate groups, which I will still manage in AD.
<img width="1673" height="798" alt="{D4700EFB-516F-4817-95A2-F6550DBFF10F}" src="https://github.com/user-attachments/assets/4f7bb866-3af6-4951-92d2-533b16a20635" />

Why connect AD to Entra ID?

The goal is one account for each person, for both the office network and the cloud.

Without sync, a new employee needs two separate accounts. When they leave, both have to be disabled, and if one is forgotten, they may still be able to get in.

With sync, the user is created once in AD and also appears in Entra ID. With password hash sync, they use the same password for both. If the account is disabled in AD, the cloud account gets disabled too after it syncs.

For synced users, AD is the main copy. Details like name, job title, department and synced group members are changed in AD. In Entra ID, I can still add them to cloud groups, check sign-in logs and assign admin roles. Microsoft 365 licences can also be assigned with a subscription.

This part is what I've learned so far. Syncing my AD is a later step in this lab.

After creating the groups and users, i wanted to practice bulk creating, and i'm using a csv file for that. For security reasons i won't show the original file, but i'll post an example of the original looks like.
<img width="899" height="473" alt="{4F606B16-2583-418C-8616-9C780C2115B7}" src="https://github.com/user-attachments/assets/d5da9a73-61d1-4437-898b-19fbfa802640" />

getting ready to import...

<img width="317" height="406" alt="{90F7E99F-2A75-4140-ACCC-C30CD554DCF8}" src="https://github.com/user-attachments/assets/85b45ac0-c3a1-4d0f-889d-db1f6d53c915" />

Result: all 20 new users appeared in Entra ID, bringing the list to 25 accounts, including my original admin account.
<img width="1919" height="859" alt="{2FC1B3DC-9999-4F23-A4C3-7B56E873DE69}" src="https://github.com/user-attachments/assets/6c50123d-a8dd-4150-b0d0-c747b311ffba" />

**Step 2: Creating an admin account**

**What I did:**
I created a separate cloud-only account called lab.admin and assigned it the Global Administrator role.

**Why:**
I didn't want to use my personal sign-up account for everyday admin work. A separate account keeps admin work apart from personal use. Microsoft also recommends cloud-only accounts for cloud admin roles, so a problem in a local AD doesn't reach them through sync.

**What for:**
To manage the lab, including users, groups, admin roles and security settings. My original account stays as a backup in case I can't get into lab.admin.

**Security note:**
Global Administrator has very broad control. In a real company, only a few people should have it, and other staff should get a role with only the access they need.

I use a separate admin account to keep admin work apart from my personal account. Global Administrator is very powerful, so it should be limited and protected with MFA.
<img width="986" height="857" alt="image" src="https://github.com/user-attachments/assets/8f0b3c54-a6e5-4dc0-b6a0-cd95c3f02ca3" />

I checked that security defaults were enabled. They require users to register for multifactor authentication (MFA), which adds a second step to protect accounts.
<img width="1919" height="868" alt="image" src="https://github.com/user-attachments/assets/ec845d74-88ac-4671-9e59-6ba0e0236b7b" />


Next up, setting up MFA for the admin global user.

When signing in with lab.admin, I was asked to change the password before continuing.
<img width="645" height="640" alt="image" src="https://github.com/user-attachments/assets/02b572b9-5b72-44fa-8cb3-de278cddcd98" />

Because security defaults were enabled, lab.admin was required to set up multifactor authentication (MFA).
<img width="1450" height="869" alt="{990E9FEF-2529-4515-8490-5BAC74654781}" src="https://github.com/user-attachments/assets/74fb6359-07ea-4d44-a44a-35f7096ca291" />

I set up Microsoft Authenticator for lab.admin, and it became the default sign-in method. This completed the MFA registration required by security defaults.

<img width="490" height="547" alt="image" src="https://github.com/user-attachments/assets/8dee98da-d77b-4c5d-a747-e17c6329baa4" />









