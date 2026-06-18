# Deploying Flow for Teams

*In this chapter: organizations add a shared layer on top of individual Flow accounts, covering admin controls, shared vocabulary, identity management, usage insights, and deployment tooling. If you use Flow solo, skip this chapter. If you are evaluating Flow for a team or already administering one, this is the reference.*

Every feature in this book so far has assumed one human, one account, one device. You dictate, Flow rewrites, text lands where your cursor is. That model works until you need thirty humans using the same terminology, a compliance officer who needs zero data retention across the org, or an IT director who wants SSO before anyone installs anything. The moment the unit of adoption shifts from person to organization, Flow needs a layer it did not need before.

That layer is The Org Layer.

## What the Org Layer Contains

The Org Layer is not a separate product. It is the set of controls, shared resources, and identity plumbing that Enterprise and Team plans expose on top of the same dictation engine every solo user runs. The Org Layer gives you three things the individual product does not: shared vocabulary that applies to every member's transcriptions automatically, admin-enforced policies that override individual settings, and identity integration so your directory is the source of truth for who has access.<sup>[1]</sup>

The admin portal at admin.wisprflow.ai is where all of this lives. It is web-only. Mobile apps have no admin UI. The desktop app exposes inviting users and approving join requests, plus a link to the portal, but every policy configuration happens in the browser.<sup>[2]</sup>

## Roles and Seats

Flow defines three roles on Team plans: Super admin, Admin, and Member. Enterprise adds a fourth: IT Admin.<sup>[1]</sup>

Super admins and admins have full access to the admin portal, including billing, user management, and settings. Only admins and super admins can directly invite new users. Members see org details and billing data in the portal but cannot make admin changes.<sup>[2]</sup>

IT Admin is the odd one. It is a management-only seat type. IT Admins can manage seats, SSO, billing, organization settings, and compliance features, but they cannot use Wispr Flow for dictation. If an IT Admin opens the desktop app, they see a non-dismissable modal with two options: Sign out, or Open Admin Portal. The modal clears automatically if their seat is upgraded without signing out. IT Admin seats are always free and never count toward billed seat totals.<sup>[1,2]</sup>

This is the role designed for the humans who set up the infrastructure but never dictate a word.

## Trials and the Grace Period

First-time team creators receive a 14-day trial. Users who have already used that trial receive only a 24-hour trial when creating a new team.<sup>[3]</sup> When a trial ends, there is a 3-day grace period. An admin must add billing information during this window. If they do not, the team is disbanded: subscription cancelled, all members removed.<sup>[1]</sup>

Joining a team can only extend an existing trial, never shorten it. If you already have a longer trial in progress (a 30-day referral trial, for instance), it is preserved. The exception: if the enterprise has team trials disabled, you are moved to a paid seat immediately, even with a longer pre-existing personal trial.<sup>[3]</sup>

Enterprise billing is per seat. The seat count for limit enforcement includes active members plus pending invitations. There is no minimum seat requirement.<sup>[3]</sup>

## The Admin Portal

The portal at admin.wisprflow.ai is the single surface for org-level configuration. From here, admins manage users, set data controls, configure SSO, enable SCIM, set up IP restrictions, view billing, and export usage data.<sup>[2]</sup>

Data Controls (Enterprise only) include:<sup>[2]</sup>

- **Context Awareness:** Set to Available (users toggle it themselves) or Disable for all users (locks the toggle org-wide).
- **Zero Data Retention:** Enforces ZDR across your organization.
- **Local data storage policy:** Store normally, auto-delete after 24 hours, or never store. The stricter settings force the auto-delete toggle on and lock it for every member.
- **SOC 2 report access** and **HIPAA BAA signing** directly from the portal.

The deeper treatment of these privacy controls lives in The Cloud Boundary (Ch21). Here, what matters is that an admin can enforce them from one place without touching individual devices.

## Identity: SSO and SCIM

SSO is configured in the admin portal and works on Mac, Windows, iOS, and Android. Wispr Flow supports SAML 2.0, with supported providers including Okta, Microsoft Entra ID, Google Workspace, and OneLogin.<sup>[4]</sup> The setup wizard handles most of the configuration; most teams finish in under ten minutes.

