# Audio and Hardware

*In this chapter, you learn why Flow's output quality is bounded by its input quality: the microphone, its position, and its connection to the device form a chain where the weakest link determines accuracy. Choosing the right mic and configuring it correctly matters more than any software setting.*

Every dictation tool has the same dirty secret. You can tune the cleanup level, train the dictionary, configure styles for every app category, and the rewrite pass will still produce garbage if the microphone is feeding it garbage. The entire pipeline described in this book, from The Rewrite Pass (Ch1) through The Cleanup Dial (Ch7) to The App-Aware Rewrite (Ch9), runs downstream of a single physical fact: what the mic captures is all Flow has to work with.

That fact has a name. Call it The Input Chain.

The Input Chain is the path from your voice to Flow's speech recognition backend: your mouth, the air between you and the microphone, the microphone itself, the analog-to-digital conversion, and the connection (wired, Bluetooth, or built-in) that carries the signal to your device. Every link in that chain either preserves your voice or degrades it. Software cannot recover what hardware lost.

## Picking and Selecting Your Microphone

Flow gives you different levels of control over mic selection depending on your platform. On Mac and Windows, in-app mic selection lets you choose a specific input device. On iOS, a single "Use Built-In Mic" toggle is all you get. On Android, there is no in-app picker at all; the OS routes audio automatically.<sup>[1]</sup>

On desktop, the mic picker lives under Settings, then General, then Microphone, then Change. You can also right-click the Flow Bar to access it. The picker shows "Auto-detect" (follows system default), "Built-in mic (recommended)," and any connected external devices. A live volume indicator with animated bars shows whether your mic is actually capturing sound.<sup>[1]</sup>

Select your mic by name. Avoid "Auto-detect" unless you never change devices. Auto-detect follows the system default, and your system default changes every time you plug in headphones, connect a Bluetooth device, or dock your laptop. Selecting a specific mic means Flow uses that mic and only that mic until you say otherwise.<sup>[2]</sup>

On iOS, the "Use Built-In Mic" toggle in Settings controls whether Flow uses the iPhone's built-in microphone or a connected Bluetooth device. When that toggle is on, Bluetooth microphone input is excluded, though you can still hear audio through Bluetooth headphones.<sup>[1]</sup>

On Android, Flow uses whatever microphone Android routes as the default input. Connect a wired headset and Android switches to it. Pair Bluetooth headphones and Android routes through them. You have no override inside the Flow app (as of Q2 2026).<sup>[1]</sup>

Microphone changes take effect at the start of your next dictation, with no app restart needed. A brief notification confirms the new microphone the next time you dictate.<sup>[1]</sup>

## The AirPods Problem

AirPods get their own section because Flow treats them differently from every other audio device. In the Mac and Windows mic picker, AirPods are flagged with a warning symbol. That warning is not decorative. It reappears up to once per hour if you keep using them.<sup>[1]</sup>

The issue is physical. Earbud microphones sit on the cable or in the earbud housing, typically 6 to 8 inches from your lips. At that distance, a whisper barely registers above ambient noise. Wireless earbuds like AirPods and Galaxy Buds compound the problem: they compress audio over Bluetooth and introduce delay that degrades accuracy. AirPods in particular may be slow to activate the microphone, causing missed words at the start of a session.<sup>[3]</sup>

Wired earbuds are only slightly better. They avoid the Bluetooth compression, but the mic-distance problem remains.<sup>[3]</sup>

The fix is not a software setting. It is any microphone that sits within a couple of inches of your mouth. The rest of this chapter covers the options.

## Recommended Microphones

Flow's documentation recommends three categories of external microphones, each suited to a different work situation.<sup>[3]</sup>

**Clip-on lavalier mics** attach to your collar and stay close to your mouth wherever you go. The DJI Mic Mini is the top pick: tiny, wireless, with magnetic and clip-on mounts. For runners-up, the Rode Wireless GO and the budget BOYA Mini 2 both handle whisper capture well.<sup>[3]</sup>

**Attachable boom mics** clip or magnet onto headphones you already own, positioning a microphone right next to your mouth. The Antlion ModMic Uni 2+ is the recommendation: a uni-directional noise-canceling capsule on a magnetic attachment that fits any headphones. This is the setup Flow recommends during onboarding for users dictating in shared office spaces.<sup>[3]</sup>

**Podcast mics** deliver the highest audio quality for a fixed desk. The Shure MV7+ is the top pick for professional-grade close-range capture. The Elgato Wave:3 is a strong USB alternative that needs no audio interface.<sup>[3]</sup>

The pattern across all three categories is the same: get the mic close to your mouth. That single variable, distance, determines whisper accuracy more than brand, price, or connection type.

## Discreet Dictation

Whispering works. Flow's speech recognition handles whispered audio with the same accuracy as normal speech, provided the microphone is close enough to capture it.<sup>[3]</sup>

On desktop, Flow introduces whispering during onboarding. The setup asks whether you work around others and tailors mic advice for shared spaces. If AirPods are connected, it warns you to switch. A "Try it yourself" screen lets you practice dictating into mock Slack, Gmail, and Notion screens; the Notion demo shows a "Whisper a note" prompt.<sup>[3]</sup>

On iOS, discreet dictation works through the keyboard mic button, the lock screen widget, or Siri shortcuts ("Take Flow note" for hands-free capture without taking the phone out of your pocket).<sup>[3]</sup>

