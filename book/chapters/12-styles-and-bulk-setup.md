# Chapter 12: Styles and Bulk Setup

*In this chapter, we cover Flow's style system, which adjusts tone per app category, the Polish shortcuts that rewrite highlighted text on command, and the bulk import pipeline that loads dictionary words and snippets from files. Together these three surfaces form the configurable layer between your voice and Flow's output, and learning to set them up means the rewrite works for you instead of around you.*

You can dictate all day and still sound wrong. Not wrong as in inaccurate. Wrong as in the email reads like a text message and the Slack reply reads like a cover letter. The Cleanup Dial (Ch7) controls how aggressively Flow rewrites your speech, but it says nothing about tone. Cleanup is a global knob. It cannot know that your personal messages need lowercase energy and your client emails need a firm handshake.

That gap is what styles fill. And once you have a library of dictionary words and snippet triggers from The Personal Lexicon (Ch10) and The Spoken Macro (Ch11), getting them into Flow one at a time starts to feel like punishment. Bulk import solves that. This chapter covers the full configurable surface: style selection, Polish shortcuts, writing samples, and the file-based import path for dictionary and snippet data.

## The Style Layer

Styles let you assign a tone preset to each of Flow's four app categories: Personal messages, Work messages, Email, and Other. When you dictate into Slack, Flow checks which category Slack belongs to, finds the style you picked for that category, and adjusts the output accordingly.<sup>[1]</sup>

The feature is available on all four platforms: Mac, Windows, iOS, and Android. There is one hard gate. Styles only activate when at least one of your selected languages is English, either American or British.<sup>[1]</sup> If your language is set to French or Japanese, the Styles tab is hidden entirely. This is a Q2 2026 limitation, not a permanent architectural decision, but it is real right now and worth knowing before you spend time configuring.

Four styles are available, though not every style appears in every category:

- **Formal.** Available for all four categories on all platforms. The default on Mac and Windows for every category until you make a selection.<sup>[1]</sup>
- **Casual.** Available for all four categories. The default for Personal messages on iOS and Android.<sup>[1]</sup>
- **Very Casual.** Available only for the Personal category. If you want Very Casual for email, you will not find it there; use Casual or Excited instead.<sup>[1]</sup>
- **Excited.** Available for Work, Email, and Other. Not available for Personal.<sup>[1]</sup>

The platform defaults tell you something about the assumptions baked into each surface. Desktop users get Formal everywhere, reflecting the expectation that desktop dictation skews professional. Mobile users get Casual for Personal, reflecting the expectation that phone dictation skews conversational.<sup>[1]</sup> Both are reasonable defaults. Both are wrong for some fraction of users. Change them.

## Setting Up Styles

On Mac and Windows, open Wispr Flow and click Styles in the left sidebar. Click a category tab, pick a style card, and dictate a test phrase in a matching app. If the output reflects the tone you selected, you are done.<sup>[1]</sup>

On iOS, open the app, tap the Styles tab in the bottom bar, pick a category, and tap a style card.<sup>[1]</sup> iOS also offers a session override: the keyboard shows a style button you can tap to temporarily switch styles without changing your saved preferences. The override lasts for that dictation session only; your per-category settings remain untouched.<sup>[1]</sup>

On Android, open the app, tap the Style tab (singular on Android, plural everywhere else), select a category, and tap the style card you want. A panel opens from the bottom. Tap Save.<sup>[1]</sup> That last step matters: style changes on Android are not applied until you tap Save. Navigating away discards unsaved changes.<sup>[1]</sup> If your Android styles seem to be ignoring your choices, this is the first thing to check.

## How Flow Picks the Right Style

When you dictate, Flow detects which app has focus and maps it to one of the four categories. Supported apps include messaging (WhatsApp, Telegram, Signal, Messenger, Discord), work tools (Slack, Teams, Zoom, LinkedIn, Notion, Jira, Google Docs), and email clients (Gmail, Outlook, ProtonMail), including web versions.<sup>[1]</sup>

