# Notes and Capture

*In this chapter: Flow includes its own capture surface, The Scratchpad, a floating notepad on desktop and a full notes editor on iOS. Notes sync across signed-in devices, support images on desktop and markdown on iOS, and reach beyond the app through Siri Shortcuts, Lock Screen widgets, Spotlight indexing, and the Action Button. The chapter covers how the Scratchpad works on Mac and Windows, how iOS Notes differs, pinning and organization, HIPAA restrictions, and when the Scratchpad becomes a safety net for failed paste operations.*

Every dictation tool assumes you already have a destination. You open the email, the document, the chat window, and then you talk. That assumption works most of the time. But there is a category of speech that has no destination yet: the half-formed idea at 2 a.m., the phrase you want to keep before you forget it, the three bullet points that will become a slide deck later. Those thoughts need a place to land before they have a place to go.

Flow ships its own landing pad. On Mac and Windows it is called the Scratchpad. On iOS it is called Notes. They share a synced backend, so what you capture on your phone shows up on your laptop, and vice versa. The concept is The Scratchpad: a capture surface that belongs to Flow, lives inside Flow, and never forces you to context-switch to a separate app just to hold an idea.

The rest of this chapter covers three things. First, how the desktop Scratchpad works and what it can hold. Second, how iOS Notes differs and the entry points that make it useful on a phone. Third, the organizational tools, sync boundaries, and the one scenario where the Scratchpad stops being optional and becomes a safety net.

## The Desktop Scratchpad

The Scratchpad on Mac and Windows is a floating panel with a multi-tab rich-text editor.<sup>[1]</sup> Open it with the Scratchpad keyboard shortcut and it appears on top of whatever you are working in without stealing focus.<sup>[1]</sup> That last detail matters. On Mac, the Scratchpad opens as a floating panel that leaves your foreground app active, so you can keep typing in your editor while the Scratchpad hovers to the side.<sup>[1]</sup> You are not choosing between your work and your note. You have both.

Notes auto-save as you type and sync via the cloud.<sup>[1]</sup> A progress indicator shows sync status: a cloud checkmark means sync is complete, and a slashed cloud means you are offline.<sup>[1]</sup> If you lose connectivity, notes save locally and sync when you reconnect. No data disappears because your Wi-Fi dropped.

### Voice Dictation in the Scratchpad

Tap the microphone icon inside the Scratchpad to start dictating. A waveform appears while you speak. Tap the green checkmark to insert the transcribed text at your cursor, or tap the X to cancel.<sup>[1]</sup> The Rewrite Pass (Chapter 1) applies here exactly as it does everywhere else in Flow: your speech is cleaned up, punctuated, and formatted according to whatever Auto Cleanup level you have set.

### Images

Desktop notes support image attachments. Paste or drag a PNG, JPEG, WebP, GIF, or BMP image directly into a note.<sup>[1]</sup> Each image must be 5 MB or smaller, and each note can hold up to 10 images.<sup>[1,2]</sup> Very large images are automatically resized. Images sync to your other signed-in desktop devices, stored in secure cloud storage and downloaded automatically.<sup>[1]</sup>

Image attachments are not supported on iOS.<sup>[1]</sup> If you paste a screenshot into a desktop note and then open it on your phone, you will see the text but not the image. That asymmetry is worth knowing if your workflow depends on visual references.

The pinning article adds more detail on image sync: supported formats for sync include WebP, PNG, JPEG, and GIF, with a maximum resolution of 4096 by 4096 pixels per image.<sup>[2]</sup> If an image fails to sync, the note's text still syncs normally; failed uploads are retried automatically.<sup>[1]</sup>

### Sorting and Navigation

Notes display newest-first, including older notes created before modification dates were tracked.<sup>[1]</sup> Custom sorting is not available as of Q2 2026.<sup>[1]</sup> The sidebar lists your notes, and links opened in the Scratchpad that would normally open in a new browser window instead open as a new Scratchpad web tab with your login session preserved.<sup>[1]</sup>

## iOS Notes

