# Chapter 3: Windows

*In this chapter, you meet the Windows build of Wispr Flow and the resource cost it carries. Setup is simpler than on macOS because Windows asks for fewer permissions, but the Electron runtime underneath means higher RAM, higher CPU, and occasional friction with the apps you are dictating into. This chapter covers installation, permissions, hotkeys, data locations, and what to expect from the platform that trades polish for reach.*

Every desktop application is a bet on a runtime. Native apps bet on tight integration with one operating system. Cross-platform apps bet on reach. Wispr Flow on Windows is an Electron app, and Electron apps pay a tax.

Call it The Electron Tax.

You get the same features as the Mac build. You get dictation, hands-free mode, the Cleanup Dial (see Ch7), Context Awareness (see Ch9), Dictionary, Snippets, Transforms. Feature parity, on paper, is real.<sup>[1]</sup> But the Windows client wraps all of it inside Chromium, and Chromium is not free. Independent reviews in early-to-mid 2026 consistently report the Windows app consuming roughly 800 MB of RAM and around 8 percent CPU while idle (inferred from multiple third-party benchmarks; Wispr's own documentation does not publish these figures).<sup>[2]</sup> On a machine with 8 GB of RAM, that idle footprint is nontrivial.

The tax is not just memory. Several reviews and user reports describe the Electron app freezing target applications such as VS Code and Notepad++ during active dictation (inferred from third-party reports, not Wispr documentation).<sup>[2]</sup> The pattern is consistent with the desktop stability work visible across recent versions of the help center documentation, which addresses repeated crash, freeze, and paste-failure fixes on Windows.<sup>[2]</sup>

If you are on a well-provisioned machine (16 GB or more, a recent x64 processor), the tax is manageable. If you are on a thin-client laptop or running heavy IDE workloads alongside Flow, you will feel it.

That is the honest trade-off. The rest of this chapter is the practical setup.

## System Requirements

Wispr Flow on Windows requires Windows 10 (64-bit) or Windows 11.<sup>[3]</sup> The hardware recommendations from the help center are straightforward: an x64 processor, 8 GB of RAM or more, approximately 200 MB of available storage, and a working microphone (built-in or external).<sup>[3]</sup>

One hard boundary: ARM-based Windows devices, including Snapdragon-powered systems, are "not officially supported and may not work correctly."<sup>[3]</sup> If you are on a Surface Pro with a Snapdragon chip or a Qualcomm-based laptop, Flow is not a reliable option as of Q2 2026.

An audio output device is optional. Flow works without a default audio output configured.<sup>[3]</sup>

## Installation

There is no dedicated Windows install article in the help center. The Setup Guide covers all four platforms, and the Windows section is compact.<sup>[1]</sup>

Download the installer from wisprflow.ai. Open it, follow the on-screen steps. Launch Wispr Flow from the Start menu. The app icon appears in your system tray when it is running.<sup>[1]</sup>

Two installer variants exist for enterprise scenarios: a per-user `Wispr Flow Setup.exe` for self-install, and a machine-wide `Wispr Flow.msi` for deployment via Intune, SCCM, or similar MDM tools.<sup>[3]</sup>

Sign in through the browser. Flow opens your default browser to the login page, where you can use Google, Apple, Microsoft, SSO, or email/password. The session transfers back automatically. If you wait too long, the sign-in attempt times out and you start again.<sup>[1]</sup>

One tip worth noting: turn on "Start at login" so Flow launches automatically when Windows starts. The setting stays active after app updates.<sup>[1]</sup>

## Permissions (or the Lack of Them)

This is where the Windows experience diverges sharply from macOS. On the Mac, you navigate a Permission Gate (see Ch4) involving Accessibility, Microphone, and optionally Screen Capture. On Windows, the permission model is simpler to the point of near-invisibility.

Windows does not require app-level Microphone or Accessibility permissions. Only system-level microphone access matters.<sup>[4,5]</sup> If Windows prompts you for microphone access during setup, allow it. If you skipped the prompt, open Settings, then Privacy & Security, then Microphone, and turn on access for Wispr Flow. If microphone access is already granted system-wide, Flow skips this step automatically.<sup>[1]</sup>

In recent versions, Flow checks microphone availability at runtime, so you typically do not need to manually re-verify permissions after an update.<sup>[4]</sup> The in-app button is labeled "Open Settings" (rather than "Allow" as on Mac) and takes you to Windows Sound Settings. If you see a "microphone privacy disabled" notification, Windows is genuinely blocking microphone access.<sup>[4]</sup>

The simplicity is real, but it comes with a subtlety. Because Windows has no Accessibility permission layer, Flow relies on standard keyboard and clipboard injection rather than OS-level accessibility APIs (inferred from documentation structure; not explicitly stated). This reduces setup friction but makes interference with other keyboard automation tools more likely if you run global hotkeys or text expanders alongside Flow.

## Hotkeys

The default push-to-talk shortcut on Windows is Ctrl+Win.<sup>[6]</sup> Hold it to dictate, release to submit. Double-tap to enter hands-free mode. The hands-free shortcut defaults to Ctrl+Win+Space, and Command Mode to Ctrl+Win+Alt.<sup>[6]</sup>

Other default shortcuts on Windows:<sup>[6]</sup>

- Paste last transcript: Shift+Alt+Z
- Copy last transcript: Shift+Alt+X
- Polish (Transform): Win+Alt+1
- Prompt Engineer (Transform): Win+Alt+2
- View Diff: Win+Alt+O
- Cancel: Escape
- Open Scratchpad: no default (opt-in only)

Each binding supports up to four shortcuts. Cancel allows only one.<sup>[6]</sup>

A valid shortcut requires three keys or fewer, with at least one modifier key (Ctrl, Alt, Shift, Win) or a valid mouse button (middle click, Mouse 4 through Mouse 10).<sup>[6]</sup> Left and right click are intentionally excluded. Caps Lock cannot be used. And standalone Ctrl or Right Ctrl cannot serve as a single-key hotkey because it would intercept every Ctrl-based shortcut in Windows, breaking copy, paste, and undo.<sup>[6]</sup>

The system reserves a long list of combinations. Ctrl+C, Ctrl+V, Ctrl+X, Alt+Tab, Alt+F4, Win+E, Win+L, and many more are blocked because Windows or common apps use them.<sup>[6]</sup> If your shortcut is rejected and it is not in the reserved list, it is likely already assigned to another Flow action. Check Settings, then General, then Shortcuts to see all current assignments.<sup>[6]</sup>

Here is the conflict scenario worth understanding: if you set your hotkey to a combination that collides with a system shortcut, the pasted output may come out as the conflicted key's character. The documentation gives the example of a hotkey conflict with Ctrl+V causing the output to be the letter "v" instead of your dictated text.<sup>[7]</sup> The fix is to remap Flow's activation shortcut or adjust the conflicting tool.

Mouse button shortcuts are available on desktop. When bound, the mouse button is intercepted system-wide while Flow is running. Apple Magic Mouse and trackpads are not compatible, but that is a Mac concern, not a Windows one.<sup>[6]</sup>

Custom keybind shortcuts are stored per-device in your local preferences. They do not sync across machines.<sup>[6]</sup>

## After Updates: Re-verifying

When Flow stops listening, typing, or responding to shortcuts after a system or app update, the issue is almost always permissions or microphone state.<sup>[4]</sup>

On Windows, the re-verification process is minimal:

1. Check that your system microphone is working in Windows Sound Settings and that no other app is using it exclusively.
2. Close and reopen Wispr Flow.
3. Dictate a short phrase. If text appears in Recent Activity, you are done.<sup>[4]</sup>

A few Windows-specific issues have surfaced and been fixed in recent updates. Some users saw an empty microphone list in Settings. Others got a false "microphone privacy disabled" error even though their microphone was enabled, particularly on machines managed by IT policies (MDM/GPO) or running Dell Optimizer or similar third-party privacy tools.<sup>[4]</sup> Both were resolved in recent versions; updating and restarting Flow fixes them.

Another fixed issue: dictation could fail repeatedly and require a full app restart to recover. The audio recorder could become unavailable after restarting onboarding or due to audio driver issues on Windows, causing a false "Listening" state on each push-to-talk attempt. Recent versions recover from this automatically, though you may notice a small delay on the first dictation press after recovery.<sup>[4]</sup>

## Data Locations

Flow stores its data in two Windows directories: `%LOCALAPPDATA%\WisprFlow` for app files, and `%APPDATA%\Wispr Flow` for data, database, session, and logs.<sup>[8]</sup> A legacy path, `%APPDATA%\Flow`, may also exist from older installations.<sup>[8]</sup>

If you ever need a completely clean reset, those are the directories to clear. But note: the "Reset & Restart" option in the app (available on desktop only) clears local data and restarts the app. Transcript history is stored locally only and is permanently lost after a reset. Dictionary, Snippets, and Notes re-sync from your account on restart. Shortcuts, stats, and settings are preserved (see Ch24 for details).<sup>[9]</sup>

One warning that applies to all desktop platforms: do not store Flow's local data in a cloud-synced folder such as OneDrive. This can cause database corruption.<sup>[8]</sup>

## What Windows Does Not Require

It is worth explicitly listing what Windows does *not* ask for, because if you are coming from the Mac chapters or have read about macOS setup elsewhere, the contrast is stark:

- No Accessibility permission. Flow inserts text without it on Windows.
- No Screen Capture permission. Context Awareness on Windows uses a different mechanism.
- No per-app microphone permission. Windows manages this at the OS level.

This makes the Windows setup faster and less error-prone than macOS. It also means there is no Permission Gate to troubleshoot when things break. If dictation stops working on Windows, the fault is almost always microphone access, a hotkey conflict, or the Electron runtime itself.

## The Honest Picture

The Electron Tax is real but not disqualifying. The Windows build gives you full feature parity with the Mac build inside a runtime that costs more resources and occasionally interferes with the apps it is serving. If you have the hardware headroom, that trade-off is acceptable. If you are on a constrained machine, test before you commit.

For enterprise deployments, the MSI installer and MDM support make Windows distribution straightforward. Auto-updates will not apply during active dictation, and enterprise admins can configure the update cadence to weekly, bi-weekly, or monthly.<sup>[4]</sup>

The Windows build works. It just makes you pay for the privilege.

## Key Points

- The Windows build is an Electron app that trades higher resource usage for full feature parity with the native Mac client.
- Windows requires only system-level microphone access, with no Accessibility or Screen Capture permissions to configure.
- ARM-based Windows devices (Snapdragon) are not officially supported as of Q2 2026; only x64 processors are valid.
- Hotkey conflicts can cause pasted output to appear as a stray character; remapping the activation shortcut is the fix.
- Store Flow data in its default local directories, never in a cloud-synced folder like OneDrive, to avoid database corruption.
