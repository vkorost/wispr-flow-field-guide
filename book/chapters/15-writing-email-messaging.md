# Chapter 15: Writing, Email, and Messaging

*In this chapter: Flow does not require you to dictate into the app that has focus. Direct Routing lets you bind shortcuts that send dictation straight to Slack, email, or your calendar, while Flow also handles awkward insertion points like Outlook on iOS, Android notification reply boxes, and browser address bars. The chapter covers the shortcut system, Outlook across all four platforms, and the Android-only surfaces where the Flow Bubble reaches into places a keyboard normally owns.*

Most humans treat dictation as a two-step process. Speak, then paste. The assumption baked into that workflow is that you dictate wherever your cursor happens to be, and if you want the text somewhere else, you move it yourself. Flow can do better than that. On Mac and Windows, you can bind a shortcut that fires dictation and routes the result to a specific destination without you touching the target app first. Slack gets a shortcut. Email gets a shortcut. Your calendar gets a shortcut. The text arrives where it belongs because you told Flow where to put it before you opened your mouth.

That is Direct Routing: the principle that dictation should target a destination, not just a cursor.

The rest of this chapter covers three surfaces. First, the shortcut system that makes Direct Routing work on desktop. Second, Outlook, because email is where most humans spend their dictation budget and Outlook has platform-specific friction on every operating system. Third, Android's notification reply boxes and browser address bars, where Flow reaches into surfaces that were never designed for third-party input.

## The Shortcut System

Flow's shortcut configuration lives in Settings, then General, then Shortcuts. Open the Shortcuts dialog and you see a row for each configurable action: push-to-talk, hands-free mode, enter rebind, Command Mode, paste last transcript, copy last transcript, and cancel.<sup>[1]</sup> Each row accepts up to four bindings, so you can have one shortcut on the laptop keyboard, another on an external keyboard, a third on a mouse button, and still have a slot left over.<sup>[1]</sup>

The rules are simple. A shortcut must contain three or fewer keys and include at least one modifier, with the single exception of Esc for cancel.<sup>[1]</sup> Reserved or OS-level shortcuts are blocked with an error. If your hands-free shortcut overlaps with your push-to-talk shortcut, Flow warns you. And the Reset to default button restores everything if you make a mess of it.

Mouse buttons work. Bind a side button on a gaming mouse to push-to-talk and you can dictate while scrolling through reference material without lifting a finger off the mouse. One notable exception: Logitech MX Master side buttons cannot be bound through Logi Options+.<sup>[1]</sup> If you use that mouse, you need a different button or a different binding path.

Double-tapping your push-to-talk shortcut locks into hands-free mode; triple-tapping dismisses it.<sup>[1]</sup> That interaction builds on the Trigger Discipline model from Chapter 2, so it will feel familiar if you have already practiced the hold-versus-tap distinction.

The shortcut system is available on Mac and Windows only.<sup>[1]</sup> Mobile platforms handle routing differently, as you will see in the sections below.

### Best Practices for Shortcuts

Start with the defaults and change only shortcuts that conflict with apps you use daily. Use a mouse button for push-to-talk if you dictate while reading or scrolling. Keep cancel bound to Esc so stopping a runaway dictation never requires you to think about which key to press.

## Outlook Across Four Platforms

Outlook is the single app most likely to be open when you start dictating a professional message, and Flow works with every flavor of it: classic Outlook, the new Outlook for Windows, Outlook on the web, and Outlook's mobile apps on iOS and Android.<sup>[2]</sup> The steps are nearly identical across platforms, but the friction points are not.

### Mac

Flow works with Outlook for Mac out of the box. Open Outlook, click into the email body (confirm the cursor is blinking), hold your Flow hotkey, speak, and release. Text pastes within a second.<sup>[2]</sup> If you are using an external keyboard without an Fn key, Flow configures Ctrl+Option as your default hotkey during setup. For longer emails, hands-free mode (Fn+Space to start, then Fn or Fn+Space again to stop) avoids the fatigue of holding a key through multiple paragraphs.

### Windows

Flow works with both the classic Outlook app and the new Outlook for Windows.<sup>[2]</sup> The default hotkey is Ctrl+Win. If paste is delayed in Outlook, restarting the app or running Flow as Administrator usually resolves it. The classic Windows Outlook app can process paste commands slowly; if text appears within a few seconds, that is normal behavior, not a failure.<sup>[2]</sup>

### iOS

On iOS, Flow uses the Flow Keyboard to dictate into Outlook. Switch to the Flow Keyboard via the globe icon, tap the microphone, and dictate.<sup>[2]</sup> The keyboard requires Full Access and Microphone permission.

Here is the friction. Some corporate Outlook configurations block third-party keyboards entirely. If you work for an organization that enforces this, the Flow Keyboard will not appear.<sup>[2]</sup> The workaround is Quick Dictation to Clipboard using the Action Button (available on iPhone 15 Pro/Pro Max and all iPhone 16 and 17 models), then tap and hold in the email body and paste.<sup>[2]</sup> That is two more steps than a desktop user faces, but it is the path that works when your IT department has locked down the keyboard. The Keyboard Detour introduced in Chapter 5 explains the broader iOS keyboard setup; this is the specific case where corporate policy adds a detour on top of the detour.