When an app could fit more than one category, the priority order is: Personal Messaging, then Email, then Work Messaging, then Other.<sup>[1]</sup> A temporary keyboard style override, if set on iOS, takes precedence over all of these for that session.

## Sync and Conflict

Style preferences sync across all your devices automatically. Changes push to the server immediately. Other devices pick them up on their next sync, which can take up to one hour. Restart the app to force an immediate sync.<sup>[1]</sup>

Conflict resolution is last-write-wins. Whichever device saved most recently sets the canonical style for that category.<sup>[1]</sup> If you change Personal to Very Casual on your phone and then change it to Formal on your laptop thirty seconds later, Formal wins everywhere. There is no merge and no warning. Keep that in mind if you share an account across multiple devices and tend to tweak settings on whichever one is nearest.

## Writing Samples

Styles set the broad tone. Writing samples sharpen it. You can add up to five writing samples per prompt, each between 50 and 500 words, that teach Flow what your personal voice sounds like.<sup>[1]</sup> Samples are configured inside the Polish prompt modals (Custom Prompt or Prompt Engineer), not on the Styles page itself.

There is a privacy dimension. When Privacy Mode is enabled, writing samples stay on your device and do not sync to the server. On Enterprise plans with Zero Data Retention, samples are not stored locally either.<sup>[1]</sup> If you are on a privacy-conscious plan, check whether your samples are actually reaching the model before assuming they are influencing output. The Cloud Boundary (Ch21) covers the broader privacy controls.

Samples are tied to the prompt they were added under. Rename a custom prompt and the samples move with it. Delete a custom prompt and the samples go with it, permanently. Samples tied to default Polish prompts are not affected by resets.<sup>[1]</sup>

## Polish Shortcuts

Polish is the on-demand rewrite surface. Highlight any text, press a keyboard shortcut, and Flow rewrites the selection according to a rule you defined. Fix grammar. Shift tone. Translate. Reformat into bullet points. The rewrite replaces the selected text in place.<sup>[2]</sup>

Polish is available on Mac and Windows only, as of Q2 2026.<sup>[2]</sup>

### Setting Up a Polish Shortcut

Open Flow settings, navigate to the Transforms page in the sidebar, and click Create New. Name the shortcut (something like "Fix Grammar" or "Make Formal"), write a rule describing how Flow should rewrite the selected text, and assign a keyboard shortcut. The shortcut needs at least one modifier key (Cmd, Ctrl, Opt, Alt, Shift, or Fn on Mac) and uses at most three keys. Mouse buttons from Mouse 4 through Mouse 10 can satisfy the modifier requirement on their own.<sup>[2]</sup>

Verify by highlighting text in any text field and pressing your shortcut. The selected text is replaced with the polished version. Changes to the name and prompt auto-save; shortcut changes save immediately.<sup>[2]</sup>

### Default Rules and Custom Rules

The base Polish configuration includes five toggleable default rules: Make more concise, Reword for clarity, Reorder for readability, Add structure for readability, and Maintain your tone.<sup>[2]</sup> Two additional rules are Pro-only: Clarify main point and Refine phrasing for impact.<sup>[2]</sup>

You can add up to five custom rules, each a maximum of 50 words, in the base Polish configure modal.<sup>[2]</sup> These custom rules let you push the rewrite in directions the defaults do not cover. "Keep all technical terms unchanged." "Always use active voice." "Remove hedging language." Specific rules outperform vague ones. "Make it better" is not a rule; "Rewrite in a professional tone for a client email" is.<sup>[2]</sup>

### Capacity and Limits

You can create up to eight custom transforms. Including the built-in Polish and Prompt Engineer presets, the Transforms page shows up to ten cards total. The Create New button disappears once all custom slots are filled.<sup>[2]</sup>

Polish accepts up to 1,000 words at a time. Selections longer than that produce a notification and are not transformed.<sup>[2]</sup> If you routinely polish long documents, break them into sections. The 1,000-word ceiling is a per-operation limit, not a daily cap.

### The Diff Viewer

