# mdshow

A desktop window that shows a file and keeps up with it — markdown rendered as formatted prose, everything else as plain text.

Point it at a file, edit that file in your usual editor, press Save, and the window catches up within a second without you touching it. It is meant to sit beside your editor: a live preview of a README you are writing, or a readable pane for a log that is still being appended to.

## What it does

- Opens in an ordinary window with a **Select File** button at the top.
- Remembers the file you chose, so the next run goes straight to it — and remembers the window's size and position too.
- Re-reads the file **once a second** and redraws **only when the text has changed**, so an idle window costs one file read per second and nothing else.
- Renders `.md` and `.markdown` files as formatted prose — headings, lists, bold, links, tables, code blocks. The extension match ignores case.
- Shows **every other file exactly as it is**, in a plain-text panel you cannot type into. No formatting is attempted, and leading spaces and blank lines survive.
- Carries the **full path of the file being watched** in the title bar.
- On a first run, with nothing chosen yet, asks for a file using your system's own file chooser.
- Says so rather than failing when the file it is watching is deleted or cannot be read.

## Requirements

A desktop session and Python 3. The window is a real Qt window, supplied by PySide6, which the install below brings with it.

Developed on Linux. Nothing in it is platform-specific, so macOS and Windows are expected to work, but only Linux has been tried.

## Installing AllSpeak

mdshow is written in [AllSpeak](https://allspeak.ai), a scripting language that reads like English, so you need the AllSpeak runtime:

```sh
pip install allspeak-ai
```

A virtual environment keeps it clear of everything else:

```sh
python3 -m venv .venv
source .venv/bin/activate
pip install allspeak-ai
```

On Linux, pip may put the `allspeak` command in `~/.local/bin`, which is not always on your `PATH`. If you get `allspeak: command not found`, run:

```sh
export PATH="$HOME/.local/bin:$PATH"
```

To make that permanent, add this to your `~/.profile`:

```sh
# set PATH so it includes user's private .local/bin if it exists
if [ -d "$HOME/.local/bin" ] ; then
    PATH="$HOME/.local/bin:$PATH"
fi
```

To check the install, run:

```sh
allspeak --version
```

You should see the AllSpeak version and nothing else — running `allspeak` on its own does the same.

## Running mdshow

```sh
git clone https://github.com/easycoder/mdshow.git
cd mdshow
allspeak mdshow
```

The `.allspeak` extension is optional. There is no build step and nothing to install beyond AllSpeak itself.

## Using it

**Select File**, the only button, opens your system's file chooser — pick any text file. The path is remembered immediately, so even a run you kill from the terminal keeps it. Cancelling the chooser leaves the file you were already watching in place.

Markdown is rendered; anything else is shown as it is. `README.md` arrives with its heading in large type; `config.toml` arrives with its comments and indentation untouched.

The window re-reads the watched file once a second and redraws only when something has really changed. Edit the file and the window follows; leave it alone and nothing happens.

The title bar always names the file on screen, which is the one place the full path is visible.

## Where your settings live

Everything mdshow remembers is in `.mdshow.conf`, beside the script:

```json
{
    "x": 300,
    "y": 150,
    "width": 640,
    "height": 480,
    "file": "/home/you/notes/README.md"
}
```

The `file` entry is written as soon as you choose a file. The four geometry values are written when the window closes — so closing the window normally saves its position, while killing the process (`Ctrl-C`) leaves the last saved position in place. Delete the file to start over: the next run asks for a file and opens at 800x600 in the middle of the screen.

## Licence

Apache License 2.0 — see [LICENSE](LICENSE).