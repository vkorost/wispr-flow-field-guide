# Chapter 11: Snippets

*In this chapter, we look at snippets: saved text blocks that expand from a spoken trigger phrase. You will learn how to create them, what makes a trigger reliable versus fragile, where expansion breaks down across platforms, and how to keep your snippet library clean as it grows. Snippets are the closest Flow gets to programmable output, and using them well means fewer repetitive keystrokes for the text you type most.*

Every tool reaches a point where typing the same thing again feels like a personal insult. Your mailing address. Your Zoom link. The four-sentence reply you send to vendor invoices. You know the text by heart, but knowing it does not make your fingers move faster. Copy and paste helps, but only if you remembered to copy the right thing, and only if you are near the device that has it on the clipboard.

Snippets solve this the way a voice-first tool should: you say a trigger phrase, and Flow replaces it with stored text. The concept is simple enough that most humans will set up their first snippet and immediately wonder why they did not do it sooner. The execution, however, has edges. Triggers can collide with your natural speech. Expansion text can paste partially in certain apps. Android and desktop handle sync differently. This chapter maps the territory.

## The Spoken Macro

A snippet is a spoken macro. You define a trigger phrase and its expansion, and whenever Flow hears the trigger during dictation, it swaps the phrase for the stored block. Say "my address" in the middle of a sentence, and Flow inserts your full street address where those two words would have gone.<sup>[1]</sup>

Triggers can be up to 60 characters. Expansion text can be up to 4,000 characters.<sup>[2]</sup> That upper bound is generous enough to hold a full email signature, a canned customer-support reply, a code template with placeholders, or a standard legal disclaimer. Flow ships with two default snippets out of the box: "my email address" and "my Flow referral."<sup>[3]</sup> You can edit or delete both.

The trigger fires mid-sentence. Say "send the package to my address" and Flow produces "send the package to 123 Main Street, San Francisco, CA 94102" (or whatever you stored).<sup>[1]</sup> The expansion always uses the exact casing you saved. Flow does not rewrite snippet content through the cleanup engine; what you stored is what you get.

That last point matters. The Rewrite Pass (Ch1) applies to your spoken words, but snippet expansions bypass it. If you save a URL in lowercase, it stays lowercase even when the snippet fires at the start of a sentence. If you save a block of text with specific line breaks, those line breaks persist. Snippets are literal.

## Trigger Design

The difference between a snippet that works every time and one that misfires weekly is trigger design. Flow matches triggers as whole words with word-boundary detection, so a trigger like "btw" will not fire if it appears inside another word.<sup>[4]</sup> But it will fire when surrounded by punctuation, dashes, or parentheses, because those count as word boundaries.

When your entire dictation consists solely of the trigger phrase, Flow strips punctuation before matching. Say "my address." with an audible period, and the snippet still fires.<sup>[1]</sup> When the trigger appears mid-sentence among other words, Flow uses standard word-boundary matching and expects a closer match.<sup>[4]</sup>

Three rules for triggers that hold up:

**Be specific.** "My email signature" is better than "thanks." "Zoom meeting link" is better than "link." The more your trigger sounds like something you would say naturally in conversation, the more likely it will fire when you do not want it to.<sup>[1]</sup>

**Be unique.** If you have both "my address" and "my email address," the overlap rule applies: the longer trigger takes priority.<sup>[5]</sup> Say "my email address" and Flow expands the longer one. Say "my address" and Flow expands the shorter one. This works, but it requires you to pronounce the full phrase clearly. If your triggers are "address" and "my address," a slight hesitation before "my" can fire the wrong one. Keep trigger phrases distinct enough that partial speech does not cause collisions.

**Test after creating.** Dictate a sentence using the trigger and confirm it fires correctly. Then dictate a sentence where the trigger words appear naturally but should not fire. If both cases work as expected, you are done.<sup>[1]</sup>

The trigger-collision rule also applies across snippets and dictionary entries. The Personal Lexicon (Ch10) establishes that a word cannot serve as both a snippet trigger and a dictionary entry. On Android, this is enforced at creation time with a validation error. On iOS and desktop, the app currently allows creating both, but keeping them unique avoids unpredictable behavior.<sup>[6]</sup>

## Creating and Managing Snippets

Creation follows the same pattern on every platform, with minor interface differences.

On Mac and Windows, open the Wispr Flow app, click Snippets in the left sidebar, click "Add new," enter your trigger and expansion, and press Cmd+Enter (Mac) or Ctrl+Enter (Windows).<sup>[1]</sup> Editing uses the pencil icon; deleting uses the delete icon with a confirmation prompt.

On iOS, open the app, tap the menu icon, select Snippets, tap the floating + button, enter your trigger and expansion, and tap Save.<sup>[1]</sup> Editing opens an edit sheet; deleting is a swipe-left or long-press action.

On Android, open the app, tap Snippets in the bottom navigation bar, tap the + button, enter the trigger and expansion, and tap Add.<sup>[1]</sup> Editing is a left-to-right swipe; deleting is a right-to-left swipe with confirmation.

Desktop users get a search bar (Cmd+F / Ctrl+F) and filter tabs for All versus Personal snippets. Team and Business (Enterprise) plans add a Shared with team filter.<sup>[1]</sup> On Team and Business plans, members can create shared snippets visible to the whole organization. Personal snippets take priority over team snippets when the same trigger exists in both.<sup>[1]</sup>

Bulk import of snippets from a JSON file is available on desktop; the mechanics belong to The Style Layer (Ch12).

## How Expansion Behaves

When a snippet fires, Flow adjusts the expansion to fit its context. If the snippet fires mid-sentence, the first letter may be lowercased and trailing punctuation removed to match the surrounding text. Proper nouns that Flow recognizes (names in your dictionary, your own name) are not lowercased mid-sentence.<sup>[5]</sup>

