# Chapter 17: Remote and Restricted Environments

*In this chapter: Flow inserts text by pasting from the local clipboard, which means anything that blocks or redirects the paste breaks the entire pipeline. Remote desktops, banking apps on Android, and non-standard keyboard layouts each create their own version of this wall. The chapter maps where the insertion boundary sits and what to do on each side of it.*

Every tool has a reach. Flow's reach ends at the clipboard. It transcribes your speech, copies the result, and fires a paste keystroke into whatever has focus. When that keystroke lands inside a local app, everything works. When it lands inside a remote desktop session, a protected banking app, or a text field that expects a keyboard layout Flow did not start with, the text either arrives late, arrives garbled, or does not arrive at all.

That boundary is worth naming. Call it The Insertion Boundary: the line past which Flow can produce text but cannot place it. The boundary is not a bug. It is a consequence of how clipboard-based insertion works across process and network lines. Once you see where the boundary sits, the workarounds stop feeling random and start feeling like what they are: routing decisions.

## Remote Desktops: Flow Stays Local

The first rule of remote desktops is one most humans learn the hard way: Flow runs on your local machine, not inside the virtual session.<sup>[1]</sup> Install it on the laptop in front of you, not in the Citrix image or the RDP window. If you install it inside the VDI, it will lack the local microphone access and system permissions it needs to function.

The second rule follows from the first: your dictated text reaches the remote session only if clipboard sharing is turned on between local and remote.<sup>[1]</sup> Flow transcribes, copies to your local clipboard, and fires a paste keystroke. The remote desktop client intercepts that keystroke and, if clipboard redirection is enabled, transfers the clipboard contents across the connection. If redirection is off, the text sits on your local clipboard and the remote session sees nothing.

Context-aware formatting (the capitalization and spacing that The App-Aware Rewrite, covered in Chapter 9, provides) does not work inside remote sessions.<sup>[1]</sup> Text pastes with default formatting. This is not a setting you can toggle; it appears to be a limitation of how Flow reads surrounding text context, which likely does not extend into the remote environment.

### Platform-by-Platform

**RDP (Microsoft Remote Desktop).** Clipboard sharing usually works well.<sup>[1]</sup> Enable it in the connection settings before connecting. Text transfers between local and remote clipboards, but formatting does not.

**Citrix Workspace.** The clipboard must be enabled by your IT administrator.<sup>[1]</sup> Some Citrix policies block clipboard access for security. If paste does not work, check with IT about clipboard redirection settings. Citrix connections may also introduce delays; wait one to two seconds after dictating before pasting.<sup>[1]</sup>

**VMware Horizon.** Requires clipboard redirection enabled in the Horizon client settings.<sup>[1]</sup> Once enabled, it works similarly to RDP.

**Amazon WorkSpaces.** Clipboard sharing is typically enabled by default.<sup>[1]</sup>

**Windows 365 / Azure Virtual Desktop.** Clipboard redirection is usually enabled and works like standard RDP.<sup>[1]</sup>

### When Auto-Paste Fails

If Flow's automatic paste does not reach the remote session, it copies your transcribed text to the clipboard and shows a notification.<sup>[1]</sup> You have two recovery paths: paste manually with the standard shortcut (Cmd+V on Mac, Ctrl+V on Windows), or use the Paste Last Transcript shortcut (Ctrl+Cmd+V on Mac, Alt+Shift+Z on Windows by default).<sup>[1]</sup>

On Windows, there is an additional wrinkle. If your remote desktop client runs with administrator privileges, Flow cannot paste into it. The app will show a message reading "Update admin settings to paste!" or "Run Flow as Administrator to insert text everywhere."<sup>[1]</sup> The fix is to run Flow as administrator, which raises it to the same privilege level as the remote desktop client.

If none of that works and the text is truly stuck, Flow's fallback is The Scratchpad (Chapter 16): it opens a local window with your transcribed text so nothing is lost.

## Banking Apps: The Privacy Wall

On Android, Flow enforces a second kind of insertion boundary that you cannot negotiate with. When you open a supported banking or financial app, Flow hides the Flow Bubble and disables all activation methods until you switch to a different app.<sup>[2]</sup> This is not configurable. There is no toggle to disable it.<sup>[2]</sup> It is a privacy safeguard, and it is always on.

The behavior is thorough. While a banking app is in the foreground, the Bubble stays hidden, Flow is fully disabled, and it does not capture any text or screen content.<sup>[2]</sup> Context awareness is suppressed: Flow does not read surrounding text or selected text while inside a banking app.<sup>[2]</sup> No activation method brings the Bubble back. The operation is silent; no persistent notification or indicator appears. If you try to trigger dictation by typing in a banking app, a one-time toast confirms that the Bubble is disabled there.<sup>[2]</sup>

