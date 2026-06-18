# iPhone (iOS)

*In this chapter: Flow on the iPhone is not a system service; it is a keyboard extension you switch to, with the Action Button and Siri Shortcuts as the shortcuts around that friction. The setup, the gotchas, and the ways to make dictation feel native on iOS are what separate a frustrating first hour from a working workflow.*

Every other platform in this book gives Flow a system-wide hook. On Windows, it is a hotkey. On Mac, it is a hotkey. On Android, it is a floating bubble that watches for the keyboard to appear. On the iPhone, Flow is a keyboard. You install it, you add it, you switch to it, and you dictate. Then you switch back. That switching cost is The Keyboard Detour, and every workflow decision on iOS flows from it.

The detour is not a bug. Apple does not let third-party apps inject text system-wide the way macOS Accessibility or Android Overlay permissions allow. A custom keyboard extension is the approved path, and Flow takes it. Understanding that constraint, rather than fighting it, is how you make iOS dictation fast.

## Setting Up the Flow Keyboard

Setup takes under a minute, but the order matters.<sup>[1]</sup>

First, install Wispr Flow from the App Store and open it at least once. The keyboard will not appear in iOS Settings until the app has launched. Sign in; the keyboard will not function without an active session.

Then add the keyboard: open Settings, tap General, then Keyboard, then Keyboards, then Add New Keyboard, and select Wispr Flow. Tap Wispr Flow in the keyboard list and enable Allow Full Access. iOS will show a confirmation popup; tap Allow.<sup>[1]</sup>

Full Access is not optional. Without it, the keyboard loads but cannot dictate.<sup>[1]</sup> Flow needs network access to send audio to its transcription servers, and Full Access is what grants a keyboard extension that capability. Audio is handled securely and is not stored on the server side (see Ch21, The Cloud Boundary, for the full privacy treatment).

To verify: open any app with a text field, tap and hold the globe icon on the keyboard, select Wispr Flow, then tap the microphone button and speak a short phrase. If text appears, the detour works.

One behavioral note worth internalizing early: the Flow Keyboard should remain visible until the transcription appears. Dismissing the keyboard or switching apps mid-processing may interrupt the transcript, so treat it as a caution rather than a guarantee of data loss.<sup>[1]</sup> On desktop, you can fire and forget; on iOS, it is safer to wait.

## The Globe-Key Tax

Switching keyboards via the globe icon is the most frequent friction point. Every time you want to dictate, you hold the globe, pick Flow, tap the mic, speak, and then (if you need to type afterward) hold the globe again and switch back. That is the raw cost of The Keyboard Detour.

Flow mitigates it in two ways: the Action Button and Siri Shortcuts. Both let you start dictation without touching the globe key.

## The Action Button

If you own an iPhone with a hardware Action Button, this is the fastest path to dictation on iOS. The Action Button is available on iPhone 15 Pro and Pro Max, all iPhone 16 models (including 16e), and all iPhone 17 models (including Air). The iPhone 17e lacks the hardware button and is excluded.<sup>[2,3]</sup>

Flow offers six shortcuts you can assign to the Action Button: Turn On/Off Flow, Dictate a Flow Note, Quick Dictation to Clipboard, Quick Dictation to Notes, Open Flow Notes, and Save Flow Note.<sup>[2,3]</sup> Quick Dictation to Clipboard copies the transcript to your clipboard; Quick Dictation to Notes saves it as a Flow note. When the Flow keyboard is active in a text field, both modes auto-insert text directly into the field instead. When the keyboard is not active, the clipboard shortcut copies text and the notes shortcut saves a note.

Setup can happen two ways. The guided path: after you have dictated at least 50 words across 3 successful dictations, a feature card appears in the keyboard prompting you to set it up.<sup>[2,3]</sup> Tap Set up and follow the walkthrough. The manual path: open the Wispr Flow app, go to Settings, then Action button shortcut, and follow the prompts to map the shortcut in iPhone Settings under Action Button.<sup>[3]</sup>

One useful behavior: pressing the Action Button while a recording is already in progress picks up the running session and begins transcription rather than canceling it. A second press stops and saves.<sup>[3]</sup> Back-to-back dictations after the first are noticeably faster because the iOS audio stack is already initialized.

## Siri Shortcuts

Six Siri Shortcuts install automatically when you add Wispr Flow; no manual setup is required.<sup>[4]</sup> They require iOS 18.3 or later.<sup>[4]</sup>

The shortcuts and their voice commands:

- **Dictate a Flow Note.** Say "take Flow note" or "dictate with Flow." When the Flow keyboard is active, text inserts into the current field. Otherwise, the transcript saves as a Flow note.
- **Quick Dictation to Clipboard.** Say "quick dictate with Flow" or "dictate to clipboard with Flow." Returns the transcript to the clipboard (or inserts directly if the Flow keyboard is active).
- **Quick Dictation to Notes.** Say "quick dictate to notes with Flow" or "save note with Flow." Saves the transcript as a note.
- **Turn On/Off.** Say "turn on off Flow" to toggle recording.
- **Open Flow Notes.** Say "open Flow note" or "create Flow note." Opens the app to a new note and starts dictation.
- **Save Flow Note.** Say "save Flow note" or "quick Flow note." Siri asks what the note should say, then saves it without opening the app.<sup>[4]</sup>

The Save Flow Note shortcut is the closest iOS gets to hands-free dictation. You never open the app, never touch the keyboard, never switch contexts. Siri confirms with "Note saved."

Beyond Siri, you can assign any of these shortcuts to Back Tap (double or triple tap the back of your iPhone, under Settings then Accessibility then Touch) or to Control Center widgets. Flow provides two Control Center widgets: a recording toggle and a Flow Notes button.<sup>[4]</sup> A Live Activity also appears on the Lock Screen and Dynamic Island while dictating, with interactive stop and save buttons.<sup>[5]</sup>

