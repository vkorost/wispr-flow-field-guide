# The Cleanup Engine

*In this chapter, you meet the control that governs how aggressively Flow rewrites your speech before it lands: Auto Cleanup. Four levels, from raw transcription to full polish, let you decide how much the rewrite pass changes your words. The chapter covers each level, the backtrack system for mid-dictation corrections, and the practical question of when to dial cleanup down.*

Every voice-to-text tool has to make a decision about your words. Keep them exactly as spoken, filler and all, or rewrite them into something you would have typed. Most tools pick one answer and stick with it. Flow gives you a dial.

That dial is Auto Cleanup, and understanding it is the difference between a tool that saves you time and one that quietly rewrites your meaning while you watch.

## The Cleanup Dial

The Rewrite Pass (Chapter 1) established that Flow is not a verbatim transcriber. It captures your speech, sends it to the cloud, and runs a language model over the result before inserting text at your cursor. Auto Cleanup is the adjustable layer inside that pass. It controls how much the model changes.<sup>[1]</sup>

There are four levels. Each one makes a different promise about how far the rewrite goes.

**None** turns off all AI formatting. You get the raw transcription: filler words intact, grammar untouched, capitalization absent. This also disables Smart Formatting entirely.<sup>[1]</sup> If you need a literal record of what was said, this is the setting. Legal transcripts, verbatim notes, any context where accuracy of utterance matters more than readability.

**Light** removes filler words (um, uh, like) and fixes grammar. It capitalizes the first word of sentences. Your phrasing and sentence structure stay yours.<sup>[1]</sup> This is the level where Flow cleans up the noise without rearranging your thoughts. Developers writing code prompts or technical descriptions tend to live here (inferred from research context).

**Medium** is the default for new users. It edits for clarity and conciseness, which means Flow will shorten sentences, remove redundant clauses, and tighten phrasing.<sup>[1]</sup> Most daily communication lands well at Medium. Email, Slack updates, document drafts. The rewrite is noticeable but rarely intrusive.

**High** is a full rewrite for brevity and polish.<sup>[1]</sup> Flow will restructure your sentences, swap vocabulary, and compress aggressively. The output reads like edited prose. That is its strength and its risk. Because the model optimizes for conciseness and tone, a High cleanup pass could soften blunt statements or reshape emphasis in ways you did not intend. When precision of meaning matters, High is the wrong level.

The Cleanup Level applies globally. Every dictation, in every app, uses the same setting. There is no per-app override, no per-dictation toggle.<sup>[1]</sup> You pick one level and it governs everything until you change it.

One more constraint worth noting: the setting is stored locally on each device and does not sync across machines.<sup>[1]</sup> If you use Flow on two Macs and a Windows laptop, you set the level three times. This is not a bug. It is a design choice that lets you run High on a machine you use for email and Light on a machine you use for code, without one overwriting the other.

As of Q2 2026, Auto Cleanup is available on Mac and Windows only. Mobile support is on the roadmap.<sup>[1]</sup>

## Smart Formatting: The Predecessor

Before Auto Cleanup existed, Flow had a simpler toggle called Smart Formatting. On or off. Smart Formatting handled the basics: removing filler words, fixing grammar, capitalizing sentences.<sup>[2]</sup> It also handled context-aware formatting, adjusting capitalization based on cursor position and stripping trailing periods in messaging apps.<sup>[2]</sup>

When Auto Cleanup shipped, Smart Formatting did not disappear. It migrated. Users who had Smart Formatting ON were moved to Auto Cleanup Light. Users who had it OFF were moved to Auto Cleanup None.<sup>[1,2]</sup> The transition was automatic. If you are a long-time Flow user and never touched your cleanup settings, you are probably running Light.

Smart Formatting also brought features that persist at Light, Medium, and High: automatic list formatting when you say numbered sequences, spoken punctuation commands ("comma," "question mark," "em dash"), and context-aware trailing-period removal in messaging apps.<sup>[2]</sup> These are handled at the formatting layer rather than the AI cleanup layer, but because they are part of Smart Formatting, they are disabled when you set the dial to None.<sup>[1]</sup>

On Android, Smart Formatting is always on and cannot be turned off. On iOS, only an on/off toggle is available; finer level selection is not available.<sup>[2]</sup> This is consistent with Auto Cleanup being desktop-only for now.

## Backtrack: Course Correction Mid-Sentence

You will misspeak. Everyone does. Flow handles this with a system called Backtrack, and it works better than you would expect.

Say "let's do coffee at 2, actually 3." Flow writes "Let's do coffee at 3." The correction phrase ("actually") triggers the backtrack engine, which identifies the prior term and replaces it.<sup>[2]</sup> The documented trigger words include "actually" and "scratch that," among others.<sup>[2]</sup> You do not need to memorize a command syntax. You just correct yourself the way you would in conversation.

Backtrack also handles natural restatements without an explicit trigger. Say "I wanted to buy a record as a gift... as a present." Flow writes "I wanted to buy a record as a present."<sup>[2]</sup> The language model uses your full dictation as context to decide what constitutes a self-correction versus a meaningful repetition. Phrases like "I actually enjoyed the movie" are preserved because the surrounding context does not suggest a correction.<sup>[2]</sup>

