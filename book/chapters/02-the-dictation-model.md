# The Dictation Model

*In this chapter, we explore the physical act of starting and stopping Flow: the hotkey hold, the hands-free lock, and the whisper mode that lets you dictate in a shared office. Choosing the right trigger for the moment is a skill unto itself, one that determines whether Flow feels like an extension of your voice or a clumsy interruption.*

You installed Flow. You granted permissions. You see the Flow Bar sitting at the center of your screen, politely waiting. Now what?

You press a key, you talk, and you let go. That is the entire interaction in its simplest form. But "press a key, talk, let go" is to dictation what "move the mouse and click" is to computing. The description is accurate. It is also nearly useless as guidance for someone who needs to dictate a three-paragraph email while standing in line at the pharmacy, or capture a ten-minute product spec while pacing their living room, or whisper a reply during a meeting without the person next to them noticing.

Flow gives you three distinct ways to start dictating. Each fits a different posture, a different context, a different level of ambient noise. Learning when to reach for which one is the core skill of this chapter. Call it Trigger Discipline.

## Push-to-Talk: The Default

Push-to-talk is the mode you meet on day one. On Mac, the default hotkey is Fn. On Windows, it is Ctrl + Win.<sup>[1]</sup> You hold the key, you speak, and you release. Flow captures the audio while the key is down, sends it to the cloud for processing, and pastes the formatted result into whatever text field had focus when you started.<sup>[1]</sup>

The interaction has a physical feel to it, like a walkie-talkie. Hold to transmit. Release to send. That physicality is the point: your finger on the key is an unambiguous signal to the system (and to yourself) that you are dictating, not thinking aloud.

A few details matter more than you would expect.

### The Brief-Hold Cancel

On Mac, holding Fn for less than roughly half a second registers as a tap, not a hold, and Flow cancels the session.<sup>[1]</sup> This is a feature, not a bug. The Fn key serves double duty on Apple keyboards, and Flow needs to distinguish between "I want to dictate" and "I tapped Fn while reaching for a function key." The threshold is short enough that you will rarely hit it on purpose, but if you are a fast-twitch person who jabs and releases, you will wonder why nothing happened.

Slow down the press. Give it a beat. You are starting a conversation with a cloud-hosted language model; it can afford half a second of your time.

### The Visual Handshake

When Flow begins listening, it shows a white animated waveform on the Flow Bar. When it detects your voice, the bar turns blue.<sup>[1]</sup> This two-state feedback is your confirmation that the mic is live and that the system is receiving signal. White bars that never turn blue mean the mic is picking up silence; check your input device. No bars at all means the hotkey did not register; check your shortcut settings.

There is also an auditory cue. Flow plays a ping when recording starts and a paste sound when your text is submitted, provided you have Sound Effects enabled in Settings.<sup>[1]</sup> If you dictate in environments where you cannot watch the screen (standing at a whiteboard, pacing a room), the ping is your confirmation that the session is live. No ping, no session.

You can also start a dictation session by clicking the Flow Bar directly, without touching a hotkey at all.<sup>[1]</sup> This is useful when you have reassigned Fn to something else, or when you are orienting a new user who is not yet comfortable with the hotkey. Click the bar, wait for the ping or the moving white bars, and speak.

### Escape as Cancel

Press Esc while dictating and Flow kills the session.<sup>[1]</sup> The text is not transcribed. On Mac and Windows, the audio is saved to Recent Activity if it was long enough to be useful, so you can recover it later if you change your mind.<sup>[1]</sup> This is a quiet safety net: if you start dictating and immediately realize you are in the wrong app or the wrong meeting context, Esc bails you out without leaving a trace in the text field.

### The "Still Processing" Gate

If you try to start a new session while a previous transcript is still being processed, Flow blocks the attempt and shows a notification: "Flow was processing your last transcript."<sup>[1]</sup> Dismiss the notification, wait for the processing to finish (usually a few seconds), and press your hotkey again. You can also click Cancel in the notification to abandon the in-progress transcription and start fresh.<sup>[1]</sup>

This is worth knowing because it explains a specific frustration: you release the hotkey, immediately press it again for a second dictation, and nothing happens. Flow is not ignoring you. It is finishing the previous job. The pipeline is sequential, not parallel.

## Hands-Free: The Long-Form Mode

Push-to-talk works beautifully for a sentence or a paragraph. For a long email, a journal entry, or a product specification, holding a key for several minutes gets uncomfortable. That is where hands-free mode comes in.

