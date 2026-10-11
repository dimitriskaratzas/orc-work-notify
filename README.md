# orc-work-notify

A [Claude Code](https://code.claude.com) plugin that plays a sound when Claude finishes a task (`Stop`) or needs your attention (`Notification`, e.g. a permission prompt). So you can go make tea and come back when it's time.

## Install

```sh
claude plugin marketplace add vagkaratzas/orc-work-notify
claude plugin install orc-work-notify@orc-work-notify
```

Then restart Claude Code or run `/reload-plugins`.

## Bring your own orc

The plugin ships **no voice clips**. Out of the box it plays your system's sounds (freedesktop `complete`/`message` on Linux, `Glass`/`Ping` on macOS).

Drop your own clips in, named after the event; the most specific wins:

| Where | Applies to |
|---|---|
| `~/.claude/sounds/stop.wav`, `~/.claude/sounds/attention.wav` | every project |
| `<project>/.claude/sounds/stop.wav`, `.../attention.wav` | that project only |

Any line you like, e.g. a grumpy *"Work complete!"* for `stop` and *"Something need doing?"* for `attention`. Use clips you have the rights to: record your own, or pick CC0 voice packs (e.g. on [OpenGameArt](https://opengameart.org) or [Freesound](https://freesound.org)).

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
