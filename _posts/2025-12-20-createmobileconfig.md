---
title: "Create and deploy a macOS configuration profile (.mobileconfig)"
date: 2025-12-20 22:10:00 +0100
categories: [Guides]
tags: [macOS]
---

This post will cover a workflow to:

1. Create a macOS configuration profile (`.mobileconfig`) with **iMazing Profile Editor**.
2. Deploy it using an MDM (**Microsoft Intune** in this example).

The workflow applies to many apps and macOS features. For this blog post we will use [DDM OS Reminder](https://github.com/dan-snelson/DDM-OS-Reminder) as the example payload.

## What is a `.mobileconfig`?

A `.mobileconfig` is an Apple **configuration profile** used to configure settings on macOS (and other Apple platforms).

Technically, it’s a document that contains:

- One or more **payloads** (plist dictionaries of keys/values)
- Profile metadata such as a name and identifier
- An signature *(this will be provided by the MDM, so you do not need to sign it yourself)*

## What you’ll need

- A Mac
- **iMazing Profile Editor**
- Admin access to **Microsoft Intune** (or another MDM)

## 1. Install iMazing Profile Editor

iMazing Profile Editor provides an easy-to-use GUI to create and edit `.mobileconfig` files. It uses a fork of the [ProfileManifests](https://github.com/DigiDNA/ProfileManifests) repository to provide a UI for many community macOS payloads.

- [Direct download](https://imazing.com/profile-editor/download)
- [App Store download](https://apps.apple.com/se/app/imazing-profile-editor/id1487860882)

## 2. Add a payload

In iMazing Profile Editor, a *payload* is the set of configuration keys for a specific feature or app.

Example (DDM OS Reminder):

1. Open **iMazing Profile Editor**.
2. Scroll until you find **DDM OS Reminder**.
3. Select it and click **+ Add Payload**.

![DDM OS Reminder payload in iMazing]({{ '/assets/img/posts/2025-12-20-createmobileconfig/1.png' | relative_url }})

*Tip: You can search by clicking the magnifying glass in the top-right corner, or by selecting any payload in the left sidebar and typing the first letters of the desired payload.*

## 3. Configure the payload

Configure the keys you care about for the payload you added.

For the example (**DDM OS Reminder**), all keys are optional, if you leave a value empty, the default value will be used.

![DDM OS Reminder configuration in iMazing]({{ '/assets/img/posts/2025-12-20-createmobileconfig/2.png' | relative_url }})

*Tip: Hover over the **?** next to each key to see details and the default value.*

## 4. Save the profile

Save the `.mobileconfig` via the top menu.

## 5. Deploy the profile via Intune

The deployment flow is similar in other MDM solutions: create a custom profile policy, upload the `.mobileconfig`, then assign it to your target devices/users.

1. In Intune, go to **Devices** → **macOS** → **Configuration**.
2. Click **Create** → **New policy**.
3. Under **Profile type**, select **Templates**.
4. Select **Custom**.
5. Set an **Intune policy display name** (shown in Intune), then click **Next**.

![Create a custom macOS profile in Intune]({{ '/assets/img/posts/2025-12-20-createmobileconfig/3.png' | relative_url }})

## 6. Configure the profile via Intune

1. Set a **Custom configuration profile name** (shown locally under **System Settings** → **Device Management**).
2. Leave the deployment channel as **Device Channel**.
3. Upload the `.mobileconfig` you created.
4. Click **Next**, choose your **Assignment Groups**, and press **Create** to publish the policy.

![Upload the .mobileconfig and assign groups in Intune]({{ '/assets/img/posts/2025-12-20-createmobileconfig/4.png' | relative_url }})