On Mac, press Fn + Space. On Windows, press Ctrl + Win + Space.<sup>[2]</sup> Flow locks into continuous recording. You take your hands off the keyboard, lean back, and talk. When you are finished, press the same shortcut again (or click the stop icon in the Flow Bar) and Flow pastes the result.<sup>[2]</sup>

The mental shift from push-to-talk to hands-free is nontrivial. In push-to-talk, the key under your finger is a constant physical reminder that you are recording. In hands-free, that reminder vanishes. You need to build a new habit: glance at the Flow Bar. If the waveform is moving, you are live. If you forget you are recording, you may dictate an aside to your dog that ends up in the quarterly review.

### The Flow Bar Asymmetry

One behavioral note catches people: during hands-free dictation, clicking the Flow Bar does not stop your recording.<sup>[2]</sup> Use the stop or cancel buttons, or press your hands-free shortcut key. During push-to-talk, clicking the Flow Bar does end the session, which is the opposite behavior. The distinction is deliberate. Hands-free sessions are meant to be long, so an accidental click should not cut you off. Push-to-talk sessions are short, so a click is a convenient way to finish. The logic is sound, but the asymmetry trips up users who switch between modes without thinking about it.

### "Press Enter" Without Touching the Keyboard

Here is a detail that turns hands-free dictation from convenient to genuinely hands-free: say "press enter" at the very end of your dictation and Flow presses the Enter key after pasting your text.<sup>[2]</sup> The words "press enter" are stripped from your transcript. This is useful for sending messages in Slack, submitting prompts in a chat interface, or any context where you need to hit Enter after your text lands.

The phrase is only recognized at the end of your dictation. If you say it in the middle of a sentence, it appears as regular text.<sup>[2]</sup> The first time Flow detects the phrase, a one-time notification explains the feature and asks you to confirm.<sup>[2]</sup> After that, it works silently.

### The iOS Path

iOS does not support keyboard shortcuts for hands-free dictation.<sup>[2]</sup> Instead, you tap the microphone button on the Flow Keyboard, speak, and tap the check button when done.<sup>[1]</sup> For a more hands-free experience, Siri can start Flow for you: say "Quick dictate to notes with Flow" or "Dictate with Flow" to begin a session that runs through Flow's own speech recognition.<sup>[2]</sup> A separate Siri phrase, "Save Flow note," uses Siri's built-in speech recognition instead of Flow's, which produces different results. Several Siri Shortcuts are available automatically upon installation, requiring no manual setup; Chapter 5 (The Keyboard Detour) covers the full list and configuration.

The iOS path is covered in depth in Chapter 5 (The Keyboard Detour). What matters here is the principle: on iOS, the trigger is a tap or a Siri phrase, not a hardware key.

### The Android Path

On Android, the trigger is the Flow Bubble, a floating overlay that appears when the on-screen keyboard opens.<sup>[1]</sup> You can tap it once to start a tap-to-dictate session (tap the checkmark when done), or long-press it for hold-to-dictate (release to submit).<sup>[2]</sup> There is no hardware hotkey equivalent. The Bubble is suppressed in password fields, phone-number fields, and numeric inputs, and it hides itself entirely inside banking and financial apps.<sup>[1]</sup>

After a successful dictation, a copy-to-clipboard button appears next to the Bubble for five seconds.<sup>[2]</sup> If Flow cannot insert text into the active field (some apps resist), the Bubble shows a Paste button so you can paste from the clipboard manually.<sup>[1]</sup> Your dictation is never lost.

Android has no equivalent of the iOS Siri trigger.<sup>[2]</sup> The Bubble is the one entry point, and it only appears when the on-screen keyboard is visible. If you are using an external hardware keyboard with your Android device, the on-screen keyboard does not open, and the Bubble does not appear.<sup>[3]</sup>

The Android path gets its own chapter (Chapter 6, The Floating Bubble). For Trigger Discipline purposes, the key point is that Android users must be comfortable with the Bubble as their primary and only entry point.

## Session Limits: The Clock You Cannot Ignore

Every dictation session has a ceiling.

On Mac and Windows, the maximum is 20 minutes. At the 19-minute mark, Flow displays a warning: "You have less than 1 minute left before you reach the 20 minute limit!"<sup>[4]</sup> At 20 minutes, the session ends automatically. Flow transcribes what you said and pastes it into the active text field. A notification titled "Transcription session ended" confirms what happened and includes a "Recover text" button that re-pastes the transcript.<sup>[4]</sup>

