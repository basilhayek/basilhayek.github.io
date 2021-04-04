---
title: Beacons and Adherence Part 2
description: Using Automate for Android to pretotype a medication adherence app that uses Bluetooth Low Energy (BLE) beacons to provide contextual reminders on taking medication
published: true
---
I used the word app in my previous post, but that's a bit grand. 

Rather, I'm going to be using a tool called Automate to create a pretotype of my adherence app.

I'm a big believer in pretotyping. It's a fast way to test out a concept. More than a few "AI-powered" products were [pretotypes powered by humans](https://www.theguardian.com/technology/2018/jul/06/artificial-intelligence-ai-humans-bots-tech-companies) working behind the scenes. 

I'll be using Automate's drag-and-drop flow builder to model my app's logic. My two key needs are the ability to detect Bluetooth Low Energy (BLE) beacons and trigger notifications in the Android notification drawer.
![A medication reminder notification with a pill emoji](https://cdn.basilhayek.com/07_ble_adherence_part_2/01_medication_reminder.png)
<!--excerpt-->

After experimenting with the different modes of my beacon, I opted to use iBeacon protocol, which broadcasts a universally unique idenfier (UUID) on a regular basis. I configured the beacon so that the UUID changes after I push the button on the beacon. This will be how I indicate that I have taken my medicine.

The high-level logic is:
1. Are we in the time window when I should be take my medicine? If not, wait until then
2. Is the regular UUID broadcasting? If so, use a notification to remind me to take my medicine. If the notification is dismissed, wait for 30 minutes before displaying the notification again
3. Is the button push UUID broadcasting? If so, clear any existing notifications, and (maybe) display a notification recognizing that I've take my medication. Then wait until tomorrow's time window. 

The reason that's a "maybe" around displaying a notification is I'm not sure I want to have to dismiss a notification each day after taking my medicine. I've already pushed the button. But if this was a real app, a variable message could help create that positive feedback loop. This is a feature I'd include in an SLC [(Simple, Lovable, Complete)](https://blog.asmartbear.com/slc.html) version, backed by user research of what customers would want to see and when, but for this proof-of-value version it's out-of-scope.

The result of turning the above three step flow into an Automate is below.
![A flowchart with logic for a Bluetooth Low Energy-based medication reminder app](https://cdn.basilhayek.com/07_ble_adherence_part_2/02_bt_adherence_flow.png)

It's basically ready to go, but of course next comes the testing.
