# Command Mode and Transforms

*In this chapter: Flow does more than insert text. Command Mode and Transforms turn your voice into an editing tool, letting you rewrite, restructure, and polish selected text without touching the keyboard. Both features require a paid subscription, both run on Mac and Windows only (as of Q2 2026), and both shift Flow from a dictation engine to something closer to a voice-controlled text editor.*

## The Voice as Editor

Most humans who adopt dictation software think of it as a one-way street. You talk, the software writes. The cursor moves forward. If something needs fixing, your hands go back to the keyboard.

That mental model is incomplete.

Flow has a second mode. Instead of inserting new text at the cursor, it can take text you have already written, listen to an instruction you speak aloud, and rewrite the selection in place. Highlight a paragraph, say "make this more concise," release the shortcut, and the paragraph shrinks. Highlight a block of English, say "translate to Polish," and you get Polish. The original text is gone; the replacement sits where the selection was.

This is Voice as Editor. Not dictation. Editing.

The distinction matters because it changes what you reach for Flow to do. Drafting is still the core use, but once you internalize that the same tool can revise, restructure, translate, and polish, the keyboard becomes the fallback rather than the default for editing passes. The two features that make this work are Command Mode and Transforms. They overlap in spirit but differ in mechanics, and understanding the boundary between them is the point of this chapter.

## Command Mode

Command Mode is the freeform surface. You highlight text (or not), hold down a keyboard shortcut, speak a natural-language instruction, and release. Flow processes the instruction and either replaces the selected text with its output or, if nothing was selected, inserts the response at the cursor.<sup>[1]</sup>

### Activation

Command Mode lives behind a toggle in Settings, under Experimental. It requires a paid subscription or an active free trial; the Experimental settings page is invisible to users on the free tier without a trial.<sup>[1]</sup> Once enabled, the default shortcuts are:

- **Mac:** Fn + Ctrl
- **Mac (no Apple Fn key):** Cmd + Ctrl + Option
- **Windows:** Ctrl + Win + Alt

You can rebind the shortcut in Settings. Up to four shortcuts per action, each with up to three keys. Keyboard shortcuts require at least one modifier key; standalone mouse buttons (Middle Click, Mouse 4 through 10) are also valid bindings and do not need a modifier.<sup>[1]</sup> Press and hold, speak the command, release. Press Escape at any time to cancel.

### With a Selection

Highlight text in any application, activate Command Mode, and speak. Flow replaces the highlighted text with the result. The replacement is destructive: your original selection is gone. Undo with Cmd+Z (Mac) or Ctrl+Z (Windows) to get it back.<sup>[1]</sup>

The ceiling is 1,000 words. Select more than that and Flow shows "Oops, too long to polish" and asks you to trim the selection.<sup>[1]</sup>

### Without a Selection

Activate Command Mode without highlighting anything and you get a different behavior: Flow generates content or answers a question and inserts it inline at the cursor. This turns Command Mode into a general-purpose voice prompt that writes directly into whatever field has focus.<sup>[1]</sup>

You can also ask Flow to recall content from your past dictations, notes, or meetings. It searches your history and surfaces the relevant text inline.<sup>[1]</sup> Reading calendar events and reminders is supported; creating new events or reminders by voice is not (as of Q2 2026).<sup>[1]</sup>

### Updating Polish Settings by Voice

This is the subtlest capability in Command Mode. Speak a preference or a rule change during Command Mode, and Flow recognizes it as a settings request rather than a text transformation. It shows a notification with the proposed change and an Apply button; nothing changes until you confirm.<sup>[1]</sup>

Examples that work: "Always capitalize acronyms." "Turn off Fix spelling." "Add a rule to never use exclamation marks." "I don't like to use the word utilize."<sup>[1]</sup>

This is hands-free configuration. You can shape your Polish rules without ever opening Settings.

### The "Press Enter" Command

Say "press enter" at the end of a dictation and Flow strips those words from the output, pastes your text, then sends an Enter keystroke. Useful in chat apps and prompt interfaces where Enter submits the message.<sup>[1]</sup>

One edge to know: a comma immediately before "press enter" is not treated as a sentence boundary. "Hello world, press enter." produces "Hello world,." with a stray period after the comma.<sup>[1]</sup>

