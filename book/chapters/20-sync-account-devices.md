# Chapter 20: Sync, Account, and Devices

*In this chapter: your Wispr Flow account is the thread that ties your devices together, carrying dictionary entries, snippets, styles, and subscription status across Mac, Windows, iPhone, and Android. Understanding what syncs, what stays local, and what vanishes on sign-out is how you keep your setup intact and avoid losing work.*

Every tool you use across multiple devices forces you to answer a question: where does your stuff live? With Wispr Flow, the answer is split. Some data follows your account wherever you sign in. Some data stays locked to the device it was created on. And some data disappears the moment you sign out, with a warning dialog that is easy to tap past in a hurry. The split is deliberate, but if you do not know where the lines are, you will lose something you care about. This chapter maps those lines.

## The Synced Identity

Your Flow account is the container. Sign into the same account on a second Mac, a Windows laptop, an iPhone, and an Android phone, and a set of data appears on each one automatically: your subscription status, your dictionary entries, your snippets, your selected languages, and your personalization styles.<sup>[1]</sup> That sync is the feature. It means you can build a dictionary on your desktop and have it waiting on your phone by the time you pick it up.

But the sync has boundaries. Transcription history does not cross devices. It is stored locally on each one, and on no platform does Flow download transcript text from the server to another device.<sup>[1]</sup> On Mac, Windows, and iOS, transcript text and audio are uploaded to Wispr's servers for service improvement unless Privacy Mode is on. On Android, only metadata is uploaded; text and audio never leave the device.<sup>[1]</sup>

The practical consequence: if you dictate something important on your phone and want to reference it later on your laptop, you will not find it there. The transcript lives on the phone. Plan accordingly.

## What Syncs and What Does Not

The full picture, as of Q2 2026:

**Syncs automatically:** subscription and Pro status, dictionary entries, snippets (on Android, syncs when you open the Snippets screen), selected languages, personalization styles (on Android, only after you tap Save).<sup>[1]</sup>

**Syncs with caveats:** daily and weekly streaks refresh from the server periodically. Total words and WPM sync, but daily and weekly counts may differ by device. Languages and styles sync; hotkeys, mic selection, and sounds are per-device.<sup>[1]</sup>

**Does not sync:** transcription history, stored locally on each device. Notification preferences, saved locally on each device and configured separately on each machine.<sup>[2]</sup> Cleanup Level (covered in Chapter 7, The Cleanup Dial) is stored locally per device. Pinned-note status on desktop is local per device (see Chapter 16, The Scratchpad).

**Image attachments in notes** sync between desktop devices. Supported formats: PNG, JPEG, and WebP. GIF is not supported by the desktop client. Limit: 5 MB per image, up to 100 images per note.<sup>[1]</sup>

## Setting Up a Second Device

The setup is short. Download Flow from wisprflow.ai/downloads (Mac or Windows) or from your device's app store (iOS or Android). Sign in using the same method you used originally: Google, Apple, Microsoft, SSO, or email. On iOS, only Google and Apple appear by default; tap More Options for the rest.<sup>[1]</sup>

One mistake kills the sync before it starts: signing in with a different method. Google and Apple create separate accounts even if the email address is the same. If your subscription shows on your Mac but not your phone, that is the first thing to check.<sup>[1]</sup>

Once signed in, your subscription, dictionary, and snippets appear automatically. On Android, snippets sync at login and again when you open the Snippets screen.<sup>[1]</sup> Style changes on Android require tapping Save before they sync; tapping Cancel discards the draft.<sup>[1]</sup>

## What Happens When You Sign Out

This is where the split matters most, and where each platform behaves differently.

**Mac and Windows:** signing out wipes your local Wispr Flow data. That includes transcript history, dictionary entries, notes, and meetings/calendar cache. App preferences (language, shortcuts, styles) are preserved.<sup>[3]</sup>

**iOS:** signing out does *not* delete any local data.<sup>[3]</sup>

**Android:** signing out deletes only transcripts. Other settings are preserved. The confirmation dialog reads "Sign out and delete transcripts?" and it means exactly that.<sup>[1,3]</sup>

The asymmetry is worth internalizing. If you sign out on a Mac, your dictionary is gone from that machine until you sign back in and re-sync. If you sign out on an iPhone, everything stays. If you sign out on Android, your transcripts are permanently destroyed, but your dictionary and snippets remain. Three platforms, three rules.

## Transcripts, Audio, and the 14-Day Window

Dismissed transcripts (not deleted) are recoverable within 14 days on Mac and Windows.<sup>[3]</sup> Audio is auto-deleted after 14 days regardless; after that, Retry and Recover are unavailable.<sup>[3]</sup> Accounts using Never Store (Zero Data Retention) never save audio at all, and recovery is not possible under that policy.<sup>[3]</sup> For the full treatment of retention policies and Privacy Mode, see Chapter 21, The Cloud Boundary.

The "Your Voice" tab is hidden when an auto-delete or never-store policy is active.<sup>[3]</sup>

## Account Management

Your account details live in Settings on every platform. On Mac and Windows, click the gear icon, then Account. On iOS, open the Menu and tap Account. On Android, open the dashboard drawer and tap Account.<sup>[4]</sup>

Profile pictures change immediately when you select a new image (5 MB maximum).<sup>[4]</sup> Name changes require tapping Save. On Mac and Windows, Flow validates your name field and rejects entries that look like a password, returning "This looks like a password, not a name."<sup>[5,6]</sup> That check exists because users have accidentally entered their password in the name field during mobile signup, causing it to appear in emails and referral links.<sup>[5]</sup> If that happened to you, the fix is a three-step sequence: reset your password, update your display name, and regenerate your referral code.<sup>[5]</sup>

