# Enlistment Hub ✎

A cozy-notebook class enlistment planner. Load the class offerings and your IPS, pick sections without clashes, auto-build schedules, and line up classes with up to three friends.

It's a web version of the Google Sheets "Enlistment Hub" sidebar. Everything runs in the browser: files are never uploaded, and plans are saved in the browser's local storage.

## Put it on GitHub Pages

1. Create a public repository on GitHub.
2. Upload `index.html` and this README to the repository root.
3. Go to **Settings → Pages**. Set **Source** to "Deploy from a branch", choose `main` and `/ (root)`, then save.
4. After a minute, the site is live at `https://<your-username>.github.io/<repo-name>/`.

## Tabs

**Setup**
- **Who's planning:** it starts with just you. Add friends only if you want to compare, up to 4 people (lilac, sky, mint, rose).
- **Avatars:** tap a person's circle to give them an emoji.
- **IPS subjects:** type or paste them, or import from an IPS file.
- **Busy times:** org meetings, work or commute. Classes that overlap them count as clashes.
- **Class offerings, four ways in:**
  - upload an `.xlsx`/`.csv`
  - paste a Google Sheets link (the sheet must be published to the web), with a "↻ refresh" button that keeps everyone's picks
  - paste rows copied from Google Sheets
  - type classes in

**Pick**
- Choose whose plan you're editing and tap a section card to add it. Clashes show before you pick.
- On each section card:
  - **☆ star** marks a favorite
  - **✎ note** saves private notes on the section or the prof, and lets you mark a prof 👍 prefer or 👎 avoid
  - **+ backup** makes it Plan B or C
- The preview panel shows:
  - a live mini timetable
  - a **clash fixer** that suggests one-tap swaps, like "move ENG 12 → E"
  - 🚶 **tight walk** warnings for back-to-back classes in different buildings (from the room prefix, like K, SOM, CTC, BEL)
  - 🍱 **no lunch break** warnings
- **Drafts:** save versions of your picks, like "chill sched" or "MWF only", and switch between them.

**Auto-build**
- Generates every clash-free combination of sections for the IPS subjects.
- **Filters:** no Saturdays, earliest class, done-by time, max hours per day, max classes in a row, one weekday free, keep a lunch break, skip avoided profs, keep current picks.
- **Sorting:** fewest days, shortest breaks, latest start, ★ favorites, or most classes with friends.
- **Friends together:** builds for 2–4 people at once, maximizing shared sections.

**Week**
- Everyone's timetable in lanes, with busy times shaded. Zoom into a day or save it as an image.
- Tap an empty spot to see which sections meet then.
- "Week in numbers" stats for each person.

**Compare**
- Match up shared subjects (with "everyone → section X"), see classes together, and find free time together.

**Checklist**
- Plan A, B and C for every IPS subject. Copy it as text or save it as an image.

## Share links & QR codes

**🔗 share plan** creates a link and a QR code containing that person's subjects, picks, backups, busy times, stars and emoji.
Opening the link, scanning the code, or pasting it into **add a friend's share code** adds the plan to Compare. Notes stay private and are not shared.

## Sheet format

Same as the Apps Script version.

- **Columns:** Select (one per person) | Subject | Section | Day | Time | Room | Instructor | Remarks | Pair Subject. The header row is found by name, so repeated header blocks are fine.
- **Days:** `Mon`, `Monday`, `SAT`, `Mon, Thu`, or `Daily`.
- **Times:** `0730-0900`, `0930–1100`, `7:30-9:00`, or `1:00-2:30`. Times before 7:00 count as PM.
- **IPS ranges (Potential IPS sheet):**
  - 1st semester: `A10:A15` / `E10:E15`
  - 2nd semester: `A18:A25` / `E18:E24`

  You can change these in Setup.

Export writes one Select column per person, plus an "IPS Subjects" sheet.