The 20-minute limit applies to both Basic (free) and Pro plans.<sup>[4]</sup> There is no cooldown between sessions: once the previous transcript finishes processing (usually a few seconds), you can press your hotkey and start again.<sup>[4]</sup> In practice, this means the 20-minute limit is not a wall so much as a mandatory breath. You dictate for 20 minutes, wait a few seconds, and pick up where you left off.

On Android, the session limit is 5 minutes.<sup>[5]</sup> About a minute before the limit, a toast notification appears with haptic feedback: "1 minute left before you reach the 5-minute limit."<sup>[5]</sup> At 5 minutes, the session stops and submits automatically; your audio is preserved and transcribed normally.<sup>[2]</sup> A toast message and a system notification confirm the session has ended.<sup>[5]</sup>

On iOS, the session limit is also 5 minutes.<sup>[5]</sup> Unlike Android, iOS shows no advance warning. At 5 minutes, the session simply stops and submits your transcription automatically.<sup>[5]</sup>

These numbers are worth committing to memory. If you are a desktop user dictating a long document, the 20-minute wall is generous but real. Plan your natural breaks around it. On mobile, whether iOS or Android, five minutes goes fast when you are thinking aloud; structure your dictation into shorter bursts rather than one unbroken monologue. On iOS, the absence of an advance warning makes this discipline especially important. You will not get a tap on the shoulder before the clock runs out.

Note that session limits are separate from the weekly word cap on free-tier accounts (covered in Chapter 19, The Word Budget). A session limit is about continuous recording time. The word cap is about total output volume per week. You can hit one without hitting the other.

## Discreet and Whisper Input

Sometimes you need to dictate in a space where speaking at full volume would be inappropriate or conspicuous. Flow handles low-volume input, but the accuracy trade-off is real.

In a quiet room, whispering works well. The cloud-based speech recognition model can resolve low-volume phonemes when there is minimal competing noise. In a noisy environment (a coffee shop, an open-plan office, a conference hallway), the accuracy drops significantly. The system struggles to isolate a whisper from background noise, and you will see more misrecognized words in the output. This is a physics problem, not a software problem: the signal-to-noise ratio determines what the model has to work with, and a whisper in noise is a weak signal.

Microphone choice matters here more than anywhere else in your Flow setup. A close-range mic (a clip-on lavalier, a boom headset) captures your whisper with less room noise than a laptop's built-in mic sitting twelve inches from your mouth. Chapter 18 (The Input Chain) covers hardware selection in detail. For Trigger Discipline purposes, the principle is: if you plan to whisper regularly, invest in a mic that sits close to your lips.

The accuracy of whisper-mode dictation is something you should test on your own device, in your own typical environment, before relying on it for production work. Results vary enough by hardware and ambient conditions that a blanket quality verdict would be misleading.

## Customizing Your Triggers

Flow does not lock you into the default hotkeys. On Mac and Windows, you can reassign both the push-to-talk and hands-free shortcuts in Settings, under General, then Shortcuts.<sup>[2]</sup> Each action can have up to four different shortcuts assigned, and each shortcut can contain up to three keys (keyboard keys and mouse buttons combined).<sup>[1]</sup>

Mouse buttons are valid triggers. You can bind Middle Click, Mouse 4, Mouse 5, or an Aux Button entry for mice that send extra button codes.<sup>[1]</sup> You can also combine a keyboard modifier with a mouse button (Ctrl + Mouse 4, for example). Left click and right click cannot be used as triggers.<sup>[1]</sup> When a mouse button is assigned as a dictation trigger, it no longer performs its default action in other apps; Mouse 4 will not trigger browser back navigation, for instance.<sup>[1]</sup> Some Logitech mice using Logi Options+ may not support Mouse 4 or Mouse 5 for push-to-talk, because the driver remaps those buttons to trackpad gestures.<sup>[1]</sup>

If your push-to-talk shortcut overlaps with your hands-free shortcut, Flow shows a five-second warning toast.<sup>[2]</sup> This is worth watching for: overlapping shortcuts cause unpredictable behavior where pressing one trigger activates the wrong mode. The fix is simple. Open the Shortcuts dialog, check that your push-to-talk and hands-free bindings do not share key combinations, and use "Reset to default" if you have tangled things beyond easy repair.<sup>[2]</sup>

On iOS, hardware keyboard shortcuts are not supported. The triggers are the microphone button on the Flow Keyboard, the Action Button (iPhone 15 Pro and later), Siri Shortcuts, and home screen widgets.<sup>[2]</sup> On Android, the trigger is always the Flow Bubble.

