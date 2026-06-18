# Chapter 24: Troubleshooting

*In this chapter, you learn how to diagnose and fix the most common failures in Wispr Flow. The path from microphone to finished text is short, and so is the list of places it can break. The Failure Map organizes every symptom by its root cause so you can stop guessing and start fixing.*

Something broke. You pressed the hotkey, spoke clearly, and nothing happened. Or text appeared in the wrong place. Or the Flow Bubble vanished and will not come back. The instinct is to restart everything and hope, but Flow's failure modes are specific enough that a restart is usually overkill and sometimes misses the actual problem.

Call it The Failure Map. The dictation pipeline has four stages (capture, cloud recognition, cleanup, insertion), and every failure you will encounter lives at one of those stages or at the edges where your device, your permissions, or your network connect to the pipeline. Knowing which stage broke is the difference between a ten-second fix and twenty minutes of blind troubleshooting.

This chapter is organized by symptom. Find what you see on your screen, read the cause, apply the fix. Cross-references point to earlier chapters where a feature or concept was introduced; this chapter does not re-explain them, only maps the failure.

## Not Recording

You press the hotkey or tap the bubble. Nothing happens. No waveform, no text, no error.

**Microphone permission is missing or revoked.** On Mac, both Microphone and Accessibility permissions are required; Screen Capture is optional for advanced features but not needed for basic dictation.<sup>[1]</sup> On Windows, no app-level permissions are required; only system microphone access matters.<sup>[1]</sup> On iOS, if Wispr Flow is not listed under Microphone in iOS Settings, tap Start Flow or the mic button to trigger the system permission request.<sup>[1]</sup> On Android, the home screen shows diagnostic cards: "We can't hear you" (mic), "Flow Bubble Disabled" (service stopped), "Enable Flow bubble on screen" (overlay missing), "Flow can't insert text" (accessibility missing), "Keep Wispr Flow running" (battery optimization), or "Bubble is snoozed."<sup>[1]</sup>

**Fix:** Toggle the relevant permission off and back on, then restart Flow. On Mac, System Settings, Privacy and Security, then Microphone and Accessibility. On Android, follow whichever home screen card appears. On iOS, Settings, Wispr Flow, Microphone.

**Clamshell mode on Mac.** Closing your laptop lid disables the built-in microphone. Flow shows a "Your laptop lid is closed" notification.<sup>[2]</sup> Connect an external microphone or open the lid.

**Another app holds the microphone exclusively.** Flow surfaces a specific notification: "Microphone is in use" or "Microphone unavailable."<sup>[3]</sup> Close the competing app (Zoom, Teams, Google Meet, Discord, FaceTime are common culprits) and try again.<sup>[3]</sup>

**Mic recording not released after Bubble dismiss on Android.** On desktop, dismissing the bubble during dictation could leave the microphone recording for the remainder of the session limit (see The Input Chain, Chapter 18, for the full treatment of mic behavior). This was addressed in recent updates.<sup>[4]</sup>

## Not Pasting

Flow transcribes your speech. You can see the transcript in History. But nothing lands in the text field.

**Clipboard conflict on Mac and Windows.** Flow temporarily uses the system clipboard to paste text and restores your previous clipboard contents afterward.<sup>[5]</sup> If the target app blocks clipboard access (Citrix, virtual desktops, corporate apps, password managers), text will not arrive. Test in a plain text editor first. If text appears there but not in your target app, the app is blocking paste.<sup>[5]</sup>

**Recovery shortcuts exist.** On Mac, press Ctrl+Cmd+V for "Paste last transcript." On Windows, Alt+Shift+Z.<sup>[5]</sup> The Scratchpad (Chapter 16) also stores your most recent transcript: Option+S on Mac, Win+Alt+S on Windows.<sup>[5]</sup>

**Windows privilege conflict.** If you see a notification reading "Update admin settings to paste!", the target app is running with higher privileges than Flow. Quit Flow, then relaunch it as Administrator.<sup>[5]</sup>

