# Context Awareness

*In this chapter, you will learn how Flow reads the active app on your screen and adjusts its output accordingly, a feature called Context Awareness. It covers how app categories shape tone and formatting, what permissions it requires on Mac versus Windows, and the privacy controls that govern what screen data Flow can see.*

Software that rewrites your speech needs to know where the words are going. An email to a client and a Slack message to your teammate contain the same information, but they do not sound the same, and they do not look the same on the page. If a rewriting engine treats both identically, it gets one of them wrong every time. Flow solves this with what amounts to a second layer of intelligence on top of The Rewrite Pass (Ch1): it reads your active app, identifies the context, and adjusts the output before it lands. This is The App-Aware Rewrite.

## What Context Awareness Does

Context Awareness identifies the app you are using and adapts transcription accuracy, style, and formatting automatically.<sup>[1]</sup> When you dictate into Gmail, Flow detects you are composing an email, reads the recipient's name from the screen, and applies your email writing style. When you switch to Slack, Flow detects you have moved to a work messaging app and shifts to your casual messaging style. No manual adjustment needed.

The feature does more than shift tone. It reads a limited amount of text near your cursor and identifies the active app. For browser-based apps, Flow identifies the specific website by URL, so Gmail, Google Docs, and a dozen other web apps are recognized individually rather than lumped together as "Chrome."<sup>[1]</sup> Supported browsers include Chrome, Safari, Arc, Brave, Edge, Firefox, and Opera.

Three specific behaviors are worth understanding:

- **Improved accuracy.** Flow uses names and context visible on screen (such as email recipients) to recognize proper nouns and preserve correct capitalization.<sup>[1]</sup>
- **Conversation context.** In Slack and Apple Messages, Flow reads conversation context for better transcription accuracy. Other apps benefit from general nearby-text reading but do not have dedicated conversation context support.<sup>[1]</sup>
- **Smart formatting in Notion.** Flow detects and ignores Notion's placeholder text ("Heading 1," "Type something...") and inserts your dictated text cleanly into the correct field.<sup>[1]</sup>

That last one is surprisingly useful. Anyone who has dictated into Notion without context awareness has watched Flow faithfully transcribe the words "Heading 1" as part of their output. The App-Aware Rewrite strips that noise before it reaches you.

## The Four Categories

Flow sorts every app into one of four categories: Email, Work messaging, Personal messaging, and Other.<sup>[1]</sup> The category determines which style settings Flow applies. Email, Work messaging, and Other default to Formal and offer Casual and Excited as alternatives. Personal messaging defaults to Casual and offers Formal and Very Casual.

When an app could belong to more than one category, Flow follows a priority order: Personal messaging, then Email, then Work messaging, then Other.<sup>[1]</sup> This means if an app registers as both Email and Work messaging, it is treated as Email. If it registers as both Personal messaging and anything else, Personal messaging wins.

The formatting behavior differs by style. Formal never strips trailing periods. Casual strips trailing periods for shorter dictations. Very Casual always strips trailing periods. None of the styles strip exclamation marks or question marks, and stripping is skipped entirely if the line already has punctuation or if text is selected.<sup>[1]</sup>

Context-aware formatting also handles mid-sentence continuation. When you resume dictating in the middle of an existing sentence, Flow lowercases the first letter and adds leading or trailing spaces as needed.<sup>[1]</sup> Small details, but the kind that accumulate into text that looks like someone typed it rather than dictated it.

## Persistent Context in Code Editors

