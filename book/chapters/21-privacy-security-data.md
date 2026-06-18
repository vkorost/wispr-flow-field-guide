# Privacy, Security, and Your Data

*In this chapter: every word you dictate crosses a network boundary. This chapter maps what happens to your audio once it leaves the device, what controls exist to limit retention and training use, and where the documented guarantees end. The Cloud Boundary is the frame for deciding what to say and what to type.*

Your voice leaves the device. Every syllable you dictate into Wispr Flow is streamed to a backend server for transcription; audio is not persisted locally on the client.<sup>[1]</sup> That is the architectural fact that shapes every privacy question in this chapter, and it is non-negotiable. There is no offline mode. There is no on-device speech model. The Cloud Boundary is the line your audio crosses the moment you press the hotkey, and every control documented below operates on the far side of that line.

Understanding where that boundary sits, what the company retains on the other side, and which knobs you can turn is the difference between informed use and hopeful use. This chapter sticks to what the sources say.

## How the Processing Model Works

Flow's transcription pipeline is cloud-only. Audio is streamed over TLS 1.2 or higher with forward-secrecy cipher suites to Wispr's backend, where it is decrypted and processed.<sup>[1]</sup> The service does not provide end-to-end encryption in the strict cryptographic sense; the backend *must* decrypt audio to perform transcription.<sup>[1]</sup> Data at rest is encrypted (typically AES-256) at the database and object-storage layers, and sensitive OAuth and SSO credentials receive an additional application-layer encryption pass.<sup>[1]</sup>

No voiceprints or biometric identifiers are collected or stored. Wispr states explicitly that it does not derive voice embeddings or any biometric identifier as defined under BIPA, GDPR Article 9, or CCPA.<sup>[1]</sup>

All customer data is processed and stored in the United States. There is no European or regional processing location. For EU and UK customers, cross-border transfers are governed by the EU Standard Contractual Clauses (June 2021), with a UK Addendum available.<sup>[1]</sup>

## Privacy Mode and Zero Data Retention

The single most consequential toggle in Flow's privacy surface is Privacy Mode, also called Zero Data Retention (ZDR). The behavior splits cleanly into two cases.<sup>[1]</sup>

With Privacy Mode on, audio, transcripts, prompts, and derived content are not retained and are not used for model training by Wispr or any subprocessor. Dictation content flows through processing without storage; the server enforces sanitization independently of the client.<sup>[1]</sup>

Without Privacy Mode (the default for trial and standard accounts), audio and transcription data are retained after processing and may be used to evaluate, train, and improve Wispr's models.<sup>[1]</sup>

Privacy Mode is available on enterprise plans, where it can be enforced at the organization level so individual users cannot disable it.<sup>[1]</sup> Whether Privacy Mode is available on the free tier is not specified in the documentation (test-it).

Privacy Mode is permanently locked on in two situations: when a user signs a HIPAA Business Associate Agreement, or when an enterprise admin enforces Zero Data Retention.<sup>[1,2]</sup> Once a BAA is signed, Privacy Mode cannot be disabled. That signing is irreversible.<sup>[2]</sup>

## What Privacy Mode Does Not Cover

Privacy Mode governs *retention and training*, not the location of processing. Audio still travels to the cloud. The transcription still happens on remote servers. Privacy Mode means the server discards the artifacts after processing rather than writing them to persistent storage.