**iOS auto-deactivation in restricted fields.** Flow automatically deactivates in number, phone, decimal, email address, numbers-and-punctuation, and ASCII-capable number pad fields.<sup>[5]</sup> Switch to a standard text field.

**Android direct insertion.** Flow inserts text directly in WhatsApp, Telegram, Messenger, Instagram, Teams, Signal, Slack, Discord, Snapchat, Google Messages, and Gmail, plus the Google search box and Chrome New Tab Page search field.<sup>[5]</sup> If insertion fails, the Flow Bubble shows a copy button so you can paste manually. In the Chrome address bar, text may be copied to the clipboard rather than inserted directly.<sup>[5]</sup>

**Non-QWERTY and non-Latin keyboard layouts** can also break insertion. This is covered under The Insertion Boundary (Chapter 17).

## Slow or Failed Transcription

You dictated, Flow recorded, but text either never arrives or takes unusually long.

**"Taking longer than usual."** This message appears when Flow's servers need extra processing time. It is permanently dismissable with "Don't show again."<sup>[6]</sup> On Android, the toast reads: "Taking longer than usual. Your audio is saved in the app."<sup>[6]</sup> Common causes: temporary server load, slow internet, VPN or firewall interference.

**Audio retention and retry.** Audio recordings are stored locally for 14 days. After that, the audio is removed but the transcript text and history entry are kept.<sup>[6]</sup> With NeverStore (Zero Data Retention) enabled, audio is never saved to History and retry from saved audio is unavailable.<sup>[6]</sup>

**How to retry.** On desktop, a failure notification includes Retry and Open History buttons. On iOS, tap the orange triangle warning icon that appears next to the mic button to see details and retry (for server errors) or dismiss (for network errors).<sup>[7]</sup> On Android, the Flow Bubble shows a Retry button for transcription failures and a Paste button for insertion failures.<sup>[7]</sup>

**Minimum requirements for retry on desktop:** the recording must be at least 5 seconds long and less than 14 days old. Dismissed transcripts have no 5-second minimum.<sup>[7]</sup>

**Retry is blocked during active dictation.** On desktop, attempting retry while dictating shows a "Cannot retry while dictating" toast.<sup>[7]</sup>

## "No Model Available" and Startup Errors

Flow shows "No Model Available," "Flow is having trouble starting," "Audio system failed to load," or simply stops responding.

**What "No Model Available" means:** Flow could not load the transcription model. Restarting Flow and checking your internet connection resolves it in most cases.<sup>[2]</sup>

**"Your laptop lid is closed" (Mac only):** the built-in mic is unavailable in clamshell mode. Select an external mic.<sup>[2]</sup>

**"Microphone Permission Required":** On Mac, this triggers a system prompt on first use or opens System Settings if you previously denied access. On Windows, it opens system microphone privacy settings.<sup>[2]</sup>

**Escalation path:** If the "Flow is having trouble loading" notification persists, the issue moves to "Flow is having trouble starting" after multiple retries. Both notifications offer Restart Flow and Contact us buttons.<sup>[2]</sup>

## Degraded Accuracy

Transcription was working yesterday. Today the output is garbled, words are wrong, or sentences cut off mid-thought.

**Most common cause: wrong microphone.** A Bluetooth device in your pocket, a webcam mic across the room, or a wireless headset that connected automatically. Check your system sound settings and confirm the correct input device is selected.<sup>[8]</sup>

**Extract and listen to the audio.** On Mac and Windows, open History, find the entry, click the three-dot menu, and click Extract audio to save a .wav file.<sup>[8]</sup> If the audio itself is distorted, the problem is upstream of Flow. If the audio is clean but the transcript is wrong, retry the transcription. Audio extraction is not available on iOS.<sup>[8]</sup>

**Language settings.** If Flow is transcribing in the wrong language, check your language selection. On desktop, the Flow Bar language indicator lets you cycle through selected languages; hover to reveal the chevron for the full picker.<sup>[4]</sup> On Android, Auto-detect is not available; you must select at least one specific language (see One Language Per Breath, Chapter 13).