Developers get a specific benefit. Flow remembers file names from Cursor, Windsurf, and VS Code across dictation sessions, so proper nouns seen in one session are recognized in the next.<sup>[1]</sup> This is not the same as Variable Recognition or File Tagging (those are Ch14's territory); this is simpler. Flow stores the context it has seen and uses it for accuracy the next time you dictate.

VS Code is included for file-name memory but excluded from file tagging and formatting.<sup>[1]</sup> The distinction matters: if you are a VS Code user expecting full context-aware behavior, you will not get it. Cursor and Windsurf get the complete treatment.

Context reading has built-in performance safeguards so dictation is never slowed down. These safeguards apply across supported apps, including code editors.<sup>[1]</sup>

## Platform Availability and Permissions

Context Awareness is available on Mac and Windows. Windows support is more limited.<sup>[1]</sup> On Mac, you must grant Accessibility permissions in System Settings for the feature to function.<sup>[1]</sup> If you have already been through The Permission Gate (Ch4), you have this covered. If you skipped the Accessibility permission during setup, Context Awareness silently fails.

On Windows, no explicit accessibility permissions are required.<sup>[1]</sup>

One Windows-specific quirk: context-aware formatting adjustments are skipped when you dictate into the Wispr Flow app itself.<sup>[1]</sup> This is a narrow edge case, but if you are composing text inside the Flow interface on Windows, expect raw output rather than context-adjusted output.

The feature is on by default on both platforms. To disable it, open Wispr Flow, go to Settings, then Data and Privacy, and toggle off Context Awareness.<sup>[1]</sup>

## Enterprise Controls

Enterprise admins get a heavier switch. On the Organization settings page under Data Controls, admins can set Context Awareness to Available (the default, where each user controls their own toggle) or Disable for all users, which forces it off for everyone and locks the toggle.<sup>[1]</sup>

When an admin disables it, your local toggle is forced off. Hovering over the locked toggle shows "This setting is managed by your organization."<sup>[1]</sup>

Admins on non-Enterprise plans (including Pro and Teams) see the setting as disabled with an "Enterprise" tag. The control exists but is gated behind the Enterprise tier.<sup>[1]</sup>

## The Privacy Layer

Context Awareness reads screen content, which means it raises questions that the rest of Flow does not. The protections are worth knowing.

Context data is read locally on your device. During an active dictation session, relevant context (nearby text, proper nouns, app metadata, dictionary entries, and, in coding environments, variable and file names) is sent to Wispr's servers to improve transcription accuracy.<sup>[1]</sup> This is the trade-off: better output requires sending more signal to the cloud.

Password fields are excluded. Password field contents are never read or included in context data.<sup>[1]</sup> On Mac, password field detection uses the standard macOS secure text field indicator. Some custom or non-standard password inputs may not be detected.

Screen OCR (full screenshot capture) is off by default. Accessibility-text context is on by default.<sup>[2]</sup> Screenshots, when enabled, are stripped on upload regardless of Privacy Mode and are never persisted server-side.<sup>[2]</sup> The distinction between OCR and accessibility-text matters: OCR captures pixel-level screen content; accessibility-text reads what the operating system's accessibility layer exposes. The default configuration uses the lighter touch.

Privacy Mode, when enabled, means no dictation or context data is retained or used for training.<sup>[1]</sup> Privacy Mode is permanently locked on if you have signed the HIPAA Business Associate Agreement (BAA), or if your enterprise admin enforces Zero Data Retention. Signing the HIPAA BAA is irreversible; you will be asked to type your legal name to confirm.<sup>[1]</sup> The deeper treatment of Privacy Mode, ZDR, and the BAA lives in The Cloud Boundary (Ch21).

Enterprise organizations can also enforce local data deletion policies (auto-delete after 24 hours, or never store) separately from Zero Data Retention.<sup>[1]</sup> Three local storage options exist in Settings under Data and Privacy: store data locally (the default), auto-delete local data every 24 hours, and never store data locally.<sup>[1]</sup>

For sensitive environments (legal, healthcare, or regulated data), disabling Context Awareness entirely is the most conservative option.<sup>[1]</sup> You can still dictate; Flow still applies The Rewrite Pass (Ch1). You just lose the app-aware adjustments.

## What Context Awareness Does Not Do

A few boundaries worth drawing:

Context Awareness does not change your Auto Cleanup level. The Cleanup Dial (Ch7) and The App-Aware Rewrite operate on different axes. One controls how aggressively Flow polishes your raw speech; the other controls how Flow adapts that polished output to the destination app. You can have High cleanup with Casual context, or None cleanup with Formal context. They are independent.

Context-aware formatting does not work inside remote desktop sessions; text pastes with default formatting instead.<sup>[3]</sup> If you are working through Citrix, RDP, or another virtual desktop, Flow cannot read the remote app context. Flow still dictates and pastes via clipboard sharing, but you lose the app-aware adjustments covered in this chapter.

Context Awareness is not the same as Styles. Styles (Ch12) let you configure tone preferences per app category; Context Awareness is the feature that detects which category you are in and applies those preferences. One is the policy; the other is the enforcement.

## Key Points

- The App-Aware Rewrite reads your active app and adjusts tone, formatting, and accuracy before text lands at your cursor.
- Four app categories determine behavior: Email, Work messaging, Personal messaging, and Other, with a fixed priority order for ambiguous apps.
- Mac requires Accessibility permissions for Context Awareness to function; Windows requires no explicit permissions but has more limited support.
- Password fields are never read, screen OCR is off by default, and screenshots are stripped on upload and never stored server-side.
- Enterprise admins can force Context Awareness off for all users; Privacy Mode and the HIPAA BAA lock down what data is retained.
- Context Awareness and the Cleanup Dial are independent controls that affect different aspects of the rewrite pipeline.
