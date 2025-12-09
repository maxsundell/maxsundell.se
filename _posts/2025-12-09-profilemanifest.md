---
title: "WIP: Creating profile manifests"
date: 2025-12-10 00:10:00 +0100
categories: [Guides]
tags: [macOS]
---

## This blogpost is WIP

* According to the <a href="https://github.com/ProfileManifests/ProfileManifests/wiki/Getting-Started">profilemanifest repo</a>, the recommended way to create a profile manifest is via the Profile Creator app. However the latest version of this app is not signed/notarized.
* Using ChatGPT and this prompt: "Using this profilemanifest template as a guide: https://raw.githubusercontent.com/ProfileManifests/ProfileManifests/refs/heads/master/ManifestExamples/com.github.profilecreator.exampleApplication.plist, create a profile manifest for this plist: $plist"
* You will likely get a faulty profile name and reverse domain notation, but this is easily fixed.
* Create a PR to the <a href="https://github.com/ProfileManifests/ProfileManifests">profilemanifest repo</a>.
* While awaiting the merge of your PR, you can use your manifest locally in iMazing Profile Editor by going to **iMazing Profile Editor** > **Settings...** > **Manifests** > **Local folder** and pointing to a local folder that contains your profile manifest.