**Dictionary overload.** A very large dictionary with hundreds or thousands of entries can sometimes cause odd substitutions. Trim to the most important terms if you see unexpected word replacements.<sup>[8]</sup>

## Flow Bar and Flow Bubble Issues

The desktop Flow Bar or the Android Flow Bubble is missing, flickering, or unresponsive.

**Flow Bar hidden deliberately.** The right-click menu includes "Hide for 1 hour," and the bar can also be hidden permanently from Settings.<sup>[4]</sup> Check there first.

**Android Bubble: pulsing loader vs. warning triangle.** The pulsing loader means Flow is auto-reconnecting to the accessibility service; no action needed. The warning triangle means reconnection has stalled or accessibility permission was revoked. Tap the triangle to go directly to accessibility settings and re-enable Flow.<sup>[4]</sup>

**Battery optimization is the top Android killer.** Aggressive battery management on Samsung, Xiaomi, Redmi, POCO, Vivo, Oppo, OnePlus, Motorola, Huawei, Honor, Realme, and Transsion devices is the most common reason the Flow Bubble disappears in the background.<sup>[4]</sup> Each manufacturer has its own exemption path. Samsung uses "Never sleeping apps"; Xiaomi, Redmi, POCO, and Vivo use "Autostart"; Oppo uses "Allow Auto-Launch" and "Allow Background Activity"; Huawei and Honor use "App launch" toggles; Realme and OnePlus use battery optimization exclusions; Motorola and Transsion use "Don't optimize."<sup>[4]</sup>

**Bubble reappearance.** If the Flow Bubble disappears, it should reappear on its own within about 45 seconds. If it does not, open the app from your launcher. If you revoke the "Display over other apps" permission while the bubble is visible, it disappears and will not return until the permission is restored.<sup>[9]</sup>

## Missing First Words

Your dictation starts mid-sentence. The first word or two are gone.

**Root cause: wireless microphone wake-up delay.** AirPods and other wireless mics can be slow to activate. Flow flags AirPods with a warning symbol in the desktop mic list.<sup>[10]</sup>

**Fix:** Switch to the built-in microphone or a wired USB mic, which have zero wake-up delay.<sup>[10]</sup> If you prefer wireless, pause briefly after pressing the hotkey and wait for the Flow Bar waveform to start moving before speaking. Starting with a filler word ("so," "okay") works; Smart Formatting removes these automatically.<sup>[10]</sup>

**Auto-detect mic setting** shows the currently active device name in parentheses (e.g., "Auto-detect (MacBook Pro)"). Selecting your microphone explicitly may reduce connection delays.<sup>[10]</sup>

**Built-in mic labeled "Built-in mic (recommended)"** in the selection list.<sup>[10]</sup> Virtual microphones from audio routing software are hidden from Flow's list unless set as the system default.<sup>[10]</sup>

## Connection Lost

Flow shows "Connection lost," dictation stops mid-sentence, or the app will not connect at all.

**VPN and security software are the usual suspects.** Flow is incompatible with most VPNs. Common offenders include NordVPN, ExpressVPN, Surfshark, Cisco AnyConnect, GlobalProtect, corporate proxies (Zscaler, Netskope, Palo Alto, Fortinet), antivirus web filters (Norton, McAfee, Bitdefender, Kaspersky), DNS filters (Pi-hole, AdGuard, NextDNS), and macOS firewalls (Little Snitch, LuLu).<sup>[11]</sup>

**What to whitelist:** the Wispr Flow application itself, plus the domains wisprflow.ai, api.wisprflow.ai, and inference.wisprflow.com.<sup>[11]</sup> If you must use a VPN, enable split tunneling and exclude these domains.<sup>[11]</sup>

**iOS partial transcript preservation.** If the connection drops mid-dictation on iOS, Flow preserves successfully transcribed segments and pastes them. You get a partial transcript rather than nothing.<sup>[12]</sup> Flow also switches to a backup transcription path immediately on first segment failure, without waiting for each subsequent segment.<sup>[12]</sup>