On Android, the Flow Bubble appears above the keyboard in any text field. Whisper into it using the same mic-distance principle: a wired headset or clip-on lavalier mic close to the mouth gets you far better whisper results than the phone's built-in mic held at arm's length.<sup>[3]</sup>

### Silence warnings

Flow monitors audio during dictation and alerts you when the mic stops delivering signal. After 5 seconds of silence, the waveform animation goes flat and a "No audio received" notification appears. If silence continues to 15 seconds, it escalates to a "Microphone is not working" notification with options to open the mic picker or contact support.<sup>[3,4]</sup>

These warnings are your canary. If you see them during whisper dictation, the mic is too far from your mouth, the input volume is too low, or another app has seized the audio device. All three are Input Chain problems, not Flow problems.

## Platform-Specific Audio Behavior

### Mac

On macOS, the built-in microphone is the default. It works well for normal-volume dictation at desk distance, but it has one hard constraint: close the laptop lid and the built-in mic is disabled. Flow detects clamshell mode and shows a notification with a "Select microphone" button. Clamshell detection requires macOS 12 or later.<sup>[1]</sup>

A separate macOS fact: identifying which app is currently using the mic requires macOS 14.2 or later. On earlier versions, Flow cannot tell you that Zoom or Teams has the mic locked.<sup>[1]</sup>

The "Mute music while dictating" setting is off by default on Mac. Enable it under Settings, then System, then Sound, and Flow will mute your default output device when you start dictating and restore it when you stop.<sup>[5]</sup>

### Windows

Windows typically grants microphone access automatically. If another app has exclusive control, the fix lives in the Sound control panel: right-click your mic in the Recording tab, then Properties, then Advanced, and uncheck "Allow applications to take exclusive control of this device."<sup>[1]</sup>

The "Mute music while dictating" setting is on by default on Windows (the opposite of Mac).<sup>[5]</sup>

### iOS

The "Disable Flow Session" setting controls what happens when an audio interruption occurs (a phone call, a Bluetooth device connecting or disconnecting, Siri activating). The timeout is user-configurable and defaults to 5 minutes. Choosing "never" means dictation never auto-stops from interruption length; choosing "immediately" means it always ends after any interruption.<sup>[1,5]</sup>

A phone call, a Siri activation, or a Bluetooth connect/disconnect event during dictation stops the recording. Flow does not automatically resume; you start dictation again manually.<sup>[1]</sup>

### Android

On Android 16, Flow supports switching to your hearing aid's microphone during dictation.<sup>[1]</sup> On earlier Android versions, hearing aids are not routed as dictation input.

Android has no in-app mic picker and no "Mute music" toggle. The OS routes audio, and Flow accepts what it gets. If you want to control which mic Flow uses on Android, connect the one you want and disconnect the ones you do not.

## When Things Go Wrong

A few mic failure modes deserve mention here because they are Input Chain failures, not transcription failures. (For the full symptom-to-fix mapping, see The Failure Map in Ch24.)

**Mic stays on after dismissing the bubble (desktop).** On Mac and Windows, dismissing the bubble during an active dictation session can leave the microphone recording in the background until the session times out after 20 minutes. Stop the dictation explicitly to release the mic immediately.<sup>[2]</sup> On Android, this was fixed in version 1.6.0; hiding the bubble now immediately stops dictation and releases the microphone.<sup>[2]</sup>

**Retry and Recover have a 14-day window.** Audio recordings older than 14 days lose their Retry, Recover, and Download audio options. If you need to diagnose a transcription problem, check the recording within two weeks.<sup>[2]</sup>

**19-minute warning.** A 1-minute warning notification fires at 19 minutes of active dictation, before the 20-minute hard session stop (see Trigger Discipline, Ch2, for session limits). This is the mic staying active for the maximum allowed duration, not a hardware fault.<sup>[2]</sup>

**If your mic disconnects mid-session,** Flow shows a "Microphone disconnected" notification with an Insert button so you can paste whatever was captured before the disconnect.<sup>[1]</sup>

## Best Practices

Position the mic close. That sentence is worth repeating because it is the single most effective thing you can do for dictation accuracy.

Select your mic by name in Flow's picker rather than relying on Auto-detect. If the volume bars move when you talk, your setup is working.<sup>[3]</sup>

Make sure your OS sound settings and Flow agree on which mic to use. Mismatched defaults are the most common source of "it worked yesterday" problems.<sup>[3]</sup>

Disable virtual microphones. Apps like NVIDIA Broadcast, VoiceMeeter, and Teams Audio can intercept your input and cause unexpected behavior.<sup>[3]</sup>

Stay consistent. Use the same mic regularly so results stay predictable.<sup>[3]</sup>

## Key Points

- Output quality is bounded by input quality; no software setting compensates for a bad microphone or poor mic placement.
- AirPods and wireless earbuds degrade dictation accuracy because they sit too far from your mouth and compress audio over Bluetooth.
- Select your microphone by name in Flow's picker rather than relying on Auto-detect, which follows the system default and shifts without warning.
- Discreet whisper dictation works well when the microphone is within a couple of inches of your mouth, regardless of platform.
- Platform differences in mic control are real: desktop gives you a full picker, iOS gives you a toggle, Android gives you nothing.
- When silence warnings appear during dictation, the problem is almost always the Input Chain, not the transcription engine.