## The iOS 26.4 Adaptation

A recent iOS 26.4 update introduced a behavioral change that affects the keyboard detour. Tapping Start Flow used to briefly open the Wispr Flow app and return you automatically. After iOS 26.4, you may need to swipe back manually. Apple changed how apps switch between each other, and Flow cannot override it.<sup>[6]</sup>

When this happens, you see a screen titled "Swipe back to your app." A one-time alert explains the new requirement the first time it triggers; tap OK and it will not appear again.<sup>[6]</sup> Voice-to-text works exactly as before once you are back in your original app.

The second iOS 26.4 change: styles no longer auto-adjust by app on iOS. Your default style now applies everywhere unless you override it. Flow shipped two mitigations: a Style tab in the app where you set a default style per category (Personal, Work, Email, Other), and a Quick Style Switcher on the keyboard (a style pill next to the Start Flow button that lets you temporarily override the style without leaving your app).<sup>[6]</sup> The override persists until you change it or clear it.

Note: the swipe-back change is rolling out gradually. Some users on iOS 26.4 may still see the legacy automatic switch-back behavior.<sup>[6]</sup>

## Notification Management

Flow uses two notification surfaces on iOS: push notifications (managed in iPhone Settings) and in-keyboard notification cards (managed by the app itself, no permissions required).<sup>[5]</sup>

Push notifications are minimal. The main push fires when a friend you referred meets the qualifying threshold, earning you a free month of Pro. A local notification may also appear if you leave the app during initial setup. Toggle push notifications in iPhone Settings under Apps then Wispr Flow then Notifications, or from Wispr Flow's own Settings.<sup>[5]</sup>

Keyboard notification cards are more active. They appear directly in the keyboard as an overlay panel (tap the menu icon to open, swipe down or tap X to close). Cards include word-limit warnings for free-plan users, referral rewards, streak progress during your first week, milestone celebrations, and the Action Button setup prompt. Most appear after at least 3 successful dictations. They are in-app only and cannot be controlled through iOS notification settings.<sup>[5]</sup>

During your first week, Flow tracks a streak: dictate on 5 different days within 7 (not necessarily consecutive) and a congratulations card appears. Starting from your second streak day, the notification drawer auto-opens after a successful dictation, accompanied by a haptic vibration.<sup>[5]</sup>

## Hide My Email

If you signed up with Sign in with Apple and chose Hide My Email, your account email ends in @privaterelay.appleid.com. When you need that address (for support, for referrals, for account recovery), find it under iPhone Settings, tap your name, then Sign-In and Security, then Hide My Email, then locate Wispr Flow in the list.<sup>[7]</sup>

One referral-program consequence worth noting: referral matching uses the exact email address, so an invitation sent to your real email will not connect to a relay address account. Use your real email at sign-up if referrals matter to you.<sup>[7]</sup>

## Restoring Purchases

iOS subscriptions are managed through the App Store, and restoring them has its own set of alert states. The Restore Purchases button lives at the bottom of the in-app paywall (Menu then upgrade button then Restore Purchases). It applies only to App Store subscriptions; if you subscribed via the website or desktop app, this path does not apply.<sup>[8]</sup>

Five possible outcomes after tapping Restore Purchases:

- **Entitlement Found.** Success. The alert names the specific subscription restored. Tap OK; the paywall closes.
- **No Active Subscription Found.** Either you are signed into a different Apple ID than the one you subscribed with, or your subscription has lapsed. Verify the Apple ID in iPhone Settings and check subscription status under Subscriptions.
- **Purchase Found, Sync Needed.** Flow detected a purchase but could not sync it to your account. Usually clears on retry. Sign out and back in if it persists.
- **Subscription Linked to Another Account.** App Store subscriptions are permanently linked to the Wispr Flow account they were first activated with. Sign in with the original account.
- **Restore Failed.** A generic network or server failure. Retry after confirming your connection.<sup>[8]</sup>

One hard rule: do not purchase a second subscription to work around a restore failure. Contact support instead.<sup>[8]</sup>

## Session Limits and Platform Boundaries

iOS dictation sessions have a 5-minute ceiling (documented in Ch2, Trigger Discipline). The Flow Keyboard automatically switches to the system keyboard for number pads, phone fields, decimal pads, email-address fields, and numbers-and-punctuation fields; this is expected behavior, not a failure.<sup>[1]</sup> Some apps with custom text fields (certain banking apps, for instance) may not support third-party keyboards at all.<sup>[1]</sup>

If another app is using the microphone, the keyboard cannot record. It will show an error message and prompt you to close the other app.<sup>[1]</sup> If microphone permission has been revoked, the keyboard directs you to Settings then Privacy and Security then Microphone to re-enable it.<sup>[1]</sup>

The keyboard also has a battery story. Older versions drained roughly 40% per hour; recent updates brought that down to approximately 5% per hour.<sup>[1]</sup> If battery usage still seems high, update to the latest version from the App Store.

## Key Points

- The Keyboard Detour is the defining constraint of iOS: Flow is a keyboard you switch to, not a system-wide service you summon.
- The Action Button and Siri Shortcuts are the two fastest ways to reduce globe-key switching friction on supported hardware.
- Full Access must be enabled for the keyboard to dictate; without it, the keyboard loads but does nothing useful.
- iOS 26.4 introduced a manual swipe-back requirement and removed per-app style auto-adjustment; both have shipped mitigations.
- Restoring App Store purchases requires the correct Apple ID and the original Wispr Flow account; subscriptions cannot be transferred between accounts.
