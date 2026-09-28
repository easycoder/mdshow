# Run it

    allspeak mdshow

**Restart it if it is running** — `mdshow.allspeak` was rewritten.

The window now watches whatever file `.mdshow.conf` names, instead of always `DIFF.md`:

- No config file, or none naming a file, opens the system file chooser at startup. Cancel it and you get the empty window plus the Select File button, not an error.
- **Select File**, at the top of the window, opens the same chooser again. The path you pick is written to `.mdshow.conf` straight away, so it survives even a run you kill rather than close.
- `.md` and `.markdown` files render as formatted prose, as before. **Every other file shows as read-only plain text** — you cannot type into it.
- The window title is the **full path of the file being watched**, following it each time you pick a new one. With no file chosen it stays `mdshow`.
- A file that is deleted while you watch it, or a path you cancel out of, leaves the panel saying so rather than blanking.

First run with no config: 800x600 centred, as before. Size and position are still saved when the window closes.
