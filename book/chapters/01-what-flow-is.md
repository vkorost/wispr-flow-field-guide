# Chapter 1: What Wispr Flow Is and How It Works

*In this chapter, you learn what Wispr Flow actually does beneath the surface: not a transcriber that records your words verbatim, but a language-model pipeline that rewrites your speech into finished prose and drops the result wherever your cursor sits. The mental model you build here, The Rewrite Pass, is the lens through which every chapter that follows makes sense.*

Most humans who try a dictation tool bring a transcription model in their heads: speak, get words, clean it up yourself. Dictation as a faster keyboard.

Wispr Flow does not work that way.

That mismatch is the source of almost every surprise this book addresses, good and bad. Flow captures your voice, sends it to cloud servers, runs it through speech recognition, hands the raw transcript to a language model for cleanup and formatting, and inserts the result into whatever text field has focus on your device. The text that appears is not your words. It is a rewrite of your words. *That distinction is the whole game.*

Call it The Rewrite Pass. Everything else in this book is a variation on that one operation: how far the pass goes, how to control it, how to teach it your vocabulary, and how to work around the places where it overshoots or annoys you. If you internalize one concept from this entire guide, make it this one.

The product's own description gestures at the idea: "Flow transcribes your speech in real time, runs AI commands to edit your text, and adapts to your vocabulary over time."<sup>[1]</sup> That sentence buries the lead. The AI editing is not an add-on feature you discover later. It is the primary operation. The transcription is an intermediate step, a waypoint the audio passes through on the way to becoming prose. The help center also describes Flow this way: "Press a hotkey, speak naturally, and Flow types your words in real time. It learns your vocabulary over time and can run AI commands."<sup>[1]</sup> The vocabulary learning and the AI commands are not accessories. They are the core of what differentiates this tool from the dictation engines built into your operating system.

## The Four-Stage Pipeline

Understanding the pipeline in concrete terms makes the product's behavior predictable. There are four stages, and knowing which one is responsible for a given behavior is the fastest route to diagnosing surprises.

**Stage 1: Capture.** A hotkey or on-screen control activates the microphone and starts recording. On Mac and Windows, you hold a keyboard shortcut and release it when you finish speaking.<sup>[2]</sup> On iOS, you switch to the Flow Keyboard and tap a microphone button. On Android, a floating overlay called the Flow Bubble appears when you open a text field and the on-screen keyboard is visible; tap the bubble to begin.<sup>[1]</sup> The capture stage is purely local. The microphone records audio that will be uploaded. Nothing is processed yet.

The practical implication of Stage 1 is that microphone quality and proximity matter more than any software setting. A quiet, close mic gives the recognition engine clean signal; a distant Bluetooth earbud gives it noise. Chapter 18 covers the audio hardware chain in detail, but the principle belongs here: garbage into capture means garbage through the rest of the pipeline.

**Stage 2: Cloud speech recognition.** The audio is uploaded to Wispr's servers. There is no on-device processing and no offline fallback. The help center puts it plainly: "Flow requires an internet connection for voice transcription."<sup>[1]</sup> No connection means no dictation. That is not a limitation of the free tier or a missing feature. It is the architecture of every tier, on every platform.

At this stage, the audio becomes raw text. The words you spoke are now a transcript, not yet cleaned up and not yet useful as something you would paste into an email or a document.

**Stage 3: The Rewrite Pass.** This is where the product earns its name and its reputation for both polish and occasional overreach. The raw transcript is handed to a language-model layer that does far more than spell-check. The help center describes it as "AI commands to edit your text" and notes that Flow "adapts to your vocabulary over time for more accurate transcription."<sup>[1]</sup> In practice, the cleanup adds punctuation and capitalization, restructures grammar, and reshapes your spoken words into finished prose. Chapter 7 covers the specific behaviors (including filler-word removal, list formatting, and mid-sentence self-correction) under The Cleanup Dial.

The user does not choose which model handles a given request; the routing is server-side and invisible. What matters from this side of the screen is the result: without this stage, you get a raw transcript. With it, you get a prose draft. The difference is the product.

**Stage 4: Insertion.** The rewritten text is inserted at the cursor using operating-system APIs. On Mac, that requires Accessibility permission (Chapter 4, The Permission Gate). On Android, it requires the accessibility service (Chapter 6, The Floating Bubble). On iOS, the insertion works through the keyboard extension.<sup>[1,2]</sup> The result lands in whichever text field has focus: a Slack message, a document, a code comment, a browser form. Any field, any application, without requiring the receiving application to know anything about Flow.

Flow works across all apps because it inserts transcribed text into whichever app has focus, without requiring any in-app integration.<sup>[1]</sup> That universality is what makes the setup overhead worth absorbing.

## The Cloud-Only Consequence

The cloud dependency is not a quirk or a temporary limitation. It is the architecture.

Every dictation session round-trips through Wispr's servers. In practice, you perceive a short pause between releasing the hotkey and seeing text appear. That is not a bug; it is the transit time for audio traveling to a server, being recognized, rewritten, and sent back. Flow is not a live stenographer typing in step with your syllables. The text arrives as a block after you stop speaking.