The first time Flow detects the phrase, it shows a one-time notification. Tap "Great" to enable, or "Disable" to keep "press enter" as literal text going forward. You can toggle the behavior later in Settings, under Experimental.<sup>[1]</sup>

### Constraints and Edge Cases

Command Mode cannot fire while a previous transcription or transform is still processing. If you press the shortcut mid-processing, Flow shows a warning instead of starting a new command.<sup>[1]</sup> Servers can also be busy; "Command Mode Servers Are Busy" means high demand, and the advice is to wait a few minutes.<sup>[1]</sup>

If Flow cannot paste the transformed result into the active field, it copies the text to your clipboard and notifies you, so you can paste manually.<sup>[1]</sup> And if the transformation produces text identical to the original, Flow shows "Your text looks good!" instead of replacing anything.<sup>[1]</sup>

Command Mode is experimental and may change. That caveat is worth taking seriously; the feature's behavior has shifted in recent updates, and earlier bugs (where a regular dictation following a voice command was silently processed as another command) have been fixed but illustrate the surface's immaturity.<sup>[1]</sup>

## Transforms

If Command Mode is the freeform prompt, Transforms is the repeatable preset. You define a named transform with a prompt, assign it a keyboard shortcut, and from then on, highlighting text and pressing that shortcut applies the transform without you having to speak at all.<sup>[2]</sup>

The distinction: Command Mode requires you to speak every time. Transforms fire from a shortcut alone, using a prompt you configured once.

### Setup and Activation

Transforms lives on its own tab in the Flow app. The first visit offers a guided demo: highlight sample text, press the default shortcut, and see Polish run. After a successful demo transform, a "Turn on Transforms" button appears. Click it, and the feature is active.<sup>[2]</sup>

The opt-in toggle at the top of the Transforms tab controls whether the feature is live. Turning it off grays out all settings and removes the Polish and View Diff shortcuts from your keyboard. This is worth knowing if your international keyboard characters (characters like n with tilde or o with umlaut produced via Option+key on Mac) suddenly stop working: activating Transforms reserves Opt+key shortcuts for transform slots. Turn the toggle off or rebind the shortcuts to get those characters back.<sup>[2]</sup>

Important: Transform shortcuts do not register at all until you first visit the Transforms tab, click "Try it out," or toggle Transforms on. This is by design; it keeps international keyboard characters working normally for users who have never opted in.<sup>[2]</sup>

### Default Shortcuts

- **Polish:** Opt+1 (Mac) / Win+Alt+1 (Windows)
- **Prompt Engineer:** Opt+2 (Mac) / Win+Alt+2 (Windows)
- **View Diff:** Opt+O (Mac) / Win+Alt+O (Windows)

You can rebind View Diff in Settings under Keyboard shortcuts. Polish and Prompt Engineer rebind from each transform's card on the Transforms tab.<sup>[2]</sup>

### Slots and Configuration

You get up to 9 transform slots. Slot 1 is fixed as Prompt Engineer; slots 2 through 9 are customizable. A "+ Create your own" card appears whenever you have fewer than 9 configured. A separate Polish card at the top controls the base Polish behavior, with 5 default toggle rules and up to 5 custom instructions of 50 words each.<sup>[2]</sup>

Each slot needs a name (for custom prompts), a prompt describing what the transform should do, and a keyboard shortcut. Writing samples are optional. Changes auto-save, but a transform is only persisted once both the prompt and shortcut are set. Close the modal with a required field missing and your changes are silently discarded.<sup>[2]</sup> There is no Save button and no Cancel button. The auto-save indicator cycles through "Saving," "Saved," and "Last saved Xs ago." A Reset button restores defaults for one transform; Reset Defaults on the main page restores everything after a confirmation step.<sup>[2]</sup>

### Writing Samples

Writing samples teach a transform what your finished output should sound like. They are scoped to each individual prompt, not shared across transforms.<sup>[2]</sup>

The limits: up to 5 samples per prompt, each between 50 and 500 words. Renaming a prompt carries its samples over. Deleting or resetting a prompt removes its samples (default Polish samples are always preserved). Only samples for the active prompt are sent when a transform fires; samples tagged to other prompts are not included.<sup>[2]</sup>