If your Mac does not have an Fn key (some external keyboards omit it), Flow assigns Ctrl + Option as the default push-to-talk hotkey during setup.<sup>[1]</sup> You can change this at any time.

## Accessibility: Keyboard and Screen Reader Paths

Trigger Discipline is not only about hotkeys and mouse buttons. For users who navigate by keyboard or screen reader, Flow provides a parallel set of paths.

Flow is built to be driven entirely from the keyboard. Tab moves focus between interactive elements. Space or Enter activates the focused item. Escape closes menus and returns focus to the previous element.<sup>[3]</sup> A visible focus ring shows which element is selected at any moment, so keyboard-only users always know where they are in the interface. History navigation works via Cmd+[ and Cmd+] on Mac (Ctrl+[ and Ctrl+] on Windows).<sup>[3]</sup>

Screen readers work with Flow across platforms. VoiceOver on Mac, NVDA and JAWS on Windows, and TalkBack on Android have been tested.<sup>[3]</sup> Flow uses semantic HTML and ARIA attributes, announces interactive element states (expanded, collapsed, disabled), and maintains a logical reading order. Navigation landmarks help screen reader users understand page structure without visual cues. Decorative images are hidden from screen readers to reduce noise, and disabled controls are communicated via the HTML disabled attribute and aria-disabled.<sup>[3]</sup>

Flow also respects your system's reduced-motion preference. When enabled (System Settings on Mac, Accessibility settings on Windows), animations are minimized, including the onboarding toast and the animated glow ring around the Start Flow button on the keyboard.<sup>[3]</sup> No in-app configuration is needed; Flow detects the system preference automatically.

On Android, the accessibility layer goes deeper. The Flow Bubble automatically repositions after landscape rotation. The Bubble signals connection status visually: a pulsing spinner means Flow is reconnecting; a warning triangle means accessibility permission may need re-granting.<sup>[3]</sup> Tapping the warning triangle opens the accessibility settings screen directly. On iOS, the QWERTY keyboard includes refinements for tap accuracy (gaps between keys activate the nearest key) and a globe button on smaller iPhone models for switching keyboards.<sup>[3]</sup>

A few gaps remain, as of Q2 2026. The Hub top bar (sidebar toggle, account panel, notifications) is not yet keyboard-accessible. Collapsed sidebar tooltips are mouse-only. Tab controls throughout the app are not yet keyboard-navigable. Some icon-only buttons lack accessible labels.<sup>[3]</sup> These are limitations, not showstoppers, and they are the kind of thing that gets incrementally fixed in monthly updates. But if you rely on keyboard navigation or a screen reader as your primary interface, it is worth testing your specific workflow before committing to Flow as your daily driver.

## Trigger Discipline in Practice

Trigger Discipline is not a feature you toggle on. It is a habit you develop. It means choosing push-to-talk for a quick Slack reply, switching to hands-free for a long email, whispering into a close-range mic when the open office is full, and knowing the session limits well enough that you never lose text to a timeout you did not see coming.

The three modes are not ranked. Push-to-talk is not "basic" and hands-free is not "advanced." They are tools for different contexts, and the skilled user moves between them without thinking about it, the same way a driver shifts gears without looking at the gearshift.

Consider the shape of a typical workday. Morning email triage: push-to-talk, one message at a time, hold and release. A long product brief after lunch: hands-free, twenty minutes of unbroken thinking poured into a document. A quick reply during a video call you are not leading: whisper mode with a lavalier mic clipped to your collar. Each scenario demands a different trigger, and Trigger Discipline is the instinct that selects the right one without deliberation.

The work here is building the muscle memory. That takes a week, maybe two. After that, the trigger disappears from your attention and what remains is the voice. That is the goal.

## Key Points

- Push-to-talk, hands-free, and whisper input are three distinct modes suited to different physical contexts; none is superior to the others.
- Desktop sessions cap at 20 minutes with a warning at 19; both iOS and Android cap at 5 minutes.
- On Android you receive a warning about one minute before the 5-minute limit; on iOS there is no advance warning at all.
- Hotkeys are fully customizable on desktop, including mouse buttons, with up to four shortcuts per action and three keys per shortcut.
- On iOS the trigger is a tap or a Siri phrase; on Android it is always the Flow Bubble overlay.
- Whisper dictation accuracy depends on mic proximity and ambient noise; test it in your own environment before relying on it.
- Keyboard navigation and screen reader support are built in across platforms, though some interface elements are not yet fully accessible.
