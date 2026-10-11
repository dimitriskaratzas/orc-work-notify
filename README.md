# orc-work-notify

A [Claude Code](https://code.claude.com) plugin that plays a sound on three events, so you can go make tea and come back when it's time:

| Event | Hook | Sound file |
|---|---|---|
| You send a prompt | `UserPromptSubmit` | `submit.wav` |
| Claude needs you (a question, a permission prompt, idle waiting) | `PreToolUse` on `AskUserQuestion`, `Notification` | `attention.wav` |
| Claude finished the task | `Stop` | `stop.wav` |

Sounds play in the background, so they never slow Claude down.

## Install

```sh
claude plugin marketplace add vagkaratzas/orc-work-notify
claude plugin install orc-work-notify@orc-work-notify
```

Then restart Claude Code or run `/reload-plugins`.

## Bring your own orc

The plugin ships **no voice clips**. Without clips it falls back to your system's sounds for `attention` and `stop` (freedesktop `message`/`complete` on Linux, `Ping`/`Glass` on macOS); `submit` stays silent.

Drop your own clips in, named after the event; the most specific wins:

| Where | Applies to |
|---|---|
| `~/.claude/sounds/{submit,attention,stop}.wav` | every project |
| `<project>/.claude/sounds/{submit,attention,stop}.wav` | that project only |

Any line you like, e.g. a grumpy *"Work work!"* for `submit`, *"Something need doing?"* for `attention` and *"Ready to work!"* for `stop`. Use clips you have the rights to: record your own, or pick CC0 voice packs (e.g. on [OpenGameArt](https://opengameart.org) or [Freesound](https://freesound.org)).

## Mute

Any non-empty `~/.claude/orc-work-notify.muted` silences it:

```sh
echo 1 > ~/.claude/orc-work-notify.muted   # mute
: > ~/.claude/orc-work-notify.muted        # unmute
```

## Players

Tries `afplay` (macOS), `pw-play`, `paplay`, `ffplay`, `aplay` in that order, falling through when one is missing or fails. Windows is not supported (PRs welcome).

## License

MIT