**"Disable Flow Session" timer on iOS** controls how long Flow keeps the session alive when the app is backgrounded. Options: Never, 1 hour, 15 min, 5 min (default), Immediately.<sup>[12]</sup>

## Restart, Reset, and Reinstall

Three escalation tiers, from lightest to heaviest.

**Quit and relaunch** clears background processes. On Mac, Cmd+Q and reopen from Applications. On Windows, right-click the system tray icon, Quit, reopen from Start. On iOS, swipe up and away. On Android, Force stop in Settings, then reopen.<sup>[13]</sup> If you quit or restart Flow while a dictation is in progress on desktop, the audio is automatically saved and appears in History with a Recover link on relaunch. Exception: a crash or force-kill may not save audio.<sup>[13]</sup>

**Reset and Restart** is available on desktop only (Settings, System, Data).<sup>[9]</sup> This deletes local History, Dictionary, Notes, notifications, meetings, calendar events, and backup files. Stats and settings are preserved.<sup>[6,9]</sup> Your dictionary re-syncs from your account on the next launch. On iOS and Android, force close or reinstall instead.<sup>[9]</sup>

**Complete removal** strips all data, including hidden folders and system permissions. Mac has an uninstall script; Windows has a batch script.<sup>[14]</sup> On iOS, simply deleting the app does not remove the login session or data shared with the Flow Keyboard extension; you must sign out and remove the keyboard extension first.<sup>[14]</sup> On Android, auto backup may restore app data; clear storage before uninstalling for a completely fresh state.<sup>[14]</sup>

## App Does Not Start

You click the icon. Nothing happens, or you see a blank screen.

**Windows installer.** Download the latest installer from wisprflow.ai/downloads.<sup>[15]</sup>

**Sign-in session timeout.** On desktop, complete the browser sign-in promptly. If the browser login takes too long, the desktop app resets and you must click Sign in via browser again.<sup>[15]</sup>

**Mac runs in menu bar only.** Wispr Flow does not appear in the Dock or the Cmd+Tab switcher. This is by design.<sup>[15]</sup> Look for the icon in the top-right menu bar.

**Android crash loop after microphone permission revoked (Android 14+).** Revoking microphone permission caused the app to crash on every launch. Fixed in recent versions: the app now starts in a limited non-recording state and prompts you to restore mic access.<sup>[15]</sup>

**Database corruption from cloud sync.** Storing Flow's app data in iCloud or OneDrive can mark database files read-only, causing corruption and crash loops.<sup>[9]</sup> Move the data folder out of any cloud-synced directory.

## Login Issues

**Sign-in paths differ by platform.** Desktop: Sign in via browser is the only path; all provider selection happens in the browser.<sup>[16]</sup> iOS: Google and Apple shown by default; Microsoft, SSO, and Email behind "More Options."<sup>[16]</sup> Android: all five options shown on the login screen.<sup>[16]</sup>

**You cannot switch login methods** once your account is created, and multiple emails cannot be linked to a single account.<sup>[16]</sup>

**CAPTCHA blocks.** CAPTCHA appears during account creation, password reset, and verification resend, not during standard login. If the CAPTCHA cannot load, the relevant button stays disabled.<sup>[17]</sup> Android does not include CAPTCHA.<sup>[17]</sup>

**Redirect loops on the download page.** Try a different browser with extensions disabled, or clear your browser cache. On mobile, install from the App Store or Google Play instead.<sup>[18]</sup>

## Service Status

**Orange banner = degraded performance. Red banner = outage.** These appear on the Hub home page on Mac and Windows only; iOS and Android do not show incident banners.<sup>[19]</sup>

**Incident notifications bypass mute settings** and cannot be silenced.<sup>[19]</sup> They are throttled to avoid repeated interruptions during a prolonged incident.<sup>[19]</sup>

**Region-specific.** Banners appear only when the active incident affects the region associated with your account. The banner auto-dismisses when the incident is resolved.<sup>[19]</sup>

