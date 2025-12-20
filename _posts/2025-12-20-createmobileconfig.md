---
title: "Create and deploy a macOS configuration file (.mobileconfig)"
date: 2025-12-20 22:10:00 +0100
categories: [Guides]
tags: [macOS]
---

This post covers a workflow to:

1. Create a macOS configuration profile (`.mobileconfig`) with **iMazing Profile Editor**.
2. Deploy it using an MDM (Microsoft Intune in this example).

The steps are general and work for many app config payloads. I’ll use **DDM OS Reminder** as the running example.

## What you’ll need

- A Mac
- **iMazing Profile Editor**
- Admin access to **Microsoft Intune** (or another MDM)

## 1. Install iMazing Profile Editor

iMazing Profile Editor is an easy way to create and edit `.mobileconfig` files. It uses an fork of the [ProfileManifest](https://github.com/DigiDNA/ProfileManifests) repo to provide a UI for many macOS config payloads.

- Direct Download: https://imazing.com/profile-editor/download
- App Store Download: https://apps.apple.com/se/app/imazing-profile-editor/id1487860882

## 2. Add a payload

In iMazing Profile Editor, a *payload* is the set of configuration keys for a specific feature or app.

Example (DDM OS Reminder):

1. Open **iMazing Profile Editor**.
2. Scroll until you find **DDM OS Reminder**.
3. Select it and click **+ Add Payload**.

## 3. Configure the payload

Configure the keys you care about for the payload you added.

For the running example (DDM OS Reminder): all keys are optional, if you leave a value empty, the default value is used.

Tip: hover over the **?** next to each key to see details and the default value.

## 4. Save the profile

Save the `.mobileconfig` via the top menu.

You do **not** need to sign the profile if you intend to upload it using an MDM.

## 5. Deploy the profile via Intune

1. In Intune, go to **Devices** → **macOS** → **Configuration**.
2. Click **Create** → **New policy**.
3. Under **Profile type**, select **Templates**.
4. Select **Custom**.
5. Set an **Intune policy display name** (shown in Intune), then click **Next**.
6. Set a **Custom configuration profile name** (shown locally under **System Settings** → **Device Management**).
7. Leave the deployment channel as **Device Channel**.
8. Upload the `.mobileconfig` you created.
9. Click **Next**, choose your **assignment groups**, and finish the policy.

The deployment flow is similar in other MDM solutions: create a custom profile policy, upload the `.mobileconfig`, then assign it to devices (or users, if your payload supports it).
