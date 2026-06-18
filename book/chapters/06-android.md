# Android

*In this chapter: Flow on Android is a floating bubble, not a keyboard. The make-or-break setup involves three permissions and a battery exemption that varies by manufacturer, and the reward is a dictation surface that works inside any text field without switching input methods. This chapter covers installation, the bubble's behavior, customization, and the Android-specific constraints that shape the experience.*

On every other platform in this book, you either press a hotkey or switch to a keyboard to start dictating. On Android, Flow presents itself as a floating circle that hovers above your existing keyboard. You do not replace your keyboard. You do not memorize a key combination. You tap a bubble, speak, and tap a checkmark. The Floating Bubble is the defining interaction on Android, and everything about the platform experience follows from it.

The bubble works because Android allows apps to draw over other apps and to use an accessibility service for inserting text into foreign input fields. Those two capabilities give Flow its power and impose its costs. Setup is not difficult, but it is specific. Skip a permission or ignore a battery setting, and the bubble disappears when you need it most.

## Installation

Flow is available from the Google Play Store. Search for "Wispr Flow," verify the developer is "Wispr Inc," and install.<sup>[1]</sup> The package ID for the official app is `com.wispr.flowapp`. This matters because fake apps have appeared on the Play Store, impersonating Flow with misspelled names like "Whisper Flow" or offering in-app purchases that the official app does not sell. The real app handles subscriptions through wisprflow.ai, not through Google Play billing. If an Android app calling itself Wispr Flow asks you to pay inside the app, it is not the real one.<sup>[2]</sup>

System requirements are straightforward: Android 13 or later, an internet connection (offline transcription is not available), free storage, and an accelerometer sensor.<sup>[3]</sup> The accelerometer requirement is not decorative; it powers the shake-to-unsnooze gesture covered later. Devices without an accelerometer are blocked from installing via the Play Store.<sup>[3]</sup> The app supports smartphones, tablets, foldables (the bubble adjusts position when transitioning between screens), and Chromebooks that run Android apps on Android 13 or higher.<sup>[3]</sup>

Android 12 is not supported. Android Go devices are not officially supported either; limited RAM causes reduced performance or instability.<sup>[3]</sup>

## The Permission Triad

Flow on Android requires three core permissions, each serving a distinct purpose.<sup>[4,5]</sup>

**Display over other apps (overlay).** This is what lets the bubble exist at all. Without it, there is no floating circle, no dictation trigger, nothing visible. Android prompts you to grant this during onboarding; tap "Open Settings," toggle it on, and Flow detects the change and returns to the foreground automatically.<sup>[1]</sup>

**Accessibility service.** This is how Flow reads which text field has focus and inserts dictated text into it. Without accessibility, the bubble can appear but cannot paste anything. During setup, Flow shows a legal consent screen with "Agree" and "Not now" options before sending you to Android's Accessibility Settings.<sup>[1,4]</sup> The exact location of the toggle varies by manufacturer: Samsung lists it under "Installed apps," Xiaomi adds an extra confirmation dialog, Vivo and Motorola show it directly in the list, and most others (Pixel, OnePlus, Realme) put it under "Downloaded apps."<sup>[4,6]</sup>

One critical warning: do not enable the Wispr Flow *shortcut* in Accessibility Settings. Only enable the main accessibility service toggle. Enabling the shortcut causes an error screen titled "Oops, something isn't right." If you accidentally toggle it on, turn it off, then enable the main service toggle, and Flow resumes setup automatically.<sup>[1,6]</sup>

**Microphone.** Android prompts for this the first time you tap the bubble to record. Choose "While using the app" or "Only this time." If you previously denied it, navigate to Settings, then Apps, then Wispr Flow, then Permissions, and enable Microphone manually.<sup>[4]</sup>

## The Battery Problem

This is where Android gets manufacturer-specific, and where the most setup failures happen. Aggressive battery management on many Android devices will kill Flow's background service, causing the bubble to vanish. A battery optimization exemption is strongly recommended (though technically optional during onboarding).<sup>[1,4]</sup>

The paths differ by manufacturer:

**Samsung (One UI):** Set Wispr Flow's battery to "Unrestricted" in Settings, then Apps, then Wispr Flow, then Battery. Add it to "Never sleeping apps" under Background usage limits. Disable "Put unused apps to sleep."<sup>[4,5]</sup>

**Xiaomi, Redmi, POCO (MIUI/HyperOS):** Two separate steps are required, and both are mandatory. Enable Autostart for Wispr Flow, and set Battery saver to "No restrictions." Skipping either step causes Flow to disconnect when you switch apps.<sup>[4,5]</sup>

**Huawei and Honor:** Set battery optimization to "Don't allow."<sup>[4]</sup>

**Oppo:** Enable "Allow Auto-Launch" and "Allow Background Activity," and disable power saving mode or add Flow to its exceptions.<sup>[4,5]</sup>

**Vivo:** Enable Autostart, lock Flow in recent apps, and set the standard battery exemption.<sup>[4,5]</sup>

