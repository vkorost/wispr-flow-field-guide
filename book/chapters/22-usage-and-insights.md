# Chapter 22: Usage and Insights

*In this chapter: Flow tracks every word you dictate and turns that data into a personal dashboard of speed, streaks, and habits. The Usage tab shows you how you compare to keyboard typists, the Leaderboard ranks your team, and the Voice Profile builds a portrait of your dictation style. Knowing what Flow measures helps you use the numbers and decide what to share.*

Every tool that watches you work eventually tells you what it saw. Flow is no exception. The difference is that Flow's observations are surprisingly specific, refreshingly honest, and available only on the desktop app. If you have been dictating for more than a few days, there is already a small dossier waiting in the sidebar.

The concept at the center of this chapter is what we will call The Voice Profile: the idea that your dictation habits, accumulated over time, form a recognizable fingerprint. Flow collects the raw numbers (words per minute, total words, streak days, corrections) and, once you cross a threshold, synthesizes them into a personalized summary. The Voice Profile is not a leaderboard trophy or a gamification gimmick. It is a mirror. Whether you look at it and adjust your habits or ignore it entirely is your call. But it exists, and it is built from your data, so you should understand what feeds it.

## The Usage Tab

The Insights page lives in the left sidebar of the Mac and Windows desktop app.<sup>[1]</sup> It does not exist on iOS or Android. If you are a mobile-only user, this chapter describes a room you cannot enter yet (as of Q2 2026).

Open Insights and you land on the Your Usage tab, which presents five tiles.

**Words per minute.** An animated radial gauge shows your average dictation speed as a whole number, plus a percentile ranking against global keyboard typists.<sup>[1]</sup> The comparison baseline is keyboard typing, not other Flow users. The average keyboard typist clocks roughly 52 WPM, so dictating at 100 WPM puts you in the top 4%, and 150 WPM lands around the top 0.5%.<sup>[1]</sup> The percentile floors at "Top 0.1%" and caps at "Top 99%." Both the WPM number and the percentile update immediately after each dictation. WPM calculation works accurately for all supported languages, including Japanese, Chinese, Korean, Thai, Khmer, and Lao.<sup>[1]</sup>

**Corrections by Flow.** This counts every transcription error, filler word, and automatic fix Flow applied during your sessions, including dictionary substitutions.<sup>[1]</sup> It is a running tally of the work the Rewrite Pass (Ch1) did on your behalf. If the number is high relative to your word count, it may mean you rely heavily on course correction, or it may mean your microphone setup is feeding Flow noisy input (see The Input Chain, Ch18).

**Total words dictated.** A lifetime counter with a month-over-month comparison badge. The badge compares your word count so far this month against the same number of days in the previous month and updates after each dictation.<sup>[1]</sup> When no prior-month data exists, the badge hides. The hover tooltip appears only when the change is nonzero.

**Desktop app usage breakdown.** A horizontal bar chart categorizes your dictation time across Personal Messages, Work Messages, Emails, AI Prompts, Documents, and Other Tasks.<sup>[1]</sup> The darkest bar is your top category; the lightest bars are everything else. Hover any segment to see a usage-intensity label (Light, Moderate, or Power usage) and the word count. This chart reflects desktop dictation only; mobile dictation is not included.<sup>[1]</sup>

**Usage streak heatmap.** A calendar view of your dictation activity. Days in your current streak glow; the glow ends on the most recent day you dictated, not on today if you have not yet spoken.<sup>[1]</sup> Other active days shade by word count. Hover any cell to see total words, apps used, and your top app for that day. The heatmap reaches back to your account creation date or March 1, 2025, whichever is more recent.<sup>[1]</sup>

A Share button at the top opens a carousel of branded share cards. Each card can be copied, downloaded as an image, or shared to X or LinkedIn.<sup>[1]</sup> Nine card types exist in this order: Flow Highlights, Total Words, Flow Streak, How Fast You Flow, Your Flow Activity, Where You Flow, Voice Profile, Flow Superlatives, and Peak Time.<sup>[1]</sup> The last three cards appear only after a Voice Profile has been generated.

One practical note: the Share button stays disabled until your main stats finish loading. It may activate before the heatmap finishes, so do not take a grayed-out button as an error. Wait a beat.<sup>[1]</sup>

## The Leaderboard

The second tab on the Insights page is the Leaderboard, available to Team and Enterprise (Business plan) users.<sup>[1]</sup> If you are on a solo plan, you see a locked preview with a prompt to create or join a team, upgrade to Enterprise, or invite teammates, depending on your account state.<sup>[1]</sup>

For those with access, the Leaderboard shows a podium view of top-ranked members and a full table below it. You can sort by five metrics: Total words, Words per minute, Current daily streak, Desktop words, and Mobile words.<sup>[1]</sup> Two of those metrics, WPM and Current daily streak, are available only when the time-range filter is set to "All time"; they hide under "This week."<sup>[1]</sup> The leaderboard refreshes hourly.<sup>[1]</sup>