Enforce SSO is the toggle that matters. When enabled, it blocks all non-SSO sign-in methods (email/password, Google, Apple, Microsoft) for users on the enforced domain.<sup>[4]</sup> It requires an active Enterprise subscription. If the subscription lapses, enforcement lifts automatically and resumes when the subscription returns to good standing.<sup>[4]</sup>

Where users find the SSO button varies by platform. On Mac and Windows, there is a single "Sign in via browser" button. On Android, all sign-in options including SSO are visible by default. On iOS, SSO is hidden: users must tap "More options" first, then choose "Continue with SSO."<sup>[5]</sup>

SCIM provisioning is Enterprise only. When active, all user management goes through your identity provider's directory sync. The "Add new user" button and join request Approve/Deny buttons are hidden in Flow. Manual user management is fully disabled.<sup>[6]</sup>

All SCIM-provisioned users are assigned the Member role. Role mapping from the identity provider is not supported. IT Admin is assigned only through the Admin Portal.<sup>[6]</sup>

One operational detail worth noting: only fully deleting the directory sync re-enables manual user management. Deactivating or pausing the connection has no effect.<sup>[6]</sup>

If your enterprise has a seat cap and SCIM provisioning requests would exceed it, the request is skipped. The user is not added and no invitation is sent. If SCIM hits a transient error instead, Flow falls back to sending an email invitation.<sup>[3,6]</sup>

A user can only belong to one Wispr Flow enterprise at a time.<sup>[6]</sup>

## Domain Capture

Domain capture lets admins control what happens when someone signs up with an email at their company's domain. Verification is self-serve via a DNS TXT record: the host follows the pattern `_wispr-verify.<your-domain>`, the value starts with `wispr-verify=`.<sup>[7]</sup>

Once verified, the admin sets a policy: Off (no restriction) or "Require team membership" (users must join the enterprise to use Flow).<sup>[7]</sup> Verification is permanent. No auto-recheck is required.<sup>[7]</sup>

Multiple domains are supported. Each shows as its own row with its own verification status, TXT record, and policy.<sup>[7]</sup>

One important constraint: domain verification uses public DNS resolution. Split-horizon or internal-only DNS will not work.<sup>[7]</sup>

## IP Allowlist

Enterprise admins can restrict access to specific networks. When enabled, only users connecting from an approved IP range can authenticate. The allowlist supports IPv4 and IPv6 CIDR ranges, up to a maximum of 64 entries. Wildcard CIDRs are rejected.<sup>[4]</sup>

The allowlist applies across desktop, web, and iOS. Android does not yet enforce it (as of Q2 2026).<sup>[1,4]</sup>

Users blocked by the allowlist are signed out automatically and shown a "Your network isn't allowed" screen. Dictation is paused while they are blocked. From that screen, they can retry (after switching to an approved network) or sign out.<sup>[2]</sup>

A self-lockout safeguard exists: the portal shows your current IP and blocks you from saving a list that does not include it.<sup>[2]</sup>

## Team Dictionary and Snippets

Enterprise teams have a shared dictionary that applies to all members. In the Dictionary section of the app (Mac, Windows, iOS, Android), filter tabs (All, Personal, Shared with team) let you browse and manage words. Team dictionary words are used during transcription for all members automatically.<sup>[3]</sup>

Any member of an enterprise team can bulk-import dictionary words or snippets directly into the shared team library via the import dialog.<sup>[3]</sup>

On Android, non-enterprise users do not see the team filter. The Android dictionary currently supports plain words only; replacements and snippets are not yet supported on Android.<sup>[3]</sup>

## Onboarding and Team Consolidation

Team-aware onboarding is available on Mac and Windows desktop only. Flow detects whether your email domain has an existing team, an active enterprise account, or no team at all, and routes you to the matching path automatically.<sup>[8]</sup>

If your email domain already has a Wispr Flow team, you see a Team Consolidation screen during onboarding. It pre-selects existing teammates from your domain and lets you add additional email addresses before joining or creating a team. A "Skip for now" option is available.<sup>[8]</sup>