**OnePlus, Motorola/Lenovo, Transsion (Tecno, Infinix, itel):** Disable battery optimization (set to "Don't optimize").<sup>[4,5]</sup>

**Realme:** Set battery optimization to "Not optimized."<sup>[4,5]</sup>

**Google Pixel and stock Android:** No manufacturer-specific steps required.<sup>[4]</sup>

If the system does kill Flow in the background, the app restarts automatically the next time you bring it to the foreground, provided you are signed in and accessibility is still enabled.<sup>[3]</sup> Flow also starts automatically on device boot when accessibility permission is granted.<sup>[3,4]</sup>

## Your First Dictation

With permissions granted, open any app with a text field. Tap into it so the on-screen keyboard appears. The Flow Bubble shows up along the left or right edge of your screen as soon as the keyboard starts opening.<sup>[5]</sup>

Two modes are available:

**Tap Mode:** Tap the bubble once to start recording. You hear a sound, see a live waveform, and speak at a natural pace. Tap the checkmark to insert the text.<sup>[5]</sup>

**Hold Mode (Push-to-Talk):** Press and hold the bubble. Speak while your finger is down. Release to insert. Best for quick messages.<sup>[5]</sup>

There is no Android equivalent to desktop's double-tap hands-free mode. Starting dictation always requires physically tapping or holding the bubble.<sup>[5]</sup>

Flow inserts text directly in popular messaging apps, including WhatsApp, Telegram, Messenger, Instagram, Microsoft Teams, Signal, Slack, Discord, Snapchat, Google Messages, and Gmail, without requiring a manual paste.<sup>[5,7]</sup> In apps where direct insertion cannot be verified, Flow falls back to the clipboard and shows a notification so you can paste manually.<sup>[4,5]</sup>

The bubble also works in notification reply boxes (inline replies from the notification shade, preserving any text you have already typed) and in browser address bars across Chrome, Firefox, Edge, Brave, Samsung Internet, Opera, and many other Chromium-based browsers.<sup>[5]</sup>

## Where the Bubble Hides

The bubble is intentionally suppressed in three contexts:<sup>[5]</sup>

1. **Password fields, PIN fields, and numeric-only inputs.** For security.
2. **Banking and financial apps.** Flow automatically detects over 100 banking and financial apps (the figure appears in the Banking App Detection article<sup>[8]</sup>) across multiple regions (United States, India, United Kingdom, Europe, Asia, Latin America, Canada, and others) and hides the bubble entirely while they are in the foreground.<sup>[8]</sup> This behavior cannot be disabled. While a banking app is active, all activation methods are blocked, context awareness is suppressed, and a one-time toast confirms "Flow Bubble is disabled inside banking apps" if you try to type.<sup>[8]</sup> Dictation in progress when a banking app opens is stopped, and the transcript is copied to the clipboard for manual pasting.<sup>[8]</sup>
3. **No on-screen keyboard.** If you are using an external keyboard or the soft keyboard is collapsed, the bubble does not appear.<sup>[5]</sup>

## Session Limits

Android dictation sessions are capped at five minutes (as of Q2 2026).<sup>[9]</sup> At approximately four minutes, a toast notification with haptic feedback warns you that one minute remains. At five minutes, the session ends automatically and Flow submits the transcription. A confirmation toast and system notification confirm the session has ended.<sup>[9]</sup>

This differs from desktop, where sessions run up to 20 minutes. On Android, break longer dictations into multiple sessions; finish a thought, let it submit, and start a new one immediately.<sup>[9]</sup>

An earlier version of the documentation described Android as having no fixed maximum session duration. The Android-specific documentation updated in 2026 now consistently states a five-minute cap, so treat the older "no maximum" claim as superseded.

## Customizing the Bubble

The bubble offers more visual control than you might expect.

**Size.** Four presets (0.7x, 0.85x, 1.0x, 1.15x) are available in Settings, then Flow Bubble Size, with a live preview and a Reset button.<sup>[10]</sup>

**Opacity.** Five steps from 20% to 100% (default 80%) in Settings, then Flow Bubble Opacity, also with a Reset button.<sup>[1,10]</sup>

**Shrink behavior.** Three toggles control auto-shrink:<sup>[10]</sup>

- *Shrink the bubble when not in use* (master toggle): reduces the bubble to a smaller icon after five seconds of inactivity.
- *Shrink to a dot*: makes the idle bubble nearly invisible.
- *Shrink in search fields*: shrinks the bubble instantly when your cursor is in a search or filter input, so it does not overlap autocomplete.

The sub-options only activate when the master toggle is on. Turning the master toggle off grays them out but preserves your selections.<sup>[10]</sup> Tapping a shrunken bubble restores it to full size and starts dictation in a single gesture.<sup>[10]</sup>

All bubble preferences (size, opacity, shrink settings) are saved per account. Signing out and back in restores them; a different account on the same device starts with defaults.<sup>[10]</sup>

## Snooze