If a dictation is already in progress when a banking app comes to the foreground, Flow stops the dictation and copies the transcribed text to your clipboard for manual pasting.<sup>[2]</sup> Finish your dictation before switching to the banking app.

When you leave the banking app and tap into a text field in another app, the Bubble reappears and voice input resumes automatically.<sup>[2]</sup>

### Regional Coverage

The detection covers a broad list of financial apps across regions<sup>[2]</sup>:

- **United States:** Major retail banks, credit unions, and fintech apps including Chime, Venmo, SoFi, Cash App, PayPal, and Google Wallet.
- **Canada:** RBC, TD Canada, BMO, Scotiabank, and CIBC.
- **Australia:** Commonwealth Bank, ANZ, Westpac, and NAB.
- **Europe:** Revolut Business, Qonto, BBVA Spain, KBC Belgium, BoursoBank France, Airwallex, Tide EU, and Intesa Sanpaolo.
- **India:** Banks and UPI-based financial apps including Paytm, PhonePe, Google Pay, and Airtel Thanks.
- **Asia:** DBS PayLah, Maybank SG, BRImo Indonesia, and Hang Seng HK.
- **Latin America:** Nubank, Mercado Pago, BBVA Mexico, and others.
- **United Kingdom:** Tide and Santander Business.
- **South Africa:** RMB Private Bank.

Apps not on the list will not trigger the hide behavior. Coverage expands with each release.<sup>[2]</sup>

Banking app detection is Android only.<sup>[2]</sup> On iOS, certain keyboard types (numeric keypads, email-address fields) automatically switch away from the Flow Keyboard, but that is input-type detection, not banking-app-specific detection.

Flow also hides the Bubble for password, PIN, and numeric-only input fields in any app, not just banking apps.<sup>[2]</sup> Browser address bars and system notification reply boxes are exceptions; Flow still appears in those surfaces.

## Non-QWERTY Keyboard Layouts: The Layout Mismatch

The third face of The Insertion Boundary is the quietest and the most confusing when it hits. Flow reads your keyboard layout at startup and uses it for the paste keystroke while the app is running.<sup>[3]</sup> If the layout active when Flow starts does not match the layout active when you dictate, the paste may fail, insert wrong characters, or trigger unexpected shortcuts instead of inserting text.

This affects Mac, Windows, and Android.<sup>[3]</sup>

### Non-Latin Layouts (Cyrillic, Arabic, CJK)

If your system is set to a non-Latin layout, switch to QWERTY before launching Flow.<sup>[3]</sup> Keep QWERTY active while dictating and pasting. You can switch back to your non-Latin layout for typing, then return to QWERTY before your next dictation.<sup>[3]</sup>

The core problem: Flow fires a paste keystroke based on the physical key mapping. On a non-Latin layout, switching to QWERTY before dictating ensures the paste keystroke maps correctly. [test-it]

### Alternative Latin Layouts (Dvorak, Colemak)

Set your preferred layout before launching Flow, and keep it active for the entire session.<sup>[3]</sup> If you need to switch layouts, restart Flow afterward so it picks up the new layout. Some apps handle modifier shortcuts by physical key position rather than character mapping; if paste still fails on Dvorak or Colemak, switching to QWERTY is the reliable fallback.<sup>[3]</sup>

The rule in both cases: do not switch keyboard layouts during an active Flow session. If you do, restart Flow.<sup>[3]</sup>

### The Scratchpad Fallback

If Flow cannot insert text into the focused field for any layout-related reason, it opens The Scratchpad (Chapter 16) with your transcribed text and copies it to the clipboard.<sup>[3]</sup> You can edit the text in the Scratchpad and paste manually. Nothing is lost; the insertion just takes an extra step.

## The Pattern

Remote desktops, banking apps, and keyboard layouts look like three unrelated problems. They are not. Each one is a case where something between Flow's clipboard and the target text field blocks or distorts the paste. In a remote session, the blocker is the network boundary and a clipboard redirection setting. In a banking app, the blocker is a deliberate privacy wall. In a layout mismatch, the blocker is a keystroke that maps to the wrong character.

The fix in every case follows the same logic: make sure the path from clipboard to cursor is clear, or accept the Scratchpad as your staging area. The Insertion Boundary is not going away. It is structural. Learn where it sits in your workflow, and you stop losing text to it.

## Key Points

- Flow inserts text by pasting from the local clipboard, so anything that blocks or redirects the paste creates an insertion boundary.
- Remote desktop sessions require clipboard sharing enabled by the client or IT policy before Flow can deliver text.
- Context-aware formatting does not extend into remote sessions; text arrives with default formatting only.
- Banking app detection on Android is automatic, cannot be disabled, and suppresses all Flow activation while a financial app is open.
- Non-Latin keyboard layouts require switching to QWERTY before dictating; alternative Latin layouts require a Flow restart after any layout change.
- When paste fails for any reason, Flow copies text to the clipboard and opens the Scratchpad so nothing is lost.
