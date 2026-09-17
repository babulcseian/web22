# How to add a new paper or news item

Both are now plain spreadsheet files. Open them in Excel or Google Sheets —
never edit them as raw text, and you will never hit a "one space breaks
everything" problem again.

---

## Editing directly on github.com (recommended workflow)

If you're working straight from the GitHub website (not a local copy),
**don't use the pencil "Edit" button** for adding or restructuring rows —
that opens the raw text, one giant line per row, which is very easy to
break by hand (especially once a title contains a comma, like the
"Smart Manhole... Status, Water Level, and Gas Detection" one, which
needs to be wrapped in quotes).

Instead, use Google Sheets as your editor, and GitHub's upload button to
save it back:

1. On the file page (e.g. `_data/publications.csv`), click **Raw** at
   the top of the file, then copy that page's URL from your browser's
   address bar.
2. Open [Google Sheets](https://sheets.google.com) → **File → Import**
   → **Insert new sheet** → paste the raw URL under "Link" → **Import data**.
   The whole file loads as a proper spreadsheet, one column per field.
3. Edit normally — click a cell to change it, or add a new row anywhere
   for a new paper/news item. You never see or touch a comma or a quote;
   Sheets handles that invisibly when you save.
4. **File → Download → Comma Separated Values (.csv)**.
5. Back on GitHub, open the `_data` folder → **Add file → Upload files**
   → drag in the file you just downloaded. GitHub sees it has the same
   name and offers to replace it → write a short commit message →
   **Commit changes**.
6. Click the file again and check the **Preview** tab — it should render
   as a clean table, like the one in your first screenshot. That's your
   confirmation the upload worked.

**Only use the pencil "Edit" button directly on GitHub for a tiny,
one-word tweak** to a value that has no comma in it — for example fixing
a typo in a title, or updating a URL. Even then, change only the exact
text between the surrounding commas and don't add or remove any comma.
If your edit would introduce a comma into a field (adding "USA, 2026"
to a title, for instance), that field needs to be wrapped in double
quotes — at that point it's safer to just do the edit in Sheets instead.

---

## Adding a new paper

1. Open `_data/publications.csv` in Excel or Google Sheets.
2. Add a new row anywhere (order doesn't matter — the website sorts by
   year automatically).
3. Fill in these columns:

   | Column      | What to put                                                  |
   |-------------|---------------------------------------------------------------|
   | type        | `journal`, `conference`, `thesis`, or `book` (lowercase)      |
   | year        | just the number, e.g. `2026`                                  |
   | title       | the paper title                                               |
   | authors     | every author separated by `|`, e.g. `Md Babul Islam | Antonio Guerrieri` |
   | me_author   | your name, spelled exactly as in the authors column — this is what gets underlined |
   | venue       | journal or conference name, e.g. `IEEE Sensors Journal (Q1)` |
   | doi         | DOI link, or leave blank                                      |
   | paper       | PDF link, or leave blank                                      |
   | code        | code repo link, or leave blank                                |
   | slides      | slides link, or leave blank                                   |
   | videos      | video link, or leave blank                                    |
   | dataset     | dataset link, or leave blank                                  |
   | figure      | image path, e.g. `/assets/img/paper/journal/my-figure.jpg`, or leave blank |
   | fit         | `cover` or `contain` — how the image is cropped               |

4. Save / export as CSV (keep the filename `publications.csv`).
5. Upload it to `_data/publications.csv` in your repo, replacing the old one.

**You never need to update a year list anywhere.** A paper for 2026, 2020,
or any year just shows up in its own year section automatically.

**A stray space before or after a link no longer matters** — every field
is trimmed automatically before it's used.

---

## Adding a news item

1. Open `_data/news.csv` in Excel or Google Sheets.
2. Add ONE new row at the very top (news is shown newest-first).
3. Fill in these columns:

   | Column       | What to put                                                  |
   |--------------|-----------------------------------------------------------------|
   | date         | e.g. `January 2026`                                             |
   | headline     | short bold title, e.g. `Paper Accepted at PiCom 2026`           |
   | description  | one or two plain sentences — no HTML needed                     |
   | location     | city/country of the event, e.g. `Tokyo, Japan` (optional — leave blank for journals or non-event news) |
   | link1_text   | label for the first button, e.g. `PiCom 2026` (optional)        |
   | link1_url    | the link for that button (optional)                             |
   | link2_text   | label for a second button, e.g. `Certificate` (optional)        |
   | link2_url    | the link for that button (optional)                             |

4. Save / export as CSV, upload to `_data/news.csv`.

**You never type any HTML tags** — no `<a href=...>`, no `<b>`, nothing.
The website builds all of that for you from the plain columns, so a
missing `href=` or an unclosed tag can no longer happen.

---

## Why this is safer than before

The old files were in YAML format, which uses `{ }` braces and `"quotes"`
that have to match up exactly — one missing quote or a stray character
could silently break an entire entry, or even the whole page. CSV files
don't have that problem: each row is just plain text in columns, and
Excel/Google Sheets handle all the quoting for you automatically, even if
a title or description contains a comma.
