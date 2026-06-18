# Dictionary

*In this chapter: Flow ships with a general vocabulary, but your world has specific names, acronyms, and terms it has never encountered. The Personal Lexicon is how you close that gap, teaching Flow the words that matter to your work and letting it correct the ones it consistently gets wrong.*

Every voice-to-text system carries a vocabulary. That vocabulary was trained on public text, conference talks, podcast transcripts, and millions of sentences written by humans who do not work at your company, do not know your colleagues' names, and have never heard your industry's acronyms spoken aloud. The moment you say "Korostyshevskiy" or "FigJam" or "HIPAA" with the expectation that it lands correctly, you are asking the system to guess. Sometimes it guesses well. Sometimes it produces something creative and wrong.

Flow solves this with a feature it calls the dictionary. The name undersells it. What you are really building is a Personal Lexicon: a living, syncing list of words, names, and correction rules that sits between your voice and the Rewrite Pass (Ch1), nudging the output toward your intent before the text ever reaches the cursor.<sup>[1]</sup>

The dictionary is not a dump of every word you will ever say. It is a curated, prioritized collection of the words the general model gets wrong for *you*. That distinction matters. Adding five hundred common English words will not make Flow smarter; adding the twelve names it keeps mangling will.

## Two Kinds of Entry

Dictionary entries come in two flavors, and understanding the difference saves you from wondering why one approach works and the other does not.

**Vocabulary words** improve recognition accuracy for uncommon or specialized terms during transcription. You add "McKenzie," and Flow is more likely to produce "McKenzie" instead of "Mackenzie" when it hears the name. The word acts as a signal boost: Flow now knows this spelling exists in your world.<sup>[1]</sup>

**Replacement rules** go further. They swap one specific transcription for another, every time. If Flow keeps producing "Draught" when you say "Draft," you create a replacement rule that catches the error and fixes it automatically. Replacement rules fire as soon as you finish dictating, before the text reaches the cursor. Each word can have exactly one replacement rule; if you need to change the correction, you edit the existing entry rather than creating a new one.<sup>[1]</sup>

The practical heuristic: if Flow sometimes gets the word right and sometimes does not, add a vocabulary word. If Flow *always* produces the same wrong spelling, create a replacement rule. The replacement is the surgical instrument; the vocabulary boost is the general nudge.

## The Personal Lexicon in Practice

Adding a word is fast on every platform. On Mac and Windows, you open the dictionary in the sidebar, click Add New, type the word, and save. On iOS, you tap the + button in the Dictionary tab. On Android, the same + button opens an Add Word dialog.<sup>[1]</sup>

There is a 60-character limit per entry on desktop and Android. iOS enforces 59 characters; a word of exactly 60 characters is rejected on the save attempt. Duplicates are rejected on all platforms with a validation message.<sup>[1,2]</sup>

Changes take effect immediately on the device where you make them. No restart required. And your dictionary syncs across Mac, Windows, iOS, and Android, so a word you add on your laptop appears on your phone the next time it checks in.<sup>[1]</sup>

That sync timing varies by platform. Desktop syncs at app start. iOS syncs when the app loads. Android syncs at sign-in and whenever the Dictionary screen is opened. If you just added a word on your Mac and want it on your Android phone right now, open the Dictionary screen on Android to force it.<sup>[2]</sup>

### Starring: Local Priority, Not Global

On Mac and Windows, you can star a dictionary entry. A starred word gets higher priority during recognition; when Flow encounters conflicting words or has many dictionary items, starred words win. The star icon sits next to each entry, and clicking it toggles the priority.<sup>[1,2]</sup>

Here is the catch that trips people up: star status is stored locally per device and does not sync. If you star "McKenzie" on your work Mac, your home Mac does not know about it. You need to star the entry on each desktop device where you want the boost.<sup>[1,2]</sup>

iOS and Android do not support starring at all. iOS sorts entries by modification date. Android has no sort controls.<sup>[1,2]</sup>

### Auto-Add: Selective Learning

Flow can learn from your corrections. When you enable Auto-add to dictionary (Settings, System, Extras), Flow watches for words it does not recognize and adds them automatically. But it is selective: only proper nouns and uncommon names get auto-added. Common words like "sprint," "roadmap," or "deploy" are deliberately excluded.<sup>[1]</sup>

Auto-learned words appear in your desktop dictionary marked with a sparkle icon, so you can distinguish them from words you added manually. If Flow auto-adds something you do not want, delete it like any other entry.<sup>[1]</sup>

## Language-Specific Abbreviations

The dictionary is not English-only. It handles a problem that multilingual users hit constantly: abbreviation collisions across languages.

Consider "BTW." In English, Flow expands it to "by the way." In Dutch, BTW is the standard abbreviation for an entirely different concept. If you dictate in Dutch and Flow keeps producing "by the way," you have a language collision. The fix: create a replacement rule where the misspelling is "by the way" (or however Flow transcribes it) and the correct spelling is "BTW."<sup>[2]</sup>

Flow ships with a few default dictionary entries, including "btw" mapped to "by the way." To reclaim that abbreviation for another language, edit or delete the default entry first, then add your own.<sup>[2]</sup>

A few best practices for abbreviation handling:

- Match your pronunciation. If you say letters individually ("bee tee double-u"), enter that phrasing as the misspelling, not the abbreviation itself.<sup>[2]</sup>
- Use precise capitalization. Enter "BTW" in the correct spelling field, not "btw" or "B.T.W."<sup>[2]</sup>
- Add variations. If you sometimes spell it out and sometimes say it as a word, add an entry for each pronunciation.<sup>[2]</sup>
- Skip periods unless your style guide requires them. "BTW" rather than "B.T.W."<sup>[2]</sup>

Flow cannot detect language context for ambiguous acronyms automatically. If you need "BTW" in Dutch and "by the way" in English, add the Dutch entry and spell out the English phrase when speaking. One Language Per Breath (Ch13) applies here too: the dictionary does not switch behavior mid-utterance.<sup>[2]</sup>

## The Platform Gap

The dictionary exists on all four platforms, but it does not behave identically on all four. Android is the platform with the most constraints. On Android, you cannot star entries, sort the list, or run a bulk import. More significantly, replacement rules (the misspelling-to-correction pairs) cannot be created on Android. There is no field for it. You must create replacement rules on desktop or iOS, and they sync to Android and apply during dictation. When you edit a synced replacement rule on Android, only the trigger word is visible; the replacement value is preserved silently in the background.<sup>[1,2]</sup>

On Android, there is also a cross-list constraint: a word cannot be both a dictionary entry and a snippet trigger. Flow shows an error if you try. On desktop and iOS, this cross-check is not enforced, so the same word can exist in both lists. When dictionary entries and snippet triggers overlap, the longer trigger takes priority over the shorter one.<sup>[3]</sup> For a fuller treatment of snippet trigger behavior, see The Spoken Macro (Ch11).

### Personal Dictionaries: The 40-Entry Limit

The Language-Specific Abbreviations documentation notes that personal dictionaries are limited to 40 manually-added entries.<sup>[2]</sup> This is a constraint worth knowing: if you are adding words one by one and hit the cap, Bulk Import (Ch12) is the path for larger vocabulary sets.

### Personal Versus Team

On Team and Enterprise plans, admins can create shared dictionary entries that apply to all team members automatically. Individual users can still add personal entries. If the same word exists in both your personal and team dictionaries, your personal version takes precedence.<sup>[1]</sup>

Team dictionary visibility differs by platform. On desktop, you see tabs for All, Personal, and Shared with Team. On iOS, team plan subscribers see filter tabs; non-team users see a flat list. On Android, only Enterprise (Business plan) users with active or trialing status see the team filter chips; everyone else sees a flat list.<sup>[1]</sup>

For a deeper look at team dictionary deployment, see The Org Layer (Ch23).

## Bulk Import

If you have a large existing vocabulary (a list of product names, a medical terminology set, a roster of client companies), adding them one by one is not practical. Bulk Import lets you upload a CSV file with up to 1,000 entries at once, with a maximum file size of 3MB. It is available on Mac and Windows only and requires an active paid subscription or active trial.<sup>[1]</sup>

The CSV format is straightforward: one column for vocabulary words, or two columns for misspelling-and-correction pairs. Quoted fields are supported, so commas inside quotes will not split a value. Duplicate entries are automatically skipped. Imported words appear with an upload icon and can have corrections added later.<sup>[1]</sup>

Bulk Import also supports snippets (in JSON format) and, when team features are enabled, a Share with Team toggle lets you import directly into the team dictionary.<sup>[1]</sup> The mechanics of bulk import are covered in detail in The Style Layer (Ch12).

## Building a Good Lexicon

The dictionary rewards curation over volume. A few principles:

**Add both forms.** If you add "API," add "APIs" too. Flow does not automatically pluralize dictionary entries, and the plural form is a different recognition target.<sup>[1]</sup>

**Prefer replacement rules for persistent errors.** If Flow *always* gets it wrong the same way, a replacement rule is more reliable than a vocabulary boost. The vocabulary word nudges; the replacement rule guarantees.<sup>[1]</sup>

**Review periodically.** Colleagues leave. Projects end. Acronyms change. A dictionary cluttered with obsolete terms is noise that can interfere with current recognition.<sup>[1]</sup>

**Star strategically on desktop.** You get higher priority from starring, but remember: the star does not sync. If you work on multiple desktops, star on each one.<sup>[1,2]</sup>

**Use the scratchpad shortcut.** On Mac and Windows, if a word is underlined as a potential misspelling in the scratchpad (see The Scratchpad, Ch16), right-click and select Add to Dictionary. One click, no modal, and the word is saved immediately.<sup>[1]</sup>

## Key Points

- The Personal Lexicon is a curated list of words and correction rules that bridges the gap between Flow's general vocabulary and your specific terminology.
- Vocabulary words nudge recognition toward correct spellings, while replacement rules guarantee a specific substitution every time Flow produces a known error.
- Starred entries get higher recognition priority on desktop, but star status is stored locally per device and does not sync across machines.
- Android applies dictionary entries and replacement rules during dictation but cannot create replacement rules; use desktop or iOS for that.
- Language-specific abbreviation collisions are solved by creating replacement rules that override Flow's default expansions for the target language.
- When a dictionary entry and a snippet trigger overlap, the longer trigger takes priority, preventing accidental misfires between the two systems.