On iOS, the capture surface is called Notes and lives inside the Wispr Flow app.<sup>[1,3]</sup> It is a plain-text editor with markdown preview, not a rich-text editor like the desktop version. Write markdown in edit mode, then tap the preview toggle in the toolbar to see it rendered.<sup>[1,3]</sup> Heading shortcuts (#, ##, ###) create H1 through H3 headings, and horizontal dividers use ---, ***, or ___.<sup>[3]</sup>

The feature set is different from desktop in important ways. iOS Notes does not support image attachments. It does support markdown rendering, Spotlight indexing, Siri Shortcuts, widgets, and the Action Button. The editor has a floating microphone button at the bottom-right for dictation, and text is inserted at your cursor position with a line break added automatically when appending to a non-empty note.<sup>[3]</sup>

### Entry Points

What makes iOS Notes powerful is not the editor. It is how many ways you can start a note without opening the app.

**Lock Screen widget.** Add the Wispr Flow widget to your Lock Screen, and a single tap opens a full-screen capture view with dictation ready.<sup>[3]</sup> Notes created via the widget do not auto-save; you must tap Save in the top-right corner to keep them, or X to discard.<sup>[3]</sup> The Save button is disabled while dictation is recording or processing, so stop dictation first. Lock Screen widgets require iOS 16 or later.<sup>[3]</sup>

**Control Center.** Two controls are available: Flow Notes (opens a new note with dictation) and Flow Toggle (starts or stops recording).<sup>[3]</sup> Control Center customization requires iOS 18 or later.<sup>[3]</sup>

**Action Button.** On iPhones with an Action Button (iPhone 15 Pro/Pro Max, all iPhone 16 models, all iPhone 17 models including iPhone Air), you can assign a Wispr Flow shortcut such as "Dictate a Flow note" or "Open Flow Notes."<sup>[3]</sup>

**Siri Shortcuts.** Six shortcuts are available immediately on install, no setup required.<sup>[3]</sup> The most notable is Save Flow Note: say "Save Flow note" to Siri, and Siri prompts "What should the note say?" Your response is saved as a note without opening the app.<sup>[3]</sup> Fully hands-free. No screen interaction. That is the closest Flow gets to ambient capture on iOS.

**Spotlight search.** Spotlight indexes note titles and the first 300 characters of each note's content, so you can find notes from your home screen.<sup>[3]</sup>

### AI Summaries

Tap the summary button on a note to generate a condensed overview.<sup>[3]</sup> AI summaries are generated on demand each time and are not saved.<sup>[3]</sup> They are disabled on accounts with data restrictions, including HIPAA BAA-signed accounts and accounts with Privacy Mode enabled.<sup>[3]</sup>

### Auto-Open and Note Management

Turn on "Start new note on app open" in Settings to automatically open a new note when you return to the Notes tab.<sup>[3]</sup> Notes are sorted by most recently modified and grouped by date. Swipe left for Share and Delete, or long-press for Copy, Edit, Share, and Delete.<sup>[3]</sup> Empty notes (no title and no content) are automatically deleted without confirmation.<sup>[3]</sup>

## Pinning

Pinning is available on Mac and Windows only.<sup>[2]</sup> Pin a note and it jumps to the top of the Notes hub, above all unpinned notes, in both the default view and search results.<sup>[2]</sup> A small pin icon on the card shows which notes are pinned. Hover over any note card to reveal Edit, Pin/Unpin, and Delete buttons, or use the pin button in the Scratchpad sidebar.<sup>[2]</sup>

There is no stated limit on the number of pinned notes.<sup>[2]</sup> Multiple pinned notes are ordered by most recently modified first.<sup>[2]</sup>

One detail that will surprise you if you use Flow on multiple machines: pin status is local to each device and does not sync.<sup>[2]</sup> Pin a meeting template on your work laptop and it will not appear pinned on your home desktop. You pin separately on each device. Pin sync is on the roadmap but not available as of Q2 2026.<sup>[2]</sup>

### Scratchpad Open Behavior

You can configure the Scratchpad shortcut to route directly to your last active pinned note. Select "Open last active pinned note" in the Scratchpad open behavior picker at Settings, then System, then Scratchpad, then Customize.<sup>[2]</sup> If no pinned note exists, the shortcut falls back to standard show/hide behavior. This setting applies only to the keyboard shortcut; other entry points (opening a note from the Notes hub, paste-failure fallback, or the status bubble) are not affected.<sup>[2]</sup>

## Sync and Its Boundaries

Notes sync across signed-in devices using a shared cloud backend.<sup>[1]</sup> On iOS, pull down on the notes list to trigger a manual sync, or tap the refresh button in the navigation bar.<sup>[3]</sup> Local edits are never overwritten by a server sync.<sup>[3]</sup>

Image sync has its own rules. Images sync across desktop devices only; iOS does not support image attachments.<sup>[1]</sup> If a note has images, the text syncs to iOS but the images do not appear.

### HIPAA BAA Accounts

HIPAA BAA-signed accounts can create and use Notes, but notes are stored locally only and do not sync across devices.<sup>[3]</sup> The pull-to-refresh and manual sync buttons remain visible but have no effect.<sup>[3]</sup> AI summaries and Spotlight indexing are also disabled on these accounts.<sup>[3]</sup> These restrictions cannot be changed by individual users when enforced by an organization administrator. The full HIPAA treatment belongs to Chapter 21 (The Cloud Boundary); here, the practical consequence is that HIPAA accounts get a capable local notepad but lose the cross-device story entirely.

## The Scratchpad as Safety Net

When Flow transcribes your speech but cannot paste the result into the target app, it does not throw the text away. It opens the Scratchpad with the transcribed text inside.<sup>[2]</sup> That paste-failure fallback means the Scratchpad is not just a convenience; it is the last line of defense between you and lost words.

The scenarios that trigger this behavior are covered in Chapter 17 (The Insertion Boundary): non-QWERTY keyboard layouts, privilege mismatches on Windows, and fields that refuse paste input. What matters for this chapter is that the Scratchpad is always there to catch what falls. Even if you never open it deliberately, you should know it exists, because one day Flow will open it for you.

## Obsidian and Plain-Text Workflows

If your note-taking lives in an external tool like Obsidian, Flow does not compete with it. Flow inserts text via paste or keyboard simulation, which means it works with any standard text editor, including Obsidian's Markdown editor (inferred from research; no dedicated documentation exists for Obsidian compatibility). Spoken commands like "new line" and "new paragraph" produce line breaks in any plain-text context. Flow does not generate Markdown syntax automatically (no heading markers, no list bullets), so you control the formatting yourself.

One practical note: if you run Obsidian alongside other text-expansion or hotkey tools, watch for hotkey conflicts with Flow's activation shortcut. The generic guidance applies: adjust Flow's hotkey in Settings if collisions occur with your existing Obsidian shortcuts. This behavior is inferred from the research corpus; test it on your own setup.

## Key Points

- The Scratchpad is Flow's built-in capture surface: a floating panel on desktop and a full notes editor on iOS, sharing a synced backend.
- Desktop notes support rich text and up to 10 images per note; iOS supports markdown preview but no image attachments.
- iOS Notes can be reached without opening the app through Lock Screen widgets, Control Center, Siri Shortcuts, the Action Button, and Spotlight.
- Pin status is local per device and does not sync, so pin your important notes separately on each machine you use.
- When paste fails, Flow opens the Scratchpad with your transcribed text, making it a safety net for insertion failures.