After polishing finishes, the Flow Bar shows "Done." with a clickable "See changes" link. Clicking it opens a diff viewer showing additions in purple, removals struck through, and an Undo button with a keyboard shortcut reminder.<sup>[2]</sup> Copy, Thumbs Up, Thumbs Down, and Retry actions are also available. The diff viewer also offers re-polish presets: Prompt Engineer, Turn to list, Translate to English, and Empathize.<sup>[2]</sup>

The diff viewer is the safety net. Polish rewrites are destructive by default; the selected text is replaced the moment polishing completes. If the rewrite missed the mark, the undo shortcut brings back the original. Use it.

## Bulk Import

Once your dictionary and snippet collection outgrows manual entry, bulk import gets them into Flow from a file. The feature is desktop-only (Mac and Windows). iOS and Android can view and edit synced items individually but cannot import files.<sup>[3]</sup>

### Access Requirements

Bulk import requires an active paid subscription or an active trial with days remaining. An expired trial does not grant access. Without a qualifying subscription, the Experimental settings page where you enable bulk import does not appear.<sup>[3]</sup>

To enable it: open the Flow app, go to Settings, then Experimental, and toggle on Bulk import. Once enabled, an Import button appears in the top-right corner of both the Dictionary and Snippets tabs.<sup>[3]</sup>

### Dictionary Import (CSV)

Dictionary items use CSV format. A single-column CSV adds vocabulary words that Flow should recognize. A two-column CSV maps an incorrect phrase (first column) to its correction (second column).<sup>[3]</sup>

The first column supports up to 60 characters. The second column supports up to 4,000 characters. Rows exceeding either limit are skipped. The parser follows standard CSV quoting rules (RFC 4180), so wrap fields containing commas in double quotes.<sup>[3]</sup>

A practical example: if you have a list of company names, product terms, and industry jargon that Flow consistently gets wrong, export them into a CSV with the misspelling in column one and the correction in column two. Import once. Done.

### Snippet Import (JSON)

Snippets use JSON format: an array of objects, each with a `name` field (the trigger, up to 60 characters) and a `text` field (the expansion, up to 4,000 characters). Both must be strings. Entries with non-string values, whitespace-only values, or values exceeding limits are skipped. Extra fields beyond `name` and `text` are ignored.<sup>[3]</sup>

### Shared Limits

Each import accepts a maximum of 1,000 items and a 3 MB file size.<sup>[3]</sup> The import modal walks through four sequential screens (Upload, Preview, Loading, Success) with a progress bar at the top.<sup>[3]</sup>

Duplicates are filtered at the preview stage. Matching is case-insensitive: "Flow" and "flow" count as the same word. Duplicates within your file keep only the first occurrence. When importing to a team library, duplicates are checked against existing team entries, not your personal library.<sup>[3]</sup>

One rule crosses the boundary between dictionaries and snippets: a word cannot exist as both a dictionary entry and a snippet trigger. Conflicting items are silently skipped during import.<sup>[3]</sup> If you are importing both a dictionary CSV and a snippets JSON, import one first, then the other, so the conflict check catches overlaps before they become silent failures.

Imported items sync across all your devices. Each device syncs independently with the cloud, so there may be a brief delay before new imports appear on your phone or second computer.<sup>[3]</sup> Bulk-imported dictionary words appear with an upload badge icon so you can tell them apart from manually added entries.<sup>[3]</sup>

## Key Points

- Styles assign a tone preset per app category, but they only activate when your language is set to English (American or British).
- Platform defaults differ: desktop starts Formal everywhere, while mobile starts Casual for Personal messages.
- Polish shortcuts let you rewrite highlighted text on command, with up to eight custom transforms on Mac and Windows only.
- Writing samples refine Flow's output beyond preset tones, but they do not sync when Privacy Mode is enabled.
- Bulk import loads up to 1,000 dictionary or snippet items from a CSV or JSON file, requiring a paid subscription and desktop access.
- A word cannot exist as both a dictionary entry and a snippet trigger; the conflict check runs silently during import.
