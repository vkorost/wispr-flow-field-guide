# macOS

*In this chapter you will learn why Accessibility permission is the single gate that controls whether Wispr Flow works or silently fails on your Mac, how to install the correct build for your hardware, and what to do when a system update resets the permissions you already granted.*

Every operating system has a chokepoint. On the Mac, it is a single toggle buried three clicks deep in System Settings. Grant Wispr Flow the Accessibility permission and dictation flows into every text field on your machine. Withhold it, or let a macOS update reset it, and Flow sits in your menu bar doing nothing useful while you wonder what broke. That toggle is The Permission Gate, and understanding it is the difference between a tool that works everywhere and one that fails in ways Apple never bothers to explain.

## Getting the Right Build

Before you touch permissions, you need the right binary. Wispr Flow ships two separate downloads: one for Apple Silicon (M1 and later) and one for Intel.<sup>[1]</sup> Install the wrong one and the app quits on launch with a dialog titled "Incorrect App Version" that reads: "You are running the Intel version of Wispr Flow on an Apple Silicon Mac. Please download the Apple Silicon version from wisprflow.ai for better performance."<sup>[1]</sup>

Check your chip first. Apple menu, About This Mac, look at the Chip or Processor line. Apple Silicon says something like "Apple M1" or "Apple M2 Pro." Intel says "Intel Core i5" or similar. Download the matching build from wisprflow.ai and move on.

The minimum is macOS 12.0, Monterey.<sup>[1]</sup> Anything older gets an "Unsupported MacOS Version" dialog and the app refuses to launch.<sup>[1]</sup> As of Q2 2026, Monterey is four major releases behind the current macOS. If you are still on it, Flow will run, but you are living on the edge of Apple's own support window.

## Installation in Under a Minute

The install is a drag-and-drop. Open the downloaded .dmg, drag the Wispr Flow icon onto the Applications folder shortcut in the installer window, close the installer window, and launch from Applications, Launchpad, or Spotlight.<sup>[1]</sup>

Three constraints matter here:

- Flow must live in an Applications folder. It accepts /Applications, ~/Applications, or /System/Applications, and nothing else.<sup>[1]</sup> Launching it from your Downloads folder or from the still-open installer window triggers a "Flow needs to be in the Applications folder to run" error, even if you already dragged the app to the right place.<sup>[1]</sup>
- Flow runs in the menu bar only. It does not appear in the Dock. It does not appear in the Cmd+Tab switcher. It sets itself to launch at login automatically.<sup>[1,2]</sup> If you are the kind of user who force-quits Dock-less apps and then wonders where they went, look up. The Wispr Flow icon is in your menu bar.
- After you eject the .dmg, delete the installer file from Downloads. It is just taking up space.

## The Permission Gate

Here is where the Mac diverges from every other platform Flow runs on. On Windows, Flow needs only system microphone access (see Ch3, The Electron Tax). On iOS, it is a keyboard extension with its own toggle (see Ch5). On Android, it is an overlay service (see Ch6). On macOS, Flow needs two permissions granted manually, and a third is optional.<sup>[3]</sup>

### Microphone

This one is obvious. A dictation app needs to hear you. On first launch, macOS shows the native permission dialog asking whether Wispr Flow can access the microphone. Click Allow.<sup>[1]</sup>

If you click "Don't Allow" (or if a previous install left the permission denied), Flow detects the denial and opens System Settings directly to Privacy & Security, Microphone, so you can flip the toggle yourself.<sup>[1,3]</sup> Flow picks up the change automatically; no restart required.

Microphone permission is necessary but not sufficient. Without it, Flow cannot record. With it alone, Flow can record but cannot insert text reliably, because insertion on macOS depends on the next permission.

### Accessibility

This is The Permission Gate itself. On Mac, Accessibility permission is what allows Flow to read the active text field, detect which app has focus, respond to the hotkey even when another app is in the foreground, and insert transcribed text at the cursor.<sup>[3]</sup> Context Awareness, the feature that adapts output to the app you are using (see Ch9, The App-Aware Rewrite), also requires Accessibility on Mac.<sup>[4]</sup>

Without Accessibility, Flow records your voice, sends it to the cloud, gets a transcript back, and then has nowhere to put it. The symptom is silence: you speak, the waveform animates, and nothing appears. No error, no explanation. Just nothing.

Open System Settings, Privacy & Security, Accessibility, and make sure Wispr Flow is toggled on.<sup>[3]</sup> If it is not listed at all, reinstall Flow. If it is listed but toggled off, toggle it on. macOS may ask you to authenticate with your password or Touch ID.

The hotkey behavior depends on this permission too. The default Mac hotkey is Fn: hold it to dictate, release to submit. The backup is Ctrl+Option for Macs or external keyboards where the Fn key behaves differently.<sup>[5]</sup> If your hotkey press does nothing at all, check Accessibility first. Keyboard shortcuts require it.<sup>[3]</sup>