The table paginates. A "Jump to me" button scrolls to your row, which is useful once the team grows past the point where you can spot yourself at a glance.

Enterprise admins can hide the Leaderboard entirely via the "Hide team leaderboard" toggle in the User Management section of the admin portal (web).<sup>[1]</sup> When enabled, the Leaderboard tab disappears for everyone in the organization, including admins. Whether hiding it is wise depends on your culture. Some teams thrive on visible ranking; others find it corrosive. The toggle exists; use your judgment.

## The Voice Profile

The third tab on the Insights page is called Your Voice.<sup>[1]</sup> It is covered in a separate help-center article and is visible only when your data storage setting is "Store locally."<sup>[1]</sup> If you or your organization uses a data-deletion policy (auto-delete transcripts every 24 hours, or never store locally), the tab hides. Switch the storage setting back to "Store locally" to restore it; any bookmarked link to Your Voice redirects to Your Usage in the meantime.<sup>[1]</sup>

What does the Voice Profile actually contain? Based on available information (single-source; verify on your own device), the Voice Profile is a personalized dictation-habits summary that includes elements like a "superpower," a headline, your peak dictation time and place, a catch phrase, your most-used and most-corrected word, and a persona label. Generation reportedly begins after you have dictated at least 2,000 words, because the profile is built from locally stored transcription data. *This description comes from a single source with no help-center corroboration as of Q2 2026. The feature is real: the share cards reference it, the tab exists, and it requires local data storage. But the specifics of what the profile says about you are best confirmed by generating your own.*

Three share cards in the carousel depend on the Voice Profile being generated: Voice Profile, Flow Superlatives, and Peak Time (labeled "When you Flow the most").<sup>[1]</sup> Until you hit the generation threshold, those slots remain empty.

## What the Numbers Mean (and What They Do Not)

The WPM gauge is the tile most humans fixate on. It is worth understanding what drives it.

Your WPM reflects dictation speed, not thinking speed. If you pause for five seconds mid-sentence to choose a word, that silence lowers your average. If you speak in rapid bursts with long gaps between them, the number compresses. The metric rewards continuous speech, which is the same behavior the Rewrite Pass handles best. Hesitant, fragmented input gives the cleanup engine less context to work with (see The Cleanup Dial, Ch7) and produces a lower WPM. There is a feedback loop: dictating more fluidly makes the output better *and* makes the number go up.

The percentile comparison to keyboard typists is generous by design. Most humans type at roughly 52 WPM, which is not fast. If you dictate at even a moderate pace, you will land comfortably in the upper percentiles. Do not mistake "Top 10%" for exceptional dictation skill; it means you are faster than the median typist, which is a low bar. The number is motivating, not diagnostic.

The corrections counter is more useful than it looks. A rising corrections count per session can mean your microphone is degrading, your environment is noisier, or you have started dictating in a style that leans heavily on course correction (backtracking mid-sentence). If the count spikes without a change in your habits, check The Input Chain (Ch18) before assuming Flow got worse.

The streak heatmap is a consistency metric. It does not measure quality. A one-word dictation counts the same as a 2,000-word session for streak purposes. If streaks motivate you, use them. If they produce guilt on rest days, ignore them.

## The "New" Badge

When Insights first becomes available on your account, a "New" badge appears next to Insights in the sidebar.<sup>[1]</sup> It wiggles shortly after the app opens and again every few minutes until you visit the page. It also wiggles on hover (unless the sidebar is collapsed). After your first visit, the badge fades permanently.<sup>[1]</sup> This is a one-time nudge, not a recurring notification.

## What Gets Collected to Build These Numbers

Flow tracks every dictation event on the desktop: when it happened, how long it took, which app received the text, how many words were produced, and what corrections were applied. This data feeds the Usage tab locally and, for Team and Enterprise users, contributes to the Leaderboard.

The Voice Profile goes further. Because it requires "Store locally" as your data storage setting, it depends on your transcription history remaining on the device. If you enable a deletion policy, the profile disappears. This is not a bug; it is a direct consequence of the privacy architecture described in The Cloud Boundary (Ch21). You cannot simultaneously tell Flow to forget your transcripts and ask it to remember your habits.

For Team and Enterprise users, the Leaderboard aggregates individual metrics into a team ranking. Enterprise admins can export usage data via the admin portal (see The Org Layer, Ch23). The Word Budget (Ch19) tracks words for billing; the Usage tab tracks words for insight. Same unit of measurement, different purpose.

## Key Points

- The Usage tab lives on Mac and Windows only; mobile users have no access to Insights as of Q2 2026.
- WPM percentile compares you to keyboard typists, not to other Flow users, making the ranking generous by default.
- The Leaderboard requires a Team or Enterprise plan, refreshes hourly, and can be hidden entirely by an admin.
- The Voice Profile requires local data storage; enabling a deletion policy hides the tab and its share cards.
- Corrections by Flow is the most underused tile and the best early-warning signal for microphone or environment problems.
- Your dictation data feeds both billing metrics and insight dashboards; the same words count in both systems.
