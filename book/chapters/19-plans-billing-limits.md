# Chapter 19: Plans, Billing, and Limits

*In this chapter, you learn how Wispr Flow meters free usage through a weekly word budget, what the three plan tiers include, how billing and invoicing work across platforms, and where discounts, referrals, and trials fit. The goal is a clear map of what costs what, what resets when, and what unlocks at each tier.*

Every voice tool eventually asks the same question: how much can you say for free? Flow answers with a weekly word budget. Not a character count, not a minute limit, not some opaque "credits" system. Words. You dictate them, Flow counts them, and when the budget runs out, the tool slows down and eventually stops. Understanding how The Word Budget works is the difference between hitting a wall mid-sentence and planning around it.

## The Word Budget

The free tier (Basic) does not cap your sessions by time. It caps them by output. On desktop (Mac and Windows), the soft cap is 2,000 words per week. Hit it and Flow keeps working, but slower. The hard cap is 5,000 words; hit that and dictation stops until the counter resets.<sup>[1]</sup> On iOS, the numbers are tighter: a 1,000-word soft cap and a 1,500-word hard cap.<sup>[2]</sup> There is a known display bug on iOS where the hard-cap message reads "1000 words" even though the actual ceiling is 1,500.<sup>[2]</sup>

The critical detail: iOS and desktop track usage independently.<sup>[2]</sup> Words dictated on your phone do not count against your desktop budget, and vice versa. If you spread your dictation across devices, you get more free words in total than either platform alone would suggest.

The counter resets every Sunday at 12am PT.<sup>[1]</sup> On desktop, the actual reset is computed using your device's local time zone, so the displayed "PT" label may not match your exact reset moment.<sup>[2]</sup> Unused words do not carry over.<sup>[3]</sup>

### The New-User Bonus

Some new signups on Mac and Windows land on the free tier with a 2,000-word weekly cap instead of the standard 14-day Pro trial.<sup>[3]</sup> The first time you hit 2,000 words, Flow grants a one-time bonus of 8,000 extra words, raising that week's cap to 10,000.<sup>[1,3]</sup> A notification appears; the "Keep dictating" button dismisses it, and the bonus is already active.<sup>[3]</sup> After the bonus week ends, the cap returns to 2,000 words. The bonus is a one-time event. It does not repeat.<sup>[3]</sup>

Not everyone gets the bonus. Referred users, students, and enterprise accounts are excluded.<sup>[3]</sup> The free-tier experience transitions to the standard view seven days after onboarding, regardless of whether you ever hit the cap.<sup>[3]</sup>

## Three Plans

Flow offers three tiers: Basic (Free), Pro, and Enterprise.<sup>[1]</sup> All three use the same voice-to-text engine; transcription accuracy is identical across tiers.<sup>[1]</sup> The difference is what you can do with the output and how much of it you can produce.

**Basic** gives you core dictation with the weekly word limits described above. You keep your dictionary, snippets, and history. Pro-only features like Command Mode and unlimited words are locked.

**Pro** removes all word limits across every platform. It adds Command Mode for voice-driven editing, prioritized support, early access to new features, and support for 100-plus languages.<sup>[1]</sup> Pro is available as a personal subscription or as multi-seat team billing with centralized admin controls.<sup>[1]</sup>

**Enterprise** includes everything in Pro, plus dedicated support, advanced admin and security controls, usage dashboards, IT Admin seats, and team leaderboards.<sup>[1]</sup> IT Admin seats are always free and never counted toward paid seats; they have no desktop app access and manage the organization from the web portal only.<sup>[1,4]</sup>

### Plan Changes

Upgrades take effect immediately. Downgrades take effect at the end of your current billing cycle.<sup>[1]</sup> Your data is preserved through downgrades; dictionary entries, snippets, and history remain available, and Pro-only features reactivate if you upgrade again.<sup>[1]</sup>

Annual billing offers a discount over monthly. Switch between cycles in Settings, then Account, then Manage Subscription.<sup>[1]</sup>

## Billing Across Platforms

How you pay depends on where you signed up, and this is where things get fractured.

**Individual Pro (Stripe):** Desktop and web subscriptions go through Stripe. Download invoices via Settings, then Plans and Billing, then Manage Subscription, which opens the Stripe billing portal.<sup>[4]</sup> Payment emails from @stripe.com or @link.com are legitimate; Wispr uses Stripe as its processor, so receipts come from Stripe, not Wispr.<sup>[4]</sup>

**Team and Enterprise:** Admins download invoices from admin.wisprflow.ai in the billing section.<sup>[4]</sup>

**iOS (Apple):** Purchases made through the App Store are handled entirely by Apple. Receipts come from no_reply@email.apple.com, and purchase history lives at reportaproblem.apple.com.<sup>[4]</sup> You manage the subscription in your iPhone's Settings under your name, then Subscriptions.

**Android:** There is no in-app subscription management on Android. Manage your subscription at app.wisprflow.ai.<sup>[1]</sup>

This platform split has real consequences. Discounts cannot be applied to App Store subscriptions; if you subscribed via the App Store and want a discount, you must cancel that subscription first and resubscribe through the desktop app or website.<sup>[5]</sup> Referral reward credits also require an active paid subscription purchased through wisprflow.ai, not the App Store and not Enterprise.<sup>[6]</sup>

## When Payment Fails