In multi-team enterprises, new members who have not been pre-assigned see a Team Picker screen. It is mandatory: no skip, no back button. If the enterprise uses cost-center billing, teams are grouped by cost center with a billing contact shown for each group.<sup>[8]</sup>

Corporate email is required. Generic, public-TLD, and university email domains (gmail.com, yahoo.com, .gov, .mil, .edu, .int and their international variants) cannot be used as team domains.<sup>[1,3]</sup>

## MDM Deployment

Wispr Flow supports MDM deployment on macOS (via Configuration Profiles, Jamf, or Kandji) and Windows (via Group Policy or Intune). The MDM-managed policy is currently update frequency: auto, weekly, bi-weekly, or monthly. Security policies (SSO enforcement, transcript retention, Context Awareness, model training opt-in) are configured by admins in the admin portal, not through MDM.<sup>[3]</sup>

## Team Insights

The Insights page in the admin portal gives admins a view of how their team uses Flow. Enterprise gets the full dashboard. Pro admins see a blurred preview with only the Words Dictated card accessible.<sup>[9]</sup>

The Impact tab surfaces estimated business value:<sup>[9]</sup>

- **Time Saved:** Calculated against a 40 WPM typed baseline.
- **Money Saved:** A salary-rate slider ($20/hr to $300/hr, default $100/hr) computes value saved per month using a trailing 29-day window. The figure never displays below $0.
- **AI Prompt Quality:** A multiplier showing how much longer dictated prompts are compared to an 8-word typed baseline. The card only appears when the team average exceeds 8 words.

The Team Members table shows each user's lifetime average WPM, total words, status, role, and last activity. Users who have never dictated show a dash, not zero, and are pinned to the bottom when sorting by WPM.<sup>[10]</sup>

Enterprise admins can hide the team leaderboard from non-admin members via Organization settings (see The Voice Profile, Ch22).<sup>[1]</sup>

## Admin Usage and CSV Export

Enterprise admins can export team usage data as CSV from the Overview tab. Each export includes a Date column and breaks activity down by day, sorted chronologically. One row per day per dimension combination. Dimension columns available: User, User email, Department, App type, App name.<sup>[10]</sup>

Exports are capped at 100,000 rows. If your filters would produce more, the export fails and asks you to narrow your filters.<sup>[10]</sup>

## Cost Centers

Cost Centers let an Enterprise split one or more teams into their own billing units with separate subscriptions and invoices. Each cost center inherits the parent enterprise's negotiated pricing automatically; there is no plan tier selection.<sup>[11]</sup>

Each break-away cost center has its own customer record, payment method, and invoices, fully separate from the parent enterprise.<sup>[11]</sup>

Cost Centers are Enterprise only and must be enabled by your account representative. An admin who is already the billing owner for another cost center in the same enterprise cannot create an additional one; a different admin must complete the flow.<sup>[11]</sup>

The Cost Centers tab on the Team page lists every cost center with columns for name, status, team count, seat count, renewal date, and creation date. It is visible to admins only.<sup>[11]</sup>

## Guided Tours

After a team plan is activated, Flow runs a short guided tour (Mac and Windows only) spotlighting three sidebar items: Insights, Dictionary, and Snippets. It is a 3-step walkthrough. The tour launches when the user clicks "Get started" on the upgrade celebration modal; dismissing the modal does not launch the tour.<sup>[12]</sup>

The tour appears once. It cannot be replayed from within the app.<sup>[12]</sup>

## Key Points

- The Org Layer adds shared vocabulary, admin-enforced policies, and identity integration on top of the same dictation engine solo users run.
- SSO enforcement blocks all non-SSO sign-in methods and lifts automatically if the Enterprise subscription lapses.
- SCIM provisioning disables all manual user management in Flow; only deleting the directory sync fully re-enables it.
- IT Admin is a free, management-only seat that cannot dictate, designed for infrastructure humans who never speak into a mic.
- Domain capture and IP allowlists give admins control over who can sign up and from which networks they can connect.
- Team dictionary words apply to every member's transcriptions automatically.
- Cost Centers let departments within an enterprise manage their own billing independently at the same negotiated price.