The practical consequence: use Flow where you have a reliable internet connection. In airplane mode, in a network-restricted corporate environment, in a conference room where cloud services are blocked by policy, Flow cannot function. There is no offline fallback at any subscription tier, on any platform, as of Q2 2026.<sup>[1]</sup>

The cloud architecture also carries a privacy dimension worth knowing about early. Every utterance you dictate leaves your device. Controls exist: a Privacy Mode that prevents retention of your audio and transcripts, and a HIPAA Business Associate Agreement available to subscribers who need it.<sup>[1]</sup> Those controls are significant, and Chapter 21 covers them in full under The Cloud Boundary. For now, the relevant fact is that your audio travels to a server, gets processed, and comes back as text. That is the product. If the round-trip is a dealbreaker for your use case, you need to know that before you build a workflow around Flow.

## The Rewrite Is the Point

Here is where the mental model becomes specific enough to use daily.

When you dictate into a typing interface expecting verbatim output, The Rewrite Pass feels like interference. The tool is changing your words without asking. When you dictate *expecting* the pass, the same behavior reads as assistance. You speak loosely, Flow writes tightly. The shift is not in the software. It is in your expectations.

The pass does quite a lot by default. The help center describes AI commands that edit, rephrase, and restructure your text, and a vocabulary-adaptation layer that learns your words over time.<sup>[1]</sup> Practically, that means the output you see is cleaner, more punctuated, and more grammatically polished than what you said. The pass also adapts to the active application; in a personal messaging app it formats casually, while in a work email client it formats formally. That context-adaptive layer is called The App-Aware Rewrite and belongs to Chapter 9.

What the pass does not do is read your mind. It rewrites what it heard toward plausible finished prose, using whatever context it has. The heavier the rewrite level, the more aggressively it polishes. The lighter the level, the closer the output stays to your raw speech. At the lightest setting, sentence structure stays mostly intact. At the heaviest, you can get a substantially different version of what you said: shorter, more polished, which is great for rough first drafts and genuinely problematic for precise technical instructions where every word was chosen deliberately.

That dial is adjustable. Learning to set it correctly for each context is half the skill of using Flow well. Chapter 7 covers The Cleanup Dial in full. For now, know the dial exists, know the default setting is not the only option, and know that when the output surprises you, the correct question is "what level is the dial set to?" not "why is the tool broken?"

*The Rewrite Pass is not a problem to solve. It is the product. Work with it and you write faster. Fight it and you spend your time correcting corrections.*

## Four Platforms, Four Entry Points

Flow is available as native applications for Mac (macOS 12.0 or later), Windows 10 or 11, iOS (18.3 or later), and Android (13 through 16).<sup>[1,3]</sup> Each platform has a distinct interface for entering and exiting a dictation session. The backend pipeline is identical. The front door is different.

**Mac and Windows (desktop).** The primary interface is the Flow Bar, a small floating element that shows an animated waveform while recording. You invoke dictation by holding a keyboard shortcut; the default on Mac is the Fn key.<sup>[1,2]</sup> The app lives in the menu bar on Mac and the system tray on Windows.<sup>[2]</sup> It does not appear in the Dock or the application switcher and has no main window in the traditional sense.

Desktop is also where the Hub lives: a home base for dictation stats, transcription history, your dictionary, snippets, styles, notes, and insights.<sup>[1]</sup> New users see a get-started message with the dictation shortcut; returning users see a welcome-back greeting, recent activity, and stats.<sup>[1]</sup> The Hub is the administrative center of the product.

The desktop experience is the most feature-complete and is where most of this book's discussion is centered. Mac requires Accessibility permission and offers separate builds for Apple Silicon and Intel hardware.<sup>[2,3]</sup> Windows requires only system microphone access and runs on x64 processors.<sup>[3]</sup> Chapter 4 covers Mac setup under The Permission Gate, and Chapter 3 covers Windows under The Electron Tax.

**iOS.** Flow operates as a keyboard extension, not a system-wide hotkey. To dictate, you switch to the Flow Keyboard using the globe icon, then tap the microphone button.<sup>[2]</sup> This is deliberately different from the desktop model, and the whole iOS chapter is organized around the friction of that extra step and the ways to reduce it. Chapter 5 names this The Keyboard Detour.

The gap narrows with the Action Button on supported models: iPhone 15 Pro, iPhone 15 Pro Max, all iPhone 16 models (including iPhone 16e), iPhone 17, iPhone 17 Pro, iPhone 17 Pro Max, and iPhone Air.<sup>[4]</sup> The iPhone 17e is not supported because it lacks a physical Action Button.<sup>[4]</sup> The Action Button can be configured as a quick dictation trigger. Six Siri Shortcuts also install automatically with Flow on iOS and provide additional entry points without touching the keyboard at all.<sup>[3]</sup> iOS also has its own Notes feature with Spotlight indexing and lock-screen widgets for quick capture.<sup>[1]</sup>

