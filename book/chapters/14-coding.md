# Coding with Flow

*In this chapter: Flow has a developer mode that reads your IDE to recognize symbols, tag files by voice, and handle the peculiarities of terminals and AI coding CLIs. The feature is called Vibe Coding, and its behavior varies sharply across editors, platforms, and input surfaces.*

Every developer tool eventually ships a voice feature. Most of them bolt it on. Flow built one that reads your code.

The feature is called Vibe Coding, and the name is earned. When you enable it, Flow stops treating your dictation as prose. It reads the open editor tab, extracts variable names, function names, and class names, and uses them as context when transcribing what you say. You say "clear pasteboard" and Flow types `clearPasteboard` because it saw the symbol in your file. That is not autocomplete. That is the Rewrite Pass (Ch1) applied to code context, and it changes what dictation can do inside an IDE.<sup>[1]</sup>

Variable Recognition is off by default. You turn it on in Settings, under Vibe Coding. The moment you do, Flow activates Screen Reader Mode in your IDE so it can read code content through accessibility APIs.<sup>[1]</sup> If Screen Reader Mode gets turned off while Variable Recognition is enabled, Flow re-enables it after your next dictation.<sup>[1]</sup> This is one of those details that sounds minor until you wonder why your IDE keeps toggling a setting you did not touch.

## Where It Works and Where It Does Not

The platform support for Vibe Coding is not uniform. It is a two-tier system, and the tiers matter.

**Cursor and Windsurf** get full Variable Recognition: backtick formatting around recognized symbols, file tagging in AI chat panels, and code context from open editors. This is the complete experience.<sup>[1,2]</sup>

**VS Code** gets screen reader mode integration only. Flow can read code context from VS Code to improve transcription accuracy, but it will not wrap symbols in backticks and it will not tag files. You get better recognition without the formatting.<sup>[1,3]</sup>

**VS Code Insiders** gets nothing. It is not supported.<sup>[1,3]</sup>

Variable Recognition and File Tagging are available on Mac and Windows only. Mobile is out (as of Q2 2026).<sup>[1,2]</sup>

The supported programming languages are JavaScript, TypeScript, Python, Java, Swift, C++, C, Rust, and Go.<sup>[1]</sup> Code in other languages does not get symbol extraction. Your Ruby or Kotlin files will not participate. That list may grow, but for now, it is the list.

## File Tagging: Talking to Your AI Chat

File Tagging is the second half of Vibe Coding, and it solves a specific annoyance. In Cursor or Windsurf, when you want to attach a file to an AI chat for context, you normally press @, type the filename, and pick from a dropdown. File Tagging lets you skip all of that. Say the filename, and Flow attaches it.<sup>[2]</sup>

File Tagging in Chat is on by default, independent of Variable Recognition.<sup>[1,2]</sup> You can toggle each setting separately under Settings, Vibe Coding.

There are two ways to tag a file by voice:

**Say the full filename with extension.** "Can you fix the bug in index dot ts please?" Flow tags `index.ts` and attaches it to the AI chat automatically.<sup>[2]</sup>

**Use a trigger word without the extension.** Say "tag," "at," "tagged," or "@" followed by the base filename. "Can you explain this code to me, tag my python script." Flow matches the file from your open tabs and attaches it.<sup>[2,3]</sup>

You can tag multiple files in a single dictation. "Look at cron dot py and vad dot py" tags both files correctly.<sup>[2,3]</sup>

Flow matches spoken filenames to their camelCase or separator-based forms. Say "cursor formatting" and Flow matches `cursorFormatting.ts`. Say "my script name" and it matches `my_script_name.py`. When multiple files could match, the longest filename wins.<sup>[2]</sup>

A few edge cases to know:

Files with no dot in their name (Makefile, Dockerfile) cannot be tagged.<sup>[2]</sup> Dot-prefixed files like `.env` require saying "dot" before the name, or speaking the literal filename.<sup>[1,2]</sup> And here is a collision that will bite you if you are not ready for it: if a Custom Dictionary substitution fires during your dictation, IDE file tagging is skipped for that entire dictation. Variable name vocabulary and backtick formatting are unaffected, but the file tag will not happen.<sup>[1,2]</sup> This is the dictionary/tagging interaction noted in The Personal Lexicon (Ch10); the rule is that one substitution disables all file tagging for that transcript.

File Tagging does not work in terminal panes within the IDE. It works in editor panels and chat panels only.<sup>[2,3]</sup>

## Terminals: The Paste Problem

Dictating into a terminal is a different game from dictating into an editor panel. Flow inserts text via your system's paste shortcut, and terminals are not always cooperative about accepting it.

