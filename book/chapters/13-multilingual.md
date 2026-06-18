# Chapter 13: Multilingual Dictation

*In this chapter: Flow supports over 100 languages but detects which one you are speaking once per session, not per word. The skill is choosing your languages deliberately, switching between sessions rather than mid-sentence, and knowing where the language boundary limits what Flow can do for you.*

Flow does not listen to your words and sort them into languages in real time. It commits to a language at the start of each dictation session and transcribes the entire segment in that language, regardless of what you actually say after the first few seconds. This is not a bug or a shortcut. It is the architectural constraint that makes 100-plus languages viable without hallucinating script switches on every borrowed noun. Internalize it and multilingual dictation becomes reliable. Fight it and every session is a coin flip.

The name for this constraint is *One Language Per Breath*.

## How Detection Works

When you press the hotkey, tap the Flow Bubble, or switch to the Flow Keyboard, the recognition engine samples the first moments of your speech and locks onto the most likely language from your selected set. Everything that follows in that session is transcribed in that language. If you switch from English to German mid-sentence, Flow does not pivot. It transcribes the German words as though they were English, producing nonsense or near-misses. The fix is simple: end the session, start a new one, and speak the other language.<sup>[1]</sup>

This per-session commitment means your language pool matters more than you might expect. The fewer languages you have selected, the less ambiguity Flow faces at the start. Two or three languages that sound distinctly different from each other (English and Japanese, say) give Flow a clean signal. Two languages that overlap in phonetics (Spanish and Italian, or Hindi and Hinglish) force the model to guess, and it will guess wrong often enough to be annoying.<sup>[1]</sup>

## Setting Your Languages

The setup path is nearly identical across platforms, with one important exception on Android.

On Mac and Windows, open Settings, go to General, then Languages. Select the languages you speak, or enable Auto-detect to let Flow choose from the full list of 100-plus options. Click Save and close. Your changes take effect on the next dictation session, not the current one.<sup>[1]</sup>

On iOS, tap Settings, then General, then Set Language. Each tap saves immediately; there is no explicit save step. Removing all specific languages enables Auto-detect automatically.<sup>[1]</sup>

On Android, tap Settings, then Languages. Select or deselect languages, then tap Save. Backing out without tapping Save discards your changes. Here is the exception that matters: Android does not offer Auto-detect. You must select at least one specific language before Save becomes available.<sup>[1,2]</sup>

The practical consequence is that Android users cannot fall back on "let the model figure it out." They have to make a deliberate language choice. This is, counterintuitively, an advantage. Auto-detect choosing from 100-plus languages is the single most common cause of wrong-language transcription on other platforms.<sup>[2]</sup>

## The Language Picker on Desktop

On Mac and Windows, the Flow Bar includes a language pill or globe icon that doubles as a quick switcher. Clicking it opens the Languages submenu, letting you toggle between your selected languages without opening Settings.<sup>[2]</sup>

You can also toggle languages from the Flow tray or menu bar icon's Languages submenu, which gives you the same list without opening the Settings window. For humans who switch languages several times a day, this is the fastest path: keep your two or three active languages selected in Settings, then cycle between them with a single click on the Flow Bar before each session.<sup>[2]</sup>

## Onboarding Defaults

Flow pre-fills your language list from your system settings during onboarding. On desktop, your system language is selected by default; if detection fails, Flow defaults to English. On iOS, the pre-fill happens on first launch only; returning to the language screen later does not re-detect.<sup>[1]</sup>

Regional variants get automatic treatment. British English is selected during onboarding for users in the UK, Canada, Australia, and New Zealand, and on desktop, Ireland and South Africa are included as well.<sup>[1]</sup>

Users in Switzerland and Liechtenstein get their own variant automatically based on system locale, which matters because Swiss German orthography replaces ß with "ss." Standard German keeps "Straße"; Swiss German produces "Strasse." If you are in Zurich and your transcription keeps inserting ß, check that you have German (Swiss) selected rather than standard German.<sup>[1]</sup>

## Code-Switching and Its Limits

Flow works best when you speak primarily in one language with occasional words from another. A borrowed noun or a brand name in English during a French dictation will usually survive. But alternating sentence by sentence, or mixing scripts within a phrase, pushes the model past its reliable range.<sup>[1]</sup>

Chinese and English together are especially difficult. Flow may transcribe English words in Chinese characters or vice versa. The documentation is blunt: a single-language setup is the most reliable fix for this combination.<sup>[1,2]</sup>

English paired with Spanish, French, or German performs better than English paired with Chinese or Japanese. If you code-switch frequently between two Romance languages, or between English and a language with a very different sound profile, keeping both selected and letting per-session detection handle it is workable. If your languages sound similar enough to confuse the model, swap the selection manually before each session.<sup>[1]</sup>

## Language Variants and Orthography

Some languages have regional variants that produce visibly different output.

**English (American) and English (British)** are mutually exclusive. Selecting one automatically deselects the other. The same mutual exclusivity applies to German and German (Swiss), Hindi and Hinglish, and Chinese (Simplified) and Chinese (Traditional).<sup>[1]</sup>

