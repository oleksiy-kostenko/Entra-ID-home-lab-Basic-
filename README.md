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