The Flow Keyboard automatically switches to your default keyboard in email address fields (To, CC, BCC), number and phone fields, and punctuation-only fields.<sup>[2]</sup> You do not need to switch manually when tabbing between the body and the recipient line.

### Android

On Android, the Flow Bubble overlay handles dictation into Outlook. Tap the email body, tap the bubble (or long-press and hold to dictate, release to stop), and Flow transcribes and pastes.<sup>[2]</sup> The Floating Bubble introduced in Chapter 6 covers the full setup; inside Outlook it works like any other text field.

### Outlook on the Web

Flow works with Outlook on the web (outlook.office.com) through a desktop browser. Click into the email body, hold your hotkey, dictate, and release.<sup>[2]</sup> Smart Formatting applies automatically, adding punctuation, capitalization, paragraph breaks, and list formatting where appropriate.

### When Outlook Does Not Cooperate

If Flow shows a transcription but text does not appear in Outlook, the problem is almost always focus. Outlook was not accepting the paste because the cursor was not in the right field.<sup>[2]</sup> Click directly in the email body (not just the Outlook window), confirm the cursor is blinking, and try again. If that fails, paste the last transcript manually with Cmd+Ctrl+V on Mac or Shift+Alt+Z on Windows.<sup>[2]</sup>

On Mac, paste failures can also mean the Accessibility permission is missing or toggled off. Confirm Wispr Flow is listed and enabled in System Settings, then Privacy and Security, then Accessibility.<sup>[2]</sup> Flow notifies you if this permission is missing and opens the correct settings page.

If paste fails entirely, Flow opens the Scratchpad with your transcribed text so nothing is lost.<sup>[2]</sup> The transcript is also copied to your clipboard.

One more note: Outlook controls font styling in emails. Flow cannot dictate in specific fonts.<sup>[2]</sup> Dictate first, then format using Outlook's toolbar.

### Desktop Session Limits in Outlook

Desktop dictation sessions have a maximum duration of 20 minutes, with a warning at 19 minutes.<sup>[2]</sup> That limit is a property of the dictation model (see Trigger Discipline in Chapter 2), not an Outlook-specific constraint. It applies in every app, but it surfaces most often in email because long professional messages push humans toward the ceiling.

## Android: Notification Replies and Browser Address Bars

Android has two surfaces that no other platform offers: notification inline reply boxes and browser address bars.<sup>[3]</sup> Both are places where the Flow Bubble appears automatically when you tap into a supported field.

### Notification Inline Replies

Expand a notification to reveal its reply box, and the Flow Bubble appears. Dictate your reply, tap the checkmark, and send without ever opening the source app.<sup>[3]</sup> This works on Pixel, Samsung, Xiaomi, OPPO, OnePlus, Vivo, Asus, and other major Android devices. Any app that provides a standard inline reply box in the system notification shade is supported: WhatsApp, Telegram, Messenger, Signal, Slack, and others.<sup>[3]</sup>

If you have already typed something into a notification reply box before activating Flow, that text is preserved. Dictated text inserts at the cursor position.<sup>[3]</sup>

A warning: avoid dictating sensitive information into notification replies. In some notification reply contexts, fields that would otherwise be excluded (PIN or password fields) may be reachable.<sup>[3]</sup>

### Browser Address Bars

Tap the address bar in Chrome, Firefox, Edge, Brave, or Samsung Internet, and the Flow Bubble appears.<sup>[3]</sup> Speak a URL or search phrase and Flow types it in. The supported browser list also includes Opera, Vivaldi, DuckDuckGo, Kiwi, UC Browser, and Yandex. Browsers that do not use standard URL input fields may not show the bubble.<sup>[3]</sup>

The Google search box on google.com and Chrome's new tab page is a separate field from the address bar, and it is also supported. In earlier versions, dictation could fail to insert text in Chrome and Chromium search boxes; that was fixed in version 2.0.1 (as of Q2 2026).<sup>[3]</sup>

### Session Limits in These Surfaces

A warning appears at about 4 minutes and dictation stops automatically at about 5 minutes in notification replies and address bars.<sup>[3]</sup> That is the same 5-minute limit that applies to these Android surfaces specifically, distinct from the desktop 20-minute ceiling.

### What the Bubble Will Not Enter

The Flow Bubble does not appear in password, PIN, phone-number, or numeric-only fields.<sup>[3]</sup> That is a safety behavior, not a bug. The bubble also does not appear in banking or financial apps; that restriction is covered in Chapter 6 (The Floating Bubble) and Chapter 17 (The Insertion Boundary).

No new permissions are required for these surfaces. If Flow is running with the permissions granted during initial setup, notification replies and address bars activate automatically.<sup>[3]</sup>

## Key Points

- Direct Routing means binding shortcuts so dictation targets a destination app, removing the extra step of navigating there first.
- Outlook works on every platform, but corporate iOS configurations may block the Flow Keyboard; Quick Dictation to Clipboard is the workaround.
- Desktop shortcuts accept up to four bindings per action, including mouse buttons, with a three-key maximum and at least one modifier required.
- Android uniquely supports dictation into notification reply boxes and browser address bars through the Flow Bubble overlay.
- Sensitive fields (passwords, PINs, phone numbers) are excluded from bubble activation on Android, a safety guardrail worth knowing about.
