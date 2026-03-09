# RestCleaner for Sibelius

A small Sibelius plugin that automatically cleans and normalizes rests according to common engraving rules.

This plugin was created to help fix common rest notation problems that often appear when writing or importing scores.

---

## Features

Current version (v1.0) supports:

### Fix illegal rests

Automatically splits illegal cross-beat quarter rests.

Example (4/4):

Incorrect:

| 1 + | 2 |
   [quarter rest]

Correct:

| 1 + | 2 |
 8rest 8rest

---

### Merge legal rests

The plugin merges rests when allowed by engraving rules.

Examples:

16 + 16  ->  8  
8 + 8    ->  4  
4 + 4    ->  2  (only in beats 1–2 or 3–4 in 4/4)

The plugin avoids merges that hide beat structure.

---

## Currently Tested Meter

- 4/4 (primary target)

Other meters may work but are not fully tested yet.

Future versions may support:

- 3/4
- 6/8
- automatic time signature detection

---

## Installation

Download the plugin file:

plugin/RestCleaner.plg

Copy it to your Sibelius user plugin directory.

### Windows

C:\Users\<username>\AppData\Roaming\Avid\Sibelius\Plugins\

### macOS

~/Library/Application Support/Avid/Sibelius/Plugins/

You may create a subfolder such as:

Plugins/Rest Cleaner/

Restart Sibelius after installing.

---

## Usage

1. Select a passage in your score.
2. Run the plugin:

Plugins → Rest Cleaner → RestCleaner

The plugin will:

1. Fix illegal rests.
2. Merge legal adjacent rests.

---

## Safety Notes

It is recommended to:

- Save your score before running the plugin
- Test on a copy first

You can always undo with:

Mac: Cmd + Z  
Windows: Ctrl + Z

---

## Known Limitations

Current version:

- does not distinguish voices
- may behave unexpectedly in complex tuplets
- primarily optimized for 4/4

---

## Future Improvements

Possible improvements:

- automatic meter detection
- better 3/4 support
- better 6/8 support
- voice-aware processing
- optional "detect only" mode

---

## License

This project is released under the MIT License.

---

## Author

Created by **Deciras**

If you encounter issues or have suggestions, feel free to open an issue.