Context Awareness has two separately toggled components: accessibility-text context (on by default, reads text from the active app's accessibility tree) and Screen OCR (off by default, captures a full-display screenshot to extract proper nouns).<sup>[2]</sup> Screen context captured for Context Awareness is stripped on upload regardless of Privacy Mode and is never persisted server-side.<sup>[1]</sup> The documentation explicitly confirms this stripping behavior for the Screen OCR path; accessibility-text context is read locally on the device and sent to Wispr's servers during an active dictation session to improve accuracy.<sup>[2]</sup> Enterprise admins can disable Context Awareness entirely from the Organization settings page under Data Controls.<sup>[2]</sup>

Snippets and custom dictionaries are stored in Wispr's backend and synced across devices regardless of Privacy Mode status. Wispr classifies these as user-authored productivity assets, not dictation content, and they receive the same at-rest encryption and access controls as other account data.<sup>[1]</sup>

## Local Data Storage Options

Independent of server-side retention, Flow offers three local-data storage modes on desktop (Mac and Windows), configured under Settings, then Data and Privacy.<sup>[3]</sup>

The first option, Store data locally, is the default. It keeps transcripts and polish history on the device. The second, Auto-delete local data every 24 hours, automatically removes transcripts and polish history older than 24 hours. The third, Never store data locally, immediately deletes all transcripts and polish history and prevents future storage.<sup>[3]</sup>

Choosing auto-delete or never-store permanently destroys existing local data, including transcripts, polish history, and Transform/Instruct history. The action cannot be undone.<sup>[3]</sup> Both deletion options also hide the "Your Voice" tab in the Insights page, because Voice Profile requires locally stored transcripts to function. The tab returns automatically if you switch back to storing data locally.<sup>[3]</sup>

Enterprise organizations can manage this setting centrally. Under a "Never store" policy, the dropdown is fully disabled. Under a "24-hour auto-delete" policy, the dropdown remains interactive but the "Store data locally" option is removed. Users can always choose a *more* restrictive option than what their organization requires.<sup>[3]</sup>

On iOS, the equivalent control is a toggle called "Automatically delete transcripts" under Settings, then Data and Privacy (off by default). When enabled, transcripts from previous days are deleted the next time the app opens or returns to the foreground, and at sign-in. Today's transcripts are always kept.<sup>[3]</sup>

On Android, there is no separate privacy-mode or data-storage setting. The only way to clear all transcripts is to sign out, which triggers a confirmation dialog and permanently deletes transcript data.<sup>[3]</sup>

## Enterprise Data Controls

Enterprise plans expose three local-data policy options in the admin portal: Store normally (the default), Delete after 24 hours, and Never store.<sup>[1]</sup> These are enforced at the organization level and apply to all members.

Enterprise admins can manage Context Awareness, ZDR enforcement, and local storage policy from the Organization settings page under Data Controls.<sup>[1,2]</sup> A HIPAA Business Associate Agreement is available for healthcare customers; signing the BAA automatically enables Privacy Mode and locks it on permanently.<sup>[1]</sup>

## Certifications and Compliance

As of Q2 2026, Wispr holds the following attestations.<sup>[1]</sup>

SOC 2 Type I was completed April 2026 by A-LIGN with a clean, unqualified opinion. The scope covers Security.<sup>[1]</sup> SOC 2 Type II has its observation period underway; the report has not yet been issued.<sup>[1]</sup> ISO 27001:2022 Stage 1 was completed April 2026 by A-LIGN, with Stage 2 scheduled for June 2026.<sup>[1]</sup>

Penetration testing was most recently performed by BSK Security LLC in November 2025, with the next engagement planned with Doyensec after the SOC 2 Type I completion.<sup>[1]</sup>

A historical note: Wispr previously held a SOC 2 Type II (Accorp Partners) and ISO 27001 (Gradient) certification. Both were proactively invalidated in March 2026 due to platform integrity concerns at the original auditor.<sup>[1]</sup>

Not currently held: FedRAMP, PCI DSS (Stripe handles payments under PCI DSS Level 1), SOC 1, and SOC 3.<sup>[1]</sup>

A HIPAA Business Associate Agreement is available for healthcare customers. Supporting controls include a HIPAA Internal Privacy Policy, PHI de-identification procedures, breach notification policy, security awareness training, encryption of PHI at rest and in transit, and audit logging.<sup>[1]</sup>

## Data Retention, Destruction, and Deletion

Data destruction follows NIST 800-88 standards for physical media; cloud data is purged per AWS and subprocessor contractual terms. Automated database backups are retained for seven days.<sup>[1]</sup>

When a user requests account deletion, Wispr executes the deletion synchronously as part of the API request rather than queuing it for a batch job. All data across the primary database is removed in the same request: account, configuration, dictation history (where retained), notes, snippets, dictionaries, preferences, usage stats, referrals, and personalization data. A separate audit record noting that the deletion occurred is kept for compliance purposes only.<sup>[1]</sup>

Audio recordings are stored locally for 14 days on desktop; after that, audio is automatically deleted and recovery is no longer possible (unless a deletion policy removes data sooner).<sup>[3]</sup> Transcript text and the history entry remain available unless a deletion policy is active.<sup>[3]</sup> Under a Never Store (ZDR) policy, audio is never saved to history and retry from saved audio is unavailable.<sup>[3]</sup>

Dismissed transcripts on Mac and Windows are recoverable within 14 days via a "Recover" link in History. After 14 days, the audio is automatically deleted and recovery is no longer possible.<sup>[3]</sup>

## The Context Awareness Privacy Dimension

Context Awareness, covered in depth in Chapter 9 (The App-Aware Rewrite), has a privacy surface worth restating here.

When Context Awareness is on (the default on Mac and Windows), relevant text data from the active application is sent alongside the audio to improve transcription accuracy. Password field contents are never read or included. On Mac, password field detection uses the standard macOS secure text field indicator; some custom or non-standard password inputs may not be detected.<sup>[2]</sup>

Screen OCR, the opt-in component, captures a full-display screenshot to extract proper nouns. Any captured screenshot is stripped on upload regardless of Privacy Mode and is never persisted server-side.<sup>[1,2]</sup>

Context Awareness can be disabled entirely under Settings, then Data and Privacy.<sup>[2]</sup> Enterprise admins can disable it for all users from the Organization settings page under Data Controls. When an admin disables it, the user preference is forced off and the toggle is locked.<sup>[2]</sup>

The context-awareness feature drew scrutiny in late 2025 when users discovered that the Screen OCR component was transmitting active-window screenshots to cloud servers without what they considered sufficient disclosure. The details of the community response are not documented in the help center. The current documentation describes the two components, their defaults, and the stripping behavior. Whether you enable Screen OCR depends on your threat model. The controls exist. The architectural guarantee is that screenshots are stripped on upload and never persisted.

## The Company Behind the Data

Wispr AI, Inc. is a Delaware C-corporation, founded in 2023, privately held, headquartered at 444 Townsend Street, San Francisco, CA 94107.<sup>[1]</sup> The security program is led by CTO/CISO Sahaj Garg, with CEO Tanay Kothari as executive sponsor.<sup>[1]</sup>

## What to Route and What Not to Route

The documented controls are real. Privacy Mode with ZDR means dictation artifacts are processed in memory and discarded. The SOC 2 Type I is complete, and the Type II observation period is underway. HIPAA BAA is available and locks Privacy Mode on permanently. Screen OCR is opt-in and stripped on upload. Data destruction follows NIST 800-88.

The limits are also real. Transcription is cloud-only. No end-to-end encryption. The backend can and does decrypt your audio. Without Privacy Mode, your data may train models. And the compliance program is in a transition period, with the new SOC 2 Type II not yet issued.

For everyday dictation of emails, messages, notes, and code prompts, these controls are sufficient for most users who enable Privacy Mode. For credentials, .env contents, material under NDA, or regulated data outside an active BAA, the safest path is not to speak it at all. That is not a judgment on the company. It is a consequence of the architecture: your voice crosses the Cloud Boundary, and the controls operate on the other side.

## Key Points

- Every dictation crosses the Cloud Boundary to remote servers; there is no offline or on-device transcription mode.
- Privacy Mode provides zero data retention for dictation artifacts but does not change where processing occurs.
- Signing a HIPAA BAA permanently locks Privacy Mode on; the action is irreversible for the life of the account.
- Screen OCR is opt-in and stripped on upload; Context Awareness text reading is on by default and can be disabled.
- SOC 2 Type I is complete as of April 2026; SOC 2 Type II is in its observation period and not yet issued.
- Local data storage options let you control transcript retention independently of server-side privacy settings.
- For sensitive or regulated content outside an active BAA, the safest approach is to type rather than dictate.