## Changing Your Email or Sign-In Method

You cannot. Your account is permanently tied to the credentials you used at creation. Google, Apple, Microsoft, email/password, and Enterprise SSO are all separate identity rails, and none can be relinked after the fact.<sup>[6]</sup>

The only path is to delete your current account and create a new one. Before you do: save your dictionary entries and snippets manually (they will not transfer), cancel any active subscription and contact support for billing adjustments, and understand that dictation stats, transcription history, Flow Notes, team membership, referral credits, AI learned preferences, and HIPAA BAA signing status are all permanently lost.<sup>[6]</sup>

Email aliases containing "+" (like user+alias@example.com) are not supported for email/password accounts. You will see an error asking you to use your original email address. This restriction does not apply to Apple, Google, or Microsoft sign-in.<sup>[4]</sup>

## Password Reset

Password resets apply only to email/password accounts. If you signed in with Google, Apple, Microsoft, or SSO, credentials are managed through those providers.

On Mac and Windows, there is no in-app password reset. You reset through a browser at wisprflow.ai/login.<sup>[7]</sup> On iOS, tap More Options on the sign-in screen, then Continue with Email, then Forgot password. A captcha challenge follows.<sup>[7]</sup> On Android, enter your email, tap Continue, then Forgot password, then Send reset link. No captcha is required on Android.<sup>[7]</sup>

After you reset your password, all sessions on all devices are signed out.<sup>[4,7]</sup> Sign back in everywhere. In rare cases a session may remain active and you will need to sign out manually from that device.<sup>[7]</sup>

## SSO and Enterprise Accounts

SSO lets you authenticate using your organization's identity provider. It also works when initiated from your provider (clicking the Wispr Flow tile in Okta, for instance). SSO enforcement requires an active enterprise subscription; if that subscription lapses, enforcement lifts automatically.<sup>[4]</sup> For the full treatment of SSO configuration, SCIM provisioning, and domain capture, see Chapter 23, The Org Layer.

## The Monthly Flow State Email

Once a month, if you dictate enough words, Flow sends a "Flow State" summary to your inbox: words dictated, words per minute, longest streak, top app, peak day and time, a calendar heatmap, and a rotating insight.<sup>[8]</sup> It is a marketing email, which means you can unsubscribe via the link at the bottom of any edition. Transactional emails (billing alerts, password resets, team invitations) cannot be disabled.<sup>[8]</sup>

On Android, push notifications are gated by the notification permission you grant during onboarding. Decline it, and you receive none.<sup>[8]</sup> Enterprise admins who want to suppress marketing emails across an entire domain must contact support; there is no self-serve toggle (as of Q2 2026), and processing takes a few business days.<sup>[8]</sup>

## Notification Preferences

On Mac and Windows, Flow groups notifications into toggleable categories: Suggestions, Announcements, Milestones, and Team updates (visible to enterprise users only).<sup>[2]</sup> Each toggle mutes all notifications in that category. Changes take effect immediately and are saved locally per device; configure them separately on each machine.<sup>[2]</sup>

A set of critical notifications always appears regardless of your settings: permission alerts, microphone hardware errors, helper app failures, billing trial-end alerts, paste and polish feedback, incident alerts, and dictation text-recovery notifications.<sup>[2]</sup>

iOS has a single Push Notifications toggle in Settings and a separate "Allow Live Activities" toggle managed at the OS level. Android has the onboarding-granted notification permission and nothing more granular.<sup>[2]</sup>

## Deleting Your Account

Account deletion is available in Settings on Mac, Windows, and iOS.<sup>[4]</sup> Android does not have an in-app Delete Account button; use the desktop app, or submit a request through Report an Issue with the request type set to Account management.<sup>[4]</sup>

Deletion removes your dictionary entries, snippets, Flow Notes, and local database records. Your login credentials and cloud-stored transcription history are fully removed after the request is processed. Active paid subscriptions are cancelled immediately. No prorated refund is issued.<sup>[4]</sup> Local history on other devices is not removed automatically; delete the app on each device to clear it.<sup>[4]</sup>

If you are the sole admin of an enterprise with other members, assign another admin first. If you are the paying admin, transfer billing before deleting.<sup>[6]</sup>

Account merging is not supported. If you end up with two accounts, pick one and manually recreate your dictionary entries in the keeper.<sup>[4]</sup>

## The iCloud and OneDrive Trap

One hazard worth flagging: if Wispr Flow's local data folder ends up inside an iCloud, OneDrive, or similar cloud-synced location, those services can make local app files read-only, which interferes with how Flow saves data. The result is database corruption and a permanent error state that previously required manual intervention.<sup>[1]</sup> Flow now auto-recovers on restart, but the recommendation stands: keep Flow's local data folder out of cloud-synced directories.<sup>[1]</sup>

## Key Points

- Your account syncs dictionary, snippets, styles, and subscription status across all devices, but transcription history stays local and never crosses platforms.
- Signing out behaves differently on each platform: Mac and Windows wipe local data, iOS preserves everything, and Android deletes only transcripts.
- You cannot change your sign-in method or email after account creation; the only path is deleting the account and starting fresh with lost data.
- Password resets sign out all sessions on all devices, so expect to re-authenticate everywhere after a reset.
- Notification preferences are per-device on desktop and have no cross-device sync, so configure them separately on each machine you use.
- Keep Flow's local data folder out of iCloud, OneDrive, and similar sync services to avoid database corruption.