The good news: a long list of terminals support direct paste with no setup. On Mac, Terminal.app, iTerm2, Warp, Ghostty, Hyper, Alacritty, and Kitty all work. On Windows, Command Prompt, PowerShell, Windows Terminal, and WezTerm all work. The integrated terminals in Cursor, VS Code, and Windsurf also support direct paste, though on Windows, Flow uses Shift+Insert instead of Ctrl+V because those IDE terminals do not accept Ctrl+V reliably.<sup>[3,4]</sup>

The bad news: WSL terminals, SSH sessions, tmux, and screen do not support direct paste. Termius on Windows does not either.<sup>[4]</sup> In all these cases, the recovery is the "Paste last transcript" shortcut: Shift+Alt+Z on Windows, Cmd+Ctrl+V on Mac.<sup>[4]</sup> There is also a "Copy last transcript" shortcut (Shift+Alt+X on Windows) that puts the text on your clipboard without pasting, for when you need to paste somewhere Flow cannot reach.<sup>[4]</sup>

One Windows-specific gotcha: if your terminal is running as Administrator and Flow is not, Windows security blocks paste between apps at different privilege levels. Flow will show a notification prompting you to relaunch it as Administrator.<sup>[4]</sup>

Flow is not available as a native Linux application.<sup>[4]</sup> If you run Linux in WSL or a virtual machine on Windows or Mac, you can still dictate and use Paste last transcript to get text into the Linux environment. But there is no Linux binary. That is the boundary (as of Q2 2026).

## AI Coding CLIs: Claude Code and Codex

When you dictate a long prompt into Claude Code or Codex, Flow automatically splits the dictation into smaller chunks before pasting. This prevents these CLIs from collapsing or truncating long pasted content.<sup>[3,4]</sup> The chunking is automatic. You do not configure it, and you do not need to wait between chunks.

If you start a new dictation while a previous one is still pasting, the chunks can collide. Wait for the chunking to finish before triggering Flow again.<sup>[3]</sup>

## Clipboard Behavior

Flow marks dictated text as concealed when pasting, which means most third-party clipboard managers (Pastebot, Pasta, and similar tools) will not store your dictated text in their history.<sup>[3]</sup> This is deliberate. It keeps your dictation out of clipboard logs.

Flow also preserves your clipboard before pasting and restores it afterward. But some clipboard content types are not preserved: file contents, PDFs, rich text with attachments, and audio data. If a paste fails, your original clipboard content may not be restored. The Paste last transcript shortcut is your recovery.<sup>[3,4]</sup>

## Practical Patterns

A few patterns worth naming for developers who dictate:

**Speak variable names phonetically.** For `userId`, say "user I.D." or "user ID." Flow matches against the symbol list in your open editor. Say variable names clearly, without filler words, for the best recognition.<sup>[3]</sup>

**Keep relevant files open.** Flow reads context from your active editor tab and the sidebar file tree. File names from recently closed tabs are remembered across dictation sessions, but open files give the strongest signal.<sup>[1,2]</sup>

**Close unused tabs.** Flow reads context from every open tab. Fewer tabs means faster processing and fewer false matches. If Flow feels slow in your IDE, this is the first thing to try.<sup>[3]</sup>

**Use trigger words for short or ambiguous filenames.** Saying "at" or "tag" before a filename reduces false matches, especially when filenames are common English words.<sup>[2,3]</sup>

**Enter insert mode before dictating into terminal editors.** In Vim, Nano, or any modal editor, switch to insert mode first. Flow pastes text; it does not send keystrokes that navigate to insert mode for you.<sup>[4]</sup>

**Set Auto Cleanup to None or Light for code-adjacent work.** The Cleanup Dial (Ch7) applies to all dictation, including what you say in IDEs. Higher cleanup levels rewrite for clarity and conciseness, which is useful for prose but can alter technical content in unexpected ways. For commit messages, documentation, or AI prompts that reference specific code, dial cleanup down.

## Key Points

- Vibe Coding reads your IDE context to recognize code symbols and tag files by voice, but it is off by default and must be enabled in Settings.
- Cursor and Windsurf get full support with backtick formatting and file tagging; VS Code gets only screen reader integration; VS Code Insiders is unsupported.
- File Tagging lets you attach files to AI chat by saying the filename, but a Custom Dictionary substitution in the same dictation disables all tagging for that transcript.
- WSL, SSH, tmux, and screen do not support direct paste; use the Paste last transcript shortcut as your recovery path.
- Long dictations into Claude Code and Codex are automatically chunked to prevent truncation; no configuration needed.
- Flow marks dictated text as concealed so clipboard managers will not log it, and it restores your previous clipboard after each paste.