**Android.** Rather than replacing the keyboard, Flow places a floating overlay (the Flow Bubble) over whatever you are doing on screen. When you open a text field and the on-screen keyboard appears, the bubble appears alongside it. Tap the bubble to start dictating; tap again to submit.<sup>[1]</sup> The bubble is customizable in size and opacity, can be snoozed by dragging it to the bottom of the screen, and is automatically hidden in banking and financial applications, in password fields, and in numeric and phone number inputs.<sup>[1,3]</sup> Chapter 6 covers this as The Floating Bubble.

**The common thread.** All four platform interfaces invoke the same backend. A dictation from an Android phone and a dictation from a MacBook Pro go through the same speech recognition and the same rewrite pass. What differs is how you start it, how the application fits into your device's security model, and what permissions you grant before the first session.

## Languages, Requirements, and Universal Insertion

**Language support.** Flow supports over 100 languages.<sup>[1]</sup> On Mac, Windows, and iOS, an Auto-detect option identifies the language you are speaking without requiring you to switch manually.<sup>[2]</sup> Auto-detect is not available on Android, where you must select at least one specific language before dictating.<sup>[1]</sup> The rewrite pass is most consistent in English; Chapter 13 covers multilingual behavior and its limits under the name One Language Per Breath.

**System requirements (as of Q2 2026).** Mac requires macOS 12.0 or later on either Apple Silicon or Intel hardware, with approximately 500 MB of free storage.<sup>[1,3]</sup> Windows requires Windows 10 (64-bit) or Windows 11, with x64 processors; ARM-based Windows devices (including Snapdragon) are not officially supported.<sup>[1,3]</sup> iOS requires iOS 18.3 or later on iPhone.<sup>[1,3]</sup> Android runs on Android 13 through 16 and requires an accelerometer for shake-gesture support.<sup>[3]</sup> All platforms require an active internet connection and a working microphone.<sup>[1]</sup>

**Where Flow inserts.** Flow works in any text field in any application, without requiring special integration or support from the receiving app.<sup>[1]</sup> The insertion mechanism goes through the operating system. Slack, Gmail, Notion, VS Code, Microsoft Word, ChatGPT, browser form fields, chat windows, code editors: Flow inserts into all of them. The help center frames the proposition directly: "Dictate anywhere you can type."<sup>[1]</sup> You grant permissions once, learn one set of habits, and those habits work everywhere you type.

Chapter 17 covers the exceptions under The Insertion Boundary: remote desktop configurations, security software, non-standard keyboard layouts, and banking-app detection logic on Android. Those exceptions are real, and knowing them is useful. But they are exceptions to a broad rule.

## What the Rest of the Book Is

Every chapter from here forward either expands one part of The Rewrite Pass pipeline or explains how to control it in a specific context.

Chapters 3 through 6 cover platform setup. The entry point, the required permissions, and the device-specific behavior differ enough across Mac, Windows, iPhone, and Android that each gets its own chapter. Read the chapter for your platform; the others are optional reference.

Chapters 7 through 14 cover the layers you can configure on the rewrite: the cleanup level (The Cleanup Dial), voice editing commands (Voice as Editor), context adaptation (The App-Aware Rewrite), vocabulary teaching (The Personal Lexicon), spoken macros (The Spoken Macro), style tuning (The Style Layer), multilingual behavior (One Language Per Breath), and coding-specific features (Vibe Coding). Each is a way to make The Rewrite Pass work better for a specific task.

Chapters 15 through 18 cover the contexts where you use Flow: writing and messaging workflows, notes and capture, remote and restricted environments, and audio hardware. These address the edges of Stage 4 (insertion) and the beginning of Stage 1 (capture).

Chapters 19 through 21 cover the business and privacy of using Flow: subscription plans (The Word Budget), account management (The Synced Identity), and what happens to your voice data when every utterance goes to a cloud server (The Cloud Boundary).

Chapters 22 through 24 cover usage insights (The Voice Profile), team deployment (The Org Layer), and troubleshooting when the pipeline breaks (The Failure Map).

The rewrite model and the cloud-only architecture are not footnotes. They are the product's identity. Every setting, every failure mode, every pleasant surprise in this book traces back to one of those four pipeline stages. Keep the pipeline in mind, and the book becomes a navigation map.

## Key Points

- Flow is not a transcription tool; it rewrites your speech into finished prose before inserting the result at your cursor.
- All processing happens in the cloud; there is no offline mode on any platform or at any subscription tier.
- The pipeline has four stages: capture, cloud speech recognition, the LLM rewrite pass, and insertion at the cursor.
- Each platform uses a different entry point: a hotkey on desktop, the Flow Keyboard on iOS, and the Flow Bubble on Android.
- The rewrite aggressiveness is adjustable; matching the cleanup level to the task is the core skill of using Flow well.
- Flow inserts into any text field in any application without requiring integration from the receiving app.
- Over 100 languages are supported, with Auto-detect available on all platforms except Android.