**Gradual rollout.** If you do not see incident banners, the feature may not yet be enabled on your account as of Q2 2026.<sup>[19]</sup>

## Re-Verifying Permissions After Updates

System or app updates can silently reset or revoke permissions on every platform.

**Mac:** toggle Microphone and Accessibility permissions off and back on in System Settings, then restart Flow.<sup>[1]</sup>

**Windows:** check that system microphone access is enabled in Windows Sound Settings. No app-level permission is needed.<sup>[1]</sup>

**iOS:** if the "We can't hear you" card appears, tap Go to Settings and re-enable the Microphone toggle.<sup>[1]</sup>

**Android:** follow whichever home screen card appears (mic, overlay, accessibility, battery, snooze). On Samsung and other OEM devices, the system can silently drop Flow's accessibility connection without any in-app warning.<sup>[1]</sup> Flow now sends a notification when this happens; tap it to go directly to accessibility settings.<sup>[1]</sup>

## iOS Audio Chunk Loss

On unstable internet, words or sentences can go missing from a dictation.

**Partial transcript preservation.** If one segment of a long dictation fails, successfully transcribed segments are preserved and pasted. You get a partial transcript rather than nothing.<sup>[12]</sup>

**Backup transcription path.** Flow switches to its backup path immediately on first segment failure. It does not wait for each subsequent segment.<sup>[12]</sup>

**Keyboard disables dictation controls when offline.** The controls return automatically when the connection is restored.<sup>[12]</sup>

**Manual cancel does not save audio.** If you cancel a recording in progress, the audio is not preserved.<sup>[12]</sup>

## Database Errors

**On Mac and Windows,** a database error notification appears when the disk is full, local data is corrupted, or the dictionary cannot load. Flow continues running but the dictionary may not apply and history may not save until you restart.<sup>[9]</sup>

**Cloud sync folders cause this.** iCloud and OneDrive can mark Flow's database files read-only, triggering corruption and crash loops. Move the data folder out of any synced directory.<sup>[9]</sup>

**Fix:** Click Restart Flow in the notification. If the notification persists, use Reset and Restart (Settings, System, Data) for a full recovery.<sup>[9]</sup>

## Getting Support

Three channels, each routed differently.

**Report an Issue** goes to the support team and receives a direct response. **Share Feedback** goes to the product team; no reply. **Flag a Transcript** is used for model training; no reply.<sup>[20]</sup>

**Attachment limits.** Desktop and Android: PNG, JPEG, BMP, or WebP, one file, 10 MB max.<sup>[20]</sup> iOS: text-only, no image attachments.<sup>[20]</sup>

**Desktop diagnostic logs** and config are auto-attached to support reports. iOS and Android send only your message text and any attached image.<sup>[20]</sup>

**Keyboard shortcut on Mac:** Cmd+/ opens Talk to support. Submit with Cmd+Enter (Mac) or Ctrl+Enter (Windows).<sup>[20]</sup>

**If you cannot sign in,** the desktop login screen has a Help button that opens a "Send a message to the Flow team" dialog. If Flow crashes, the error recovery screen offers a Contact support button that pre-fills an email to support@wisprflow.ai.<sup>[20]</sup>

## Key Points

- Every Flow failure lives at one of four pipeline stages: capture, recognition, cleanup, or insertion; identify the stage before you troubleshoot.
- Wireless microphone wake-up delay is the single most common cause of missing first words; wired or built-in mics eliminate it.
- On Android, aggressive battery optimization from the device manufacturer is the top reason the Flow Bubble disappears in the background.
- Audio is retained locally for 14 days on desktop, giving you a retry window for any failed transcription.
- Reset and Restart on desktop is the nuclear option that deletes local history; use it only when simpler restarts fail.
- Service status banners on Mac and Windows tell you whether an outage is on Flow's side, saving you from troubleshooting a problem you cannot fix.
- When reporting an issue, include your platform, the exact error text, and what you already tried; the support team resolves most cases in one reply.
