# Sermon archive – how it works and how to add a sermon

The Sermons page on uugroton.org contains a small script that reads two files
from this repository (served by GitHub Pages) and builds the page from them:

- `sermons.csv`     – one line per sermon/service
- `transcripts.csv` – one line per transcript (rarely changes)

So a weekly update never touches WordPress. The routine is:

1. Copy the new mp3 into the repo, named `YYYY-MM-DD.mp3`.
2. Add one line to `sermons.csv` (anywhere – the page sorts by date).
3. Commit and **push**.

GitHub Pages republishes within a minute or two. Browsers cache the CSV for up
to a day, so a page you loaded earlier today may not show the new line until
tomorrow; a hard refresh (Ctrl+F5 / Cmd+Shift+R) shows it immediately.

## sermons.csv columns

| column     | what goes in it |
|------------|-----------------|
| date       | `YYYY-MM-DD` (required) |
| title      | sermon title |
| speaker    | leave **blank** for Rev. Elea Kemler; otherwise the name(s), e.g. `Rev. Megan Lynes` |
| audio      | filename in this repo, e.g. `2026-09-13.mp3`. Several files: separate with `;` and add a label after `=`, e.g. `2026-04-04-li.mp3=audio – Li Kynvi;2026-04-04-elea.mp3=audio – Elea Kemler` |
| youtube    | the YouTube video ID only – the part after `youtu.be/` or `watch?v=`, e.g. `R0KYTMAd-G8` |
| transcript | full URL of a transcript page, if any |
| html       | normally blank. If filled in, it is shown verbatim (as HTML) instead of title/speaker/links – used for a few unusual older entries |

A typical new line:

```
2026-09-13,What the Autumn Asks of Us,,2026-09-13.mp3,AbCdEfGhIjK,,
```

Same service but a guest preacher:

```
2026-09-20,Small Graces,Rev. Megan Lynes,2026-09-20.mp3,XyZ123abc45,,
```

A service whose sermon has not been extracted yet (date + YouTube only, shown
in grey): leave title and audio blank, fill in youtube.

If a title contains a comma, put the title in double quotes:
`2026-10-04,"Hope, Again",,2026-10-04.mp3,...`

## transcripts.csv columns

`date, title, url, note` – `note` is optional extra text shown after the link.

## Editing tips

- Any text editor works; keep the file as plain UTF-8 CSV (Excel is fine if
  you "Save As → CSV UTF-8").
- Don't rename the two CSV files or move them out of the repo root – the page
  fetches them at `https://uugroton.github.io/sermons/sermons.csv`.
- If the page ever shows "the sermon list could not be loaded", the usual
  cause is a push that hasn't happened yet or a CSV with mismatched quotes.