### Screen Capture (Optional)

Screen Capture permission is not required for basic dictation. It enables advanced features that benefit from reading on-screen content beyond what Accessibility alone provides.<sup>[3]</sup> You can grant it later if you find you want those features. Skipping it does not break anything fundamental.

## What Lives Where

Flow stores its data in several standard macOS locations:

- ~/Library/Application Support/Wispr Flow (main data)
- ~/Library/Logs/Wispr Flow (logs)
- ~/Library/Caches/Wispr Flow (cache)
- ~/Library/Preferences/Wispr Flow.plist (preferences)
- ~/Library/Saved Application State/Wispr Flow.savedState (window state)
- ~/Library/HTTPStorages/Wispr Flow (network storage)<sup>[6]</sup>

A legacy path, ~/Library/Application Support/Flow, may exist if you installed an earlier version of the app.<sup>[6]</sup>

You do not need to manage these directly under normal use. They matter when troubleshooting, when doing a clean uninstall, or when you discover that your iCloud Drive or OneDrive sync has been pointed at ~/Library and is silently corrupting Flow's database (see Ch20, The Synced Identity, for the sync-corruption scenario).

## After Updates: the Gate Can Close

macOS has a habit of resetting permissions after system updates. Apple does this for security reasons that are defensible in theory and infuriating in practice. You granted Accessibility last month; you updated to macOS 15.5; now Accessibility is toggled off and Flow has stopped inserting text. No notification. No prompt. You just start talking and nothing happens.

The fix is the same every time.<sup>[3]</sup>

1. Quit Flow (click the menu bar icon, select Quit).
2. Open System Settings, Privacy & Security, Microphone. Find Wispr Flow, toggle it off, then on again.
3. Go to Privacy & Security, Accessibility. Confirm Wispr Flow is enabled.
4. Reopen Flow from Applications.
5. Dictate a short phrase. If text appears, you are done.

On recent macOS versions, Flow's in-app permission links open the correct System Settings pane automatically.<sup>[3]</sup> On older versions, or on macOS Tahoe where a bug caused permission links to open the wrong pane, you may need to navigate manually. That specific bug was fixed in a recent Flow update.<sup>[3]</sup>

The real lesson is this: if Flow was working yesterday and is not working today, and you recently updated macOS, the answer is almost always permissions. Re-verify before you do anything else.

## The Menu Bar Life

Flow on Mac is a menu-bar-only application.<sup>[1,2]</sup> There is no window. There is no Dock icon. Cmd+Tab will not find it. This is by design: a dictation tool that sits in your peripheral vision, ready when summoned, invisible when not.

The Flow Bar appears when you activate dictation (hold Fn or your configured hotkey). It shows an animated waveform while listening (verify the exact color behavior on your device). When you release the hotkey, the audio goes to the cloud, the transcript comes back, and Flow inserts it at your cursor. The Flow Bar disappears.

This interaction model is clean once you internalize it. The confusion comes when something goes wrong and you look for Flow in the Dock, in Cmd+Tab, in the App Switcher, and find nothing. Flow is always in the menu bar. Click the icon there to access settings, check for updates, or quit.

## What This Chapter Does Not Cover

The Mac chapter is self-contained. You do not need to read Ch3 (Windows), Ch5 (iPhone), or Ch6 (Android) to set up Flow on your Mac. What happens after you start dictating (the cleanup engine, context awareness, command mode, dictation habits) lives in later chapters.

Specifically:

- The Rewrite Pass (Ch1) explains what Flow does with your speech after it leaves the microphone.
- Trigger Discipline (Ch2) covers push-to-talk versus hands-free mode, session limits, and hotkey mechanics in detail.
- The Cleanup Dial (Ch7) controls how aggressively Flow rewrites your words.
- The App-Aware Rewrite (Ch9) explains Context Awareness, which requires Accessibility permission on Mac (and you now know why that matters).
- The Failure Map (Ch24) covers troubleshooting when something breaks.

Your job in this chapter was to get through The Permission Gate. Everything that follows assumes you did.

## Key Points

- Accessibility permission is the single control that determines whether Flow can insert text, detect apps, and respond to hotkeys on macOS.
- Installing the wrong chip-specific build (Apple Silicon vs. Intel) causes an immediate quit with no workaround except downloading the correct version.
- macOS system updates can silently reset permissions, causing Flow to stop working without any visible error or notification.
- Flow runs exclusively in the menu bar and will never appear in the Dock or the Cmd+Tab application switcher.
- Microphone permission lets Flow hear you, but Accessibility permission lets Flow act on what it heard.
- Screen Capture is optional and can be granted later without breaking basic dictation functionality.