Sometimes you need the bubble gone entirely: for a screenshot, a full-screen video, or a focused reading session. Drag the bubble toward the bottom of the screen. A dark gradient fades in, a drop target expands with haptic feedback, and when you release into it, the bubble disappears for 10 minutes. A toast confirms: "Wispr Flow is snoozed for 10 min. Shake your phone to bring it back."<sup>[11]</sup>

To bring it back early, shake your phone firmly back and forth a couple of times while the phone is unlocked. The bubble reappears with haptic feedback and a "Wispr Flow is back!" confirmation. You can also open the app and tap "End snooze now" on the home screen; the bubble returns the next time you tap into a text field.<sup>[11]</sup>

Snooze specifics worth knowing:<sup>[11]</sup>

- Snoozing stops any active dictation and releases the microphone. The mic does not continue recording in the background.
- Opening the keyboard while snoozed will not bring the bubble back.
- Snooze is fixed at 10 minutes. No configuration option exists.
- Snooze is unavailable while the accessibility repair prompt is showing. If accessibility is lost during a snooze, snooze is auto-cancelled so the repair prompt becomes visible.
- A single light shake will not trigger unsnooze. It takes a firm back-and-forth motion.
- Shake-to-unsnooze is blocked inside banking apps.

## Work Profiles and Account Switching

Flow works on Android work profiles, though accessibility toggle placement varies by device and some MDM configurations may restrict the required permissions.<sup>[6]</sup> Full enterprise management and MDM deployment on Android are not currently available; for managed deployments, Wispr Flow supports macOS and Windows via tools like Jamf, Kandji, and Intune.<sup>[6]</sup>

Switching accounts on Android is straightforward: open the app, go to Account, and tap Sign out. Confirm in the dialog (you will see a warning that signing out deletes all locally stored transcripts), then sign in with a different account.<sup>[12]</sup> Each account keeps its own settings, and the previous account's transcripts and audio are cleared when a new account signs in. Signing back in as the same user restores your settings and keeps transcription history intact.<sup>[12]</sup>

## Language Selection

Android does not offer Auto-detect for languages. You must select at least one specific language in Settings, then Languages, then tap Add more, select your choices, and tap Done and Save. Exiting without tapping Save discards the change.<sup>[1]</sup>

This is a real constraint for multilingual users. On desktop, the Flow Bar provides a one-click language picker; on Android, you navigate through the settings screen. Russian is listed as a supported language, and the Russian Google Play listing describes Flow as working well with Russian punctuation. However, the quality of Russian dictation on Android and the behavior of Cyrillic characters in dictionary entries are not documented with enough specificity to make a verdict. Treat both as test-it: verify on your own device whether Russian transcription meets your accuracy needs and whether Cyrillic dictionary entries are accepted and applied correctly during dictation.

## What Android Does Not Have

Several desktop features are absent on Android as of Q2 2026:

- **Command Mode** (voice commands for text editing like "select all," "copy," "bold") is desktop-only. No Android UI or gesture exists for invoking it.
- **Starring and sorting dictionary entries** are not available. Replacement rules can only be created on desktop or iOS; Android applies those rules during dictation but cannot create them.<sup>[1]</sup>
- **Bulk import** of dictionary items or snippets is desktop-only.<sup>[1]</sup>
- **Auto-detect language** is unavailable; you must manually select languages.
- **The Flow Bar language picker** does not exist; language switching uses the settings screen.
- **20-minute sessions** are desktop-only; Android enforces five minutes.<sup>[9]</sup>
- **In-app subscription management** is not available on Android. Subscriptions are purchased and managed through wisprflow.ai (or through the iOS App Store for iOS users).<sup>[2]</sup>

Dictionary and snippets do sync to Android: dictionary entries sync each time you open the Dictionary tab, and snippets sync each time you open the Snippets tab.<sup>[1]</sup> Voice-triggered snippet expansion during dictation may work on Android (earlier Android betas did not support it, and documented fixes were released, but current behavior is not confirmed in the available documentation; test on your own device). Android uniquely enforces a cross-validation rule: a word cannot be used as both a dictionary entry and a snippet trigger. On desktop and iOS, this validation is not yet enforced at entry time (inferred from research; mark this claim as such).

## Key Points

- The Floating Bubble is an overlay, not a keyboard replacement; it requires three permissions (overlay, accessibility, microphone) and a per-manufacturer battery exemption to stay alive.
- Aggressive battery management on Samsung, Xiaomi, Huawei, Oppo, Vivo, and similar devices is the most common cause of the bubble disappearing; the fix is manufacturer-specific.
- Android dictation sessions are capped at five minutes with a one-minute warning; break longer thoughts into multiple sessions.
- The bubble is automatically hidden in banking and financial apps, password fields, and numeric inputs; this behavior cannot be overridden.
- Snooze hides the bubble for 10 minutes; shake your phone firmly to bring it back early.
- Russian dictation quality and Cyrillic dictionary behavior on Android are undocumented with enough precision to make a verdict; test both on your own device.