There is one hard rule: Backtrack works at every Auto Cleanup level except None.<sup>[1,2]</sup> At None, you get raw transcription, which means your false starts and corrections land in the text exactly as spoken. That is the trade-off. Full fidelity means no automatic cleanup of mistakes.

## Reviewing and Reverting

Flow knows that cleanup can overstep. It gives you two ways to catch it.

The first is the notification. After a longer dictation at Medium or High, Flow briefly shows a "Cleaned up! See what's changed" notification.<sup>[1]</sup> Click it and you see exactly what Auto Cleanup altered. The notification only appears at Medium or High, only on longer dictations, never inside AI apps, and it stops appearing over time so it does not become noise.<sup>[1]</sup>

The second is the diff shortcut. Press Opt+O on Mac or Win+Alt+O on Windows to open the diff for your last cleanup. Press it again to close.<sup>[1]</sup> This works anytime, not just when the notification fires. If you suspect the rewrite changed your meaning, the diff is your audit trail.

If the rewrite went too far, use "Undo AI edit" from the Home tab to revert to your original dictation.<sup>[1]</sup> Your raw words are never lost. Flow keeps them.

## When Cleanup Gets Suppressed

Auto Cleanup does not always run. The most important suppression: when Transforms is active on your account, Auto Cleanup is suppressed entirely.<sup>[1]</sup> Transforms (covered in Chapter 8, "Voice as Editor") is a separate editing layer. The two cannot run simultaneously. If you have enabled Transforms and notice your dictation landing without any cleanup polish, this is why.

The interaction is worth understanding at the architecture level. Auto Cleanup runs automatically on every dictation. Transforms runs on demand, on selected text. They serve different purposes, but they share the same processing pipeline, and that pipeline only runs one at a time. This is a design constraint, not a temporary limitation.

## When to Dial Down

The question every new user eventually asks: which level should I use?

Start at Medium. It is the default for a reason. For most dictation into most apps, Medium produces text that reads like you typed it carefully. The edits are invisible to anyone reading the output.

Dial down to Light when you need your phrasing preserved. Technical writing, code comments, anything where your specific word choice carries meaning. Light removes the verbal noise without touching your structure.

Dial down to None when you need a literal record. Verbatim notes, transcripts you plan to quote, situations where "what I said" and "what Flow thinks I meant" must not diverge.

Dial up to High when speed matters more than precision of voice. Drafting emails you will review before sending. Capturing rough ideas you plan to rewrite anyway. High is a first-draft accelerator, not a final-draft tool.

The cautionary case is code. Developers working in IDEs should be cautious with anything above Light (inferred). Medium and High can rewrite variable names, alter technical phrasing, and restructure comments in ways that break meaning. Light preserves your tokens while cleaning up your filler.

## The Language Boundary

Auto Cleanup runs in every language Flow supports, but it is optimized for English. In non-English languages, the cleanup pass may behave less consistently.<sup>[1]</sup> This is not a bug to report. It is a known limitation of the underlying language model. If you dictate in French or Japanese and the cleanup feels erratic, try dropping to Light or None and handling the formatting yourself.

The multilingual dimension of Smart Formatting is broader. It supports an expanded set of languages, including Chinese (and Cantonese) and Russian, for baseline formatting operations like punctuation and capitalization.<sup>[2]</sup> But the AI-driven cleanup at Medium and High is where the English optimization gap becomes noticeable.

## Spoken Punctuation and Lists

Smart Formatting, which underpins the cleanup system, handles two categories of spoken formatting that deserve mention here because they interact with your cleanup level choice.

**Spoken punctuation.** You can say punctuation marks by name and Flow inserts them. "Period," "comma," "question mark," "colon," "semicolon," "ellipsis," "open parenthesis," "close parenthesis," and many more.<sup>[2]</sup> The system is forgiving about exact phrasing. "Full stop" works for a period. "Star" works for an asterisk. Because spoken punctuation is part of Smart Formatting, these commands are available at Light, Medium, and High. At None, Smart Formatting is disabled entirely, so spoken punctuation commands will not be processed.<sup>[1]</sup>

**Automatic lists.** Say numbered sequences ("one, apples, two, bananas") and Flow formats them as a numbered list.<sup>[2]</sup> Sequence words ("first," "second") also trigger list formatting. This is handled at the formatting layer, not the cleanup layer.

**Press Enter.** On desktop, saying "press enter" at the end of your dictation simulates pressing the Enter key after your text is pasted.<sup>[2]</sup> The first time Flow detects this phrase, it asks you to confirm whether you want the feature enabled. Once enabled, it works reliably. This is desktop only and is suppressed in Command Mode.

## Key Points

- Auto Cleanup is a four-position dial, not a binary toggle; each level makes a different trade-off between fidelity and polish.
- The cleanup level applies globally and is stored per device, giving you different settings on different machines but no per-app control.
- Backtrack lets you correct yourself mid-sentence using natural phrases, but it requires at least Light cleanup to function.
- Transforms and Auto Cleanup are mutually exclusive; enabling Transforms suppresses the cleanup pass entirely.
- The diff shortcut and revert option mean you can always audit what cleanup changed and restore your original words.
- Auto Cleanup is optimized for English; non-English dictation may need a lower cleanup level for consistent results.
- Start at Medium, drop to Light for technical work, and treat High as a first-draft accelerator rather than a final-draft tool.