Only sentence-ending punctuation (period, question mark, exclamation mark) is stripped before the snippet. Commas, colons, semicolons, and other punctuation survive.<sup>[5]</sup>

On Windows, this context-aware adjustment is skipped entirely when you are dictating into the Wispr Flow app itself.<sup>[5]</sup> If you are testing snippets in Flow's own text fields and the casing looks wrong, try the same snippet in another app before filing a bug.

Snippet expansions insert static text. Dynamic variables like today's date are not supported.<sup>[1]</sup> If you need a date in your snippet, you update the expansion manually. This is a real limitation for humans who use date-stamped templates, but it also means snippet behavior is predictable: what you saved is what you get, every time.

## Clipboard and Paste Mechanics

On Mac, Flow pastes snippet content using the clipboard, then restores your previous clipboard contents shortly after the operation completes.<sup>[5]</sup> Most of the time this is invisible. The exception: large clipboard contents like PDFs, audio files, and rich text with attachments (RTFD format) are not restored.<sup>[5]</sup> If you had a 40-page PDF on your clipboard, triggered a snippet, and then pressed Cmd+V expecting your PDF, it would be gone. This is worth knowing if you work with large documents and use the clipboard as a staging area.

When a paste operation fails in the target app, Flow sends a notification asking you to paste manually. The default shortcuts are Ctrl+Cmd+V on Mac and Alt+Shift+Z on Windows.<sup>[7]</sup> If manual paste succeeds, the issue is app-specific, not a snippet problem.

On Windows, if a notification appears saying "Update admin settings to paste!" with the body "Run Flow as Administrator to insert text everywhere," the fix is to relaunch Flow as Administrator.<sup>[7]</sup> This surfaces when Flow cannot paste into elevated applications.

## The Android Story

Android handles snippets differently in ways that matter.

Snippets are cached locally after your first visit to the Snippets screen, so they remain available offline after that initial load.<sup>[8]</sup> Sync happens at login and each time you open the Snippets screen.<sup>[9]</sup> If you create a snippet on your desktop and want it on your Android phone, open the Snippets screen on Android. That triggers the sync.

Android enforces the snippet-versus-dictionary uniqueness rule at creation time. Try to add a snippet trigger that already exists as a dictionary entry, and you will see an inline validation error.<sup>[6]</sup> This is stricter than iOS and desktop, where the conflict is technically possible.

The partial-paste failure deserves its own paragraph. In earlier versions, dictated text was successfully inserted into apps like WhatsApp, Telegram, Messenger, Signal, Slack, Teams, Discord, Instagram, Snapchat, Google Messages, and Gmail, but Flow incorrectly treated it as a failure and either fell back to the clipboard or reported an insertion error. This was fixed in Wispr Flow 2.0.0 for Android.<sup>[10]</sup> If you are running an older version and snippets seem to fail in messaging apps, update first.

Other Android-specific fixes worth noting: version 1.8.5 resolved duplicate entries appearing after editing a snippet; version 1.8.2 fixed snippet replacements not applying during dictation; version 1.5.2 addressed crashes from duplicate items in the snippets list and a sync issue where snippets and dictionary entries could get mixed up.<sup>[11]</sup> All of these are resolved in current versions. If you see any of these symptoms, the answer is always the same: update and restart.

## Team Snippets

On Team and Business (Enterprise) plans, snippets gain a shared dimension. Members can create snippets visible to the entire organization, and shared snippets behave identically to personal ones: say the trigger, get the expansion.<sup>[1]</sup>

Personal snippets take priority. If a trigger exists in both your personal list and the team library, your personal version wins.<sup>[1]</sup> This means you can override a team snippet without deleting it, which is useful when the standard company disclaimer needs a department-specific tweak.

Creating a team snippet on desktop means toggling "Share with team" in the Add snippet dialog. Moving an existing personal snippet to the team library uses the Share icon next to the snippet (desktop) or a long-press menu option (iOS).<sup>[1]</sup> Good candidates for team snippets: the company address, standard disclaimers, team signatures, and frequently used meeting links.

The Org Layer (Ch23) covers team administration in depth; this chapter only establishes how team snippets work from the individual user's perspective.

## When Snippets Do Not Fire

A quick diagnostic for the most common failures:

The trigger is misspelled. Open the Snippets list, verify the trigger text, and say the phrase clearly and completely. Trigger matching is case-insensitive, so "My Email" and "my email" both work.<sup>[5]</sup>

The triggers are too similar. If "my address" and "my email address" both exist and the wrong one fires, rename one trigger to be more distinct. "Home address" and "work email address" leaves no ambiguity.

The trigger matches natural speech. If you keep accidentally firing "thanks" when you are genuinely saying thanks in a sentence, change the trigger to something you would never say conversationally, like "my thanks template."

Sync has not happened. On Android, open the Snippets screen to force a sync.<sup>[9]</sup> On desktop, click Refresh on the Snippets page. If snippets still do not appear across devices, sign out and back in.<sup>[1]</sup>

For deeper sync behavior across platforms, The Synced Identity (Ch20) has the full picture.

## Key Points

- Snippets are spoken macros: a trigger phrase expands into stored text, bypassing the cleanup engine for literal output.
- Trigger design determines reliability; specific, unique phrases that do not overlap with natural speech prevent misfires.
- The longer trigger always wins when triggers overlap, and a word cannot serve as both a snippet trigger and a dictionary entry.
- On Mac, Flow restores your previous clipboard after pasting a snippet, except for large items like PDFs and audio files.
- Android caches snippets locally after the first visit to the Snippets screen and syncs each time that screen is opened.
- Team snippets share vocabulary across an organization, but personal snippets always take priority over team versions.