**Hinglish** is a code-switched blend of Hindi and English. With Hinglish selected, Hindi speech is romanized into Hinglish and English speech is formatted as normal English. If you naturally mix both languages and Flow is producing only Hindi or only English, the fix is to select Hinglish explicitly rather than either language alone.<sup>[1,2]</sup>

**Chinese (Simplified and Traditional)** are separate options. On iOS, Flow pre-fills the variant based on your iOS region: China or Singapore pre-fills Simplified; Taiwan, Hong Kong, or Macau pre-fills Traditional. If no region is detected, Simplified is the default. On desktop, Malaysia is also treated as Simplified. Cantonese is a distinct option, separate from both.<sup>[1]</sup>

## French Typographic Spacing

When dictating in French, Flow automatically inserts a narrow space before semicolons, colons, question marks, exclamation marks, and the closing guillemet (»), and after the opening guillemet («). This matches standard French typography and is not a bug. It applies only when French is in your selected language list.<sup>[1]</sup>

The spacing does not apply to colons in times (12:30), ratios (1:1), or URLs, and it is skipped inside code editors and developer tools such as VS Code, Cursor, Xcode, Terminal, and IntelliJ.<sup>[1]</sup>

## The Language Display

Languages appear in the picker with their English name followed by their native-language name in parentheses: "Spanish (Español)," "Japanese (日本語)." Country flag emojis were removed because languages do not map cleanly to countries. On iOS, Auto-detect shows a magnifying glass icon; on desktop, it appears as a toggle showing "100+ languages" when enabled.<sup>[1]</sup>

You can search the picker by either name. Searching for "hindi" also surfaces Hinglish on desktop. On desktop, English, Spanish, and Chinese (Simplified) appear at the top as common languages. Arrow keys navigate the list; Enter selects.<sup>[1]</sup>

## Fixing Wrong-Language Transcription

If Flow types your words in the wrong language, the fix is almost always the same: select only the language you are dictating in and remove the others. Most cases resolve in under a minute.<sup>[2]</sup>

Start with three quick checks. Is Auto-detect on? It can be pushed to the wrong language by accents or short phrases. Do you have more than one language selected? Fewer is more accurate. Did you pick the right regional variant? Wanting British spelling but having American selected is a variant problem, not a detection problem.<sup>[2]</sup>

If you have narrowed to a single language and Flow still transcribes incorrectly, the cause is usually audio: background noise, a low-quality microphone, or a Bluetooth headset with poor recording quality. Try a different mic and a quiet space (see The Input Chain, Ch18).<sup>[2]</sup>

## Non-English Transcription Quality

Flow's documentation states plainly that non-English transcription is not yet as accurate as English. This is a general caveat, not language-specific, and it applies across all platforms as of Q2 2026.<sup>[1]</sup>

Auto Cleanup (see The Cleanup Dial, Ch7) is optimized for English and less consistent in other languages. If your non-English output looks oddly rewritten or loses nuance, consider dialing cleanup down to Light or None for those sessions. (Inferred from the general caveat that non-English transcription is less accurate.<sup>[1]</sup>)

## Russian and Cyrillic: An Honest Assessment

Russian is listed in the language picker on all platforms, inferred from the "100+ languages" claim in the documentation.<sup>[1]</sup> There are no rigorous, language-specific quality evaluations for Russian transcription in the published documentation, on any platform.

Whether Russian dictation quality meets your threshold is something you will need to test on your own device. The same applies to Cyrillic dictionary behavior on mobile: the documentation specifies character limits for dictionary entries but does not explicitly confirm or deny Cyrillic acceptance. There is no documented restriction on character sets, which strongly suggests Cyrillic entries work, but this is inference, not a guarantee. Test it.

For English and Russian code-switching within a single session, the general *One Language Per Breath* constraint applies. Keep both languages selected and switch between sessions, or swap the selection manually before dictating. Rapid intra-sentence switching between English and Russian is not documented as a tested scenario.

## Styles Require English

Personalized Styles (see The Style Layer, Ch12) only apply when dictating in English, whether American or British. On iOS, Text Styles require English as a selected language. On all platforms, if you dictate in any other language, Styles are not applied to the output.<sup>[1]</sup>

This is not a temporary limitation flagged for a future fix. It is the current design as of Q2 2026.

## Key Points

- Flow commits to one language per session; switching languages means starting a new dictation, not changing mid-sentence.
- Selecting fewer languages improves detection accuracy; Auto-detect across 100-plus options is the most common source of wrong-language output.
- Android does not offer Auto-detect, which forces deliberate language selection and often produces better results.
- Regional variants like British English, Swiss German, and Hinglish are separate selections with mutually exclusive pairs.
- Personalized Styles apply only when dictating in English; all other languages receive unformatted output from the style engine.
- Russian dictation is supported but its quality and Cyrillic dictionary acceptance on mobile are unverified; test both on your own device.
