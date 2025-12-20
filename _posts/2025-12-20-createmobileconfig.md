---
title: "Create and deploy a macOS configuration file (.mobileconfig)"
date: 2025-12-20 22:10:00 +0100
categories: [Guides]
tags: [macOS]
---

This post covers a workflow to:

1. Create a macOS configuration profile (`.mobileconfig`) with **iMazing Profile Editor**.
2. Deploy it using an MDM (**Microsoft Intune** in this example).

The steps are general and will work for many different apps and system features. I will use **DDM OS Reminder** as the running example.

## What is a `.mobileconfig`?

A `.mobileconfig` is an Apple **configuration profile** used to configure settings on macOS (and other Apple platforms). Internally, it’s a **property list (plist)** document that contains one or more payloads.

Each payload is a plist dictionary of keys/values, and the profile is wrapped with metadata such as a profile name, identifier, and (optionally) a signature.

In practice: you create the profile, upload it to your MDM, and the MDM installs it on devices.

## What you’ll need

- A Mac
- **iMazing Profile Editor**
- Admin access to **Microsoft Intune** (or another MDM)

## 1. Install iMazing Profile Editor

iMazing Profile Editor is an easy way to create and edit `.mobileconfig` files. It uses a fork of the [ProfileManifests](https://github.com/DigiDNA/ProfileManifests) repo to provide a UI for many macOS config payloads.

- [Direct download](https://imazing.com/profile-editor/download)
- [App Store download](https://apps.apple.com/se/app/imazing-profile-editor/id1487860882)

## 2. Add a payload

In iMazing Profile Editor, a *payload* is the set of configuration keys for a specific feature or app.

Example (DDM OS Reminder):

1. Open **iMazing Profile Editor**.
2. Scroll until you find **DDM OS Reminder**.
3. Select it and click **+ Add Payload**.

![DDM OS Reminder payload in iMazing]({{ '/assets/img/posts/2025-12-20-createmobileconfig/1.png' | relative_url }})

## 3. Configure the payload

Configure the keys you care about for the payload you added.

For the running example (**DDM OS Reminder**), all keys are optional—if you leave a value empty, the default value is used.

![DDM OS Reminder payload in iMazing]({{ '/assets/img/posts/2025-12-20-createmobileconfig/2.png' | relative_url }})

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

![DDM OS Reminder payload in iMazing]({{ '/assets/img/posts/2025-12-20-createmobileconfig/3.png' | relative_url }})

6. Set a **Custom configuration profile name** (shown locally under **System Settings** → **Device Management**).
7. Leave the deployment channel as **Device Channel**.
8. Upload the `.mobileconfig` you created.
9. Click **Next**, choose your **Assignment Groups**, and press **Create** to publish the policy.

![DDM OS Reminder payload in iMazing]({{ '/assets/img/posts/2025-12-20-createmobileconfig/4.png' | relative_url }})

The deployment flow is similar in other MDM solutions: create a custom profile policy, upload the `.mobileconfig`, then assign it to your target devices (or users, if your payload supports it).