When Stripe cannot charge your payment method, the subscription enters a past-due state.<sup>[7]</sup> Team, enterprise, and iOS paid users keep full access during this window. Personal Pro users on desktop lose Pro access immediately.<sup>[7]</sup>

Wispr emails the billing admin when the payment first fails, then sends a final reminder six days later if it is still failing.<sup>[7]</sup> Once Stripe exhausts its retry attempts and marks the subscription as canceled, your account downgrades to Basic. Weekly word caps apply and Pro features are disabled.<sup>[7]</sup> The exact length of the past-due window depends on Stripe's retry schedule, not a fixed day count.<sup>[7]</sup>

Your data is not lost on downgrade. Dictionary, history, and settings are preserved. Pay the outstanding invoice and Pro restores, usually within minutes.<sup>[7]</sup>

## The Trial

Flow offers a 14-day Pro trial for new users.<sup>[8]</sup> On the last day (when one day remains), a personalized Trial End Value Summary modal appears on Mac and Windows, showing your usage and two options: upgrade to keep unlimited words, or continue on Basic at 2,000 words per week.<sup>[8]</sup> After the trial ends, a notification appears during the grace period the next time you dictate, offering only the upgrade option.<sup>[8]</sup>

Teams get a short grace period after the trial ends before the team loses access.<sup>[8]</sup> If billing is not added within that window, the team is disbanded and all members are removed.<sup>[1]</sup>

The trial summary is rolling out gradually as of Q2 2026; not all eligible users will see it.<sup>[8]</sup>

## Discounts

Six categories qualify for discounted pricing: Student, Education (non-student), Non-profit, Accessibility support, Military, and Senior citizen.<sup>[5]</sup> Apply through the web support page at wisprflow.ai/support (for PDFs) or through the desktop app's Help menu (for image verification).<sup>[5]</sup> Verification submission is limited on mobile: iOS has no file attachments, and Android's discount-specific forms are not available in-app.<sup>[5]</sup>

Only one promotional code can be active at a time.<sup>[5]</sup>

### Student Accounts

Student accounts carry two special properties. First, they are not subject to the free-tier word cap that some new signups see.<sup>[5]</sup> Second, approved students receive roughly a 90-day trial (compared to the standard 14 days), calculated from the account creation date by default.<sup>[9]</sup> If you apply for student pricing months after signing up, your effective remaining trial may be shorter than 90 days; support can recalculate from the approval date, but this is not automatic.<sup>[9]</sup>

Student pricing starts at $7.50/month or $6/month billed annually (USD defaults; actual pricing varies by currency and country, resolved server-side based on IP location).<sup>[9]</sup> On iOS, weekly, monthly, and yearly student plans are available through the App Store; weekly plans are App Store only.<sup>[9]</sup>

## The Referral Program

Share your referral link and the friend who signs up gets a 30-day Pro trial.<sup>[6]</sup> You earn one free month of Pro per successful referral.<sup>[6]</sup> The activation threshold: your friend must dictate at least 2,000 words or upgrade to Pro.<sup>[6]</sup>

Reward credits require an active paid subscription purchased through wisprflow.ai. App Store subscribers and Enterprise members can send invitations and give friends the extended trial, but will not earn rewards themselves.<sup>[6]</sup>

Students who sign up for a Student plan receive a 90-day trial, which takes precedence over the 30-day referral trial.<sup>[6]</sup>

The "Apply referral" tab (for entering a code after signup without a link) is available on Mac and Windows only. iOS users cannot apply referral codes in-app; they must sign in on desktop or contact support.<sup>[6]</sup>

You can refer while on the free plan. Credits are tracked and apply automatically when you upgrade.<sup>[6]</sup> There is no limit to how many people you can refer.<sup>[6]</sup>

### Referral Code Regeneration

If you regenerate your referral code, the old link stops working for new signups. Existing referrals are automatically updated to the new code.<sup>[6]</sup>

## Word Budget Troubleshooting

If your word counter does not reset after Sunday, check three things. First, confirm your plan badge says Basic (word limits only apply to Basic and inactive subscriptions; Pro, Team, Student, and Enterprise plans with active subscriptions have no weekly limits).<sup>[2]</sup> Second, verify that Sunday midnight has passed in your time zone. Third, check whether the count matches across views; if it is correct in one place but stale in another, restart Flow to sync.<sup>[2]</sup>

If restarting does not fix it, sign out and sign back in. Be aware that signing out on desktop clears local-only data including transcript history, dictionary entries, and local notes (cloud-synced content is preserved).<sup>[2]</sup>

## Key Points

- Free Flow runs on a weekly word budget that resets every Sunday, not a per-session time limit or a monthly quota.
- iOS and desktop track usage independently, so spreading dictation across devices effectively doubles the free allowance.
- Billing is fragmented across Stripe, Apple, and the web portal; where you subscribed determines how you manage invoices and whether discounts apply.
- Student accounts bypass the free-tier word cap entirely and receive a roughly 90-day trial instead of the standard 14 days.
- Referral rewards require a paid subscription through wisprflow.ai; App Store and Enterprise subscribers can share but cannot earn credits.
- When payment fails, personal Pro users lose access immediately while team and enterprise users retain it during the retry window.
- Downgrades preserve all your data; upgrading again restores Pro features without rebuilding your dictionary or snippets.