Samples sync between Mac and Windows but are not available on iOS. Under Privacy Mode, sample text content is not uploaded (metadata only). Under enterprise Zero Data Retention policies, samples are kept on-device only.<sup>[2]</sup>

### Auto-Polish After Dictation

Flow can apply a transform automatically to every dictation you finish. Click the chevron icon in the Flow status bubble to open the dropdown, turn on "Auto Apply After Dictation," and choose Polish, Prompt Engineer, or any custom prompt you have saved.<sup>[2]</sup>

The selection persists across restarts. When a non-default transform is active, the status bubble shows the first two letters of the prompt name in uppercase (for example, "SU" for "Summarize"). If auto-polish fails or times out, Flow falls back to pasting the original unpolished dictation rather than losing your words.<sup>[2]</sup>

### The Diff Viewer

After any transform, press Opt+O (Mac) or Win+Alt+O (Windows) to see what changed. The diff viewer shows inline changes: teal highlights for additions, strikethrough for removals. A badge reads "1 Change" or "N Changes." Actions include Accept edits, Configure Polish, Undo, Copy, Thumbs Up, Thumbs Down, and Retry.<sup>[2]</sup>

### Transforms in the Scratchpad

Inside the Scratchpad (Flow's built-in notes surface, covered in Chapter 16), Transforms gets its own bar at the bottom of the window, separate from the global keyboard shortcuts. Three AI-ranked suggestion chips appear at a time, drawn from a catalog of six: More concise, More professional, More casual, Turn to list, Turn to table, and Polish. A refresh icon reshuffles the set. A free-text input ("Follow up or ask a question") lets you write a one-off transform applied with Enter.<sup>[2]</sup>

Transforms in the Scratchpad apply to highlighted text if any is selected, otherwise to the entire note. Images attached to the note are preserved across transforms. And the Version history dropdown shows every save labeled by source (Typed edits, Dictated, Transform, Custom transform, or Created) with relative timestamps, so you can step back to any prior version.<sup>[2]</sup>

### Platform and Plan Limits

Transforms is rolling out gradually on Mac and Windows (as of Q2 2026). Polish on iOS is also rolling out gradually, with a 10-word minimum and a 1,000-word maximum. Writing samples and the "Translate to English" re-polish option are Mac and Windows only.<sup>[2]</sup>

Desktop accepts 1 to 1,000 words per transform (exactly 1,000 is allowed; 1,001 triggers the error). Short text below the minimum is silently skipped with no notification.<sup>[2]</sup>

Custom transform prompt slots do not sync across devices; they are stored locally on each Mac or Windows machine. Your base Polish on/off settings and toggles do sync.<sup>[2]</sup>

## The Relationship Between the Two

Command Mode and Transforms serve the same goal through different mechanisms. Command Mode is ad hoc: you speak a new instruction every time. Transforms is repeatable: you configure once and invoke with a shortcut. In practice, you will likely use Command Mode for one-off requests ("translate this to French," "summarize this for a non-technical audience") and Transforms for the operations you run daily (Polish, a custom "make concise" prompt, a tone shift).

Both require a paid subscription or active free trial. Both work on Mac and Windows. Both have a 1,000-word ceiling on selected text. Command Mode edits can be undone with Cmd+Z (Mac) or Ctrl+Z (Windows). Transform edits can be reverted with the Undo button in the diff viewer, or stepped back through Version history in the Scratchpad.<sup>[1][2]</sup>

The combination is what earns the name Voice as Editor. Dictation gets words onto the screen. Command Mode and Transforms shape them once they are there. The hands stay off the keyboard for both passes.

## Key Points

- Command Mode accepts freeform spoken instructions to transform selected text or generate new content at the cursor, with a 1,000-word selection ceiling.
- Transforms provides repeatable, shortcut-driven presets that apply a saved prompt to highlighted text without requiring you to speak each time.
- Both features require a paid subscription or active free trial and are available on Mac and Windows only (as of Q2 2026).
- Writing samples let you teach each transform what your finished output should sound like, scoped per prompt and synced between desktop devices.
- Auto-polish can apply a transform to every dictation automatically, falling back to the original unpolished text if the transform fails or times out.
- Command Mode replacements can be undone with Cmd+Z or Ctrl+Z. Transform replacements can be reverted with the Undo button in the diff viewer, or stepped back through Version history in the Scratchpad.
