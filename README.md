# Enlistment Hub ✎

A cozy-notebook class enlistment planner. Load the class offerings and your IPS, pick sections without clashes, auto-build schedules, and plan together with friends in rooms that sync live through a Google Sheet.

Files:
- `index.html` is the whole website.
- `Sync.gs` is the script that goes in your Google Sheet. It's only needed for syncing with friends.
- `Enlistment Hub Sheet.xlsx` is a ready-made Google Sheet to upload, with one tab per term:

| Tab | Term |
|---|---|
| SY 26-27 1st sem | 1st semester (filled in from your pasted list) |
| SY 26-27 2nd sem | 2nd semester (filled in from the 3rd Year Scheds PDF) |
| SY 27-28 0th sem | intersession |
| SY 27-28 1st sem | 1st semester |
| SY 27-28 2nd sem | 2nd semester |

---

## 1. Put the site on GitHub Pages

1. Upload `index.html` and `README.md` to your repository (`Sync.gs` is optional here).
2. Go to **Settings → Pages**. Set **Source** to "Deploy from a branch", choose `main` and `/ (root)`, then save.
3. After a minute, the site is live at `https://<your-username>.github.io/<repo-name>/`.

The site already works on its own at this point. Everything is saved in your browser only.

---

## 2. Turn on syncing with your Google Sheet (about 5 minutes, done once)

Only the person who owns the Google Sheet does this. Friends just open the site and join.

> **Easiest:** upload `Enlistment Hub Sheet.xlsx` to Google Drive, open it, and choose **File → Save as Google Sheets**. Use that new copy (scripts only work in real Google Sheets).
> Or use your own sheet: any tab with a **Subject** header row counts as a term.

### a. Add the script
1. Open your Google Sheet → **Extensions → Apps Script**.
2. Your existing `code.gs` can stay. Click **＋** next to *Files* → **Script**, name it `Sync`, and paste in everything from `Sync.gs`. Click 💾 **Save**.
   - If your project already has a function called `doPost`, delete that old one. Your `doGet` is fine.
3. At the top, choose the function **`EH_setup`** and click **▶ Run**.
4. Google asks for permission. This is your own script asking to edit your own sheet:
   - **Review permissions** → choose your account → **Advanced** → **Go to … (unsafe)** → **Allow**.
   - This creates hidden tabs: **EH Profiles**, **EH Rooms**, **EH Archive** and **EH Stats**.

### b. Deploy it as a web app
1. Click **Deploy → New deployment** → the ⚙ gear → **Web app**.
2. Set **Execute as: Me** and **Who has access: Anyone**.
   - "Anyone" only means the site can reach the script. Nobody can see or change a plan without a room code or PIN.
3. Click **Deploy** and copy the **Web app URL** (it ends in `/exec`).

### c. Connect the site
Pick one:
- **Recommended:** on GitHub, open `index.html` → ✏️ **Edit**.
  1. Search for `const SYNC_URL = '';`.
  2. Paste your URL between the quotes, e.g. `const SYNC_URL = 'https://script.google.com/macros/s/…/exec';`.
  3. **Commit changes**. Now everyone who opens the site is connected automatically.
- **Or:** open the site → **Setup → Plan together, live**, paste the URL there, and tap **connect**. Only your browser remembers it, but your invite links carry it to friends.

### d. Updating the script later
If you ever change `Sync.gs`:
1. Paste the new version over the old one and click 💾 **Save**.
2. Run **`EH_setup`** once more. It adds any new hidden tabs and columns, and never deletes data.
3. **Deploy → Manage deployments → ✏️ → Version: New version → Deploy**. The URL stays the same, so the site keeps working.

---

## 3. Using it with friends

1. **Make a profile:** Setup → *create my profile* → your name and a PIN (4–12 characters).
   - Your current picks come along.
   - You get a **personal code** (like `XDTVQ-5TUCD`). Save it to sign in on other devices.
2. **Make a room:** use the 👥 room menu at the top, or Setup → *+ new room*. Name it (e.g. "blockmates").
3. **Invite:** share the link, the QR code, or the 8-character room code (like `TTDQ-5KX2`).
   - Friends open it, make a quick profile, and they're in.
4. **Plan:** everyone sees each other's picks update every few seconds. Use the room menu at the top to switch between rooms, or pick **just me** to see only your own plan.

### Room extras
- **What's new:** the Compare tab starts with the room's activity, like "Bea picked THEO 13 – D2" or "Bea switched THEO 13 from D1 to D2". A red number on the Compare tab shows what you haven't seen yet.
- **💌 Join me:** on a section you picked, tap *ask … to join* (it shows when a friend needs that subject but isn't in your section). You can also tap 💌 in *Match up*.
  - Your friend gets a pop-up. **Yes, join!** switches them into that section, and you see "Bea joined you" in What's new.
  - *Later* keeps the request in their What's new card.
- **💬 Room notes:** tap *✎ note* on a section. The *Room note* box is seen by everyone in the room (140 characters). The 📝 private box stays private.
- **Reactions:** while viewing a friend's plan, tap ❤️ 😭 🤝 🔥 👀 on their picked sections. They see "🔥 Bea" on their card. Tap again to remove it.

### How it's kept safe
- **Your PIN protects your plan.** Friends can see your picks, but only you can change them, in every room.
- **Room codes control who can join.** A room holds up to 4 people, and you can be in up to 20 rooms.
- **Room creators** can rename the room, remove someone, or make a **new room code** (old invite links stop working).
- **PINs and recovery codes are never stored**, only scrambled (salted hashes).
- **Forgot your PIN?** Everyone gets a one-time **recovery code** when they make a profile (screenshot it!). On the sign-in screen, tap **forgot PIN?**, enter the recovery code and a new PIN. You then get a new recovery code, and other devices are signed out.
  - Lost it, or made your profile before recovery codes existed? Setup → *your account* → **🔑 new recovery code** (while you're still signed in).
- **Wrong-PIN lockout:** after 5 wrong tries (PINs or recovery codes), the profile locks for 15 minutes. The lock doubles each time after that.
- **The sheet owner can see** everyone's saved plans and notes in the hidden *EH* tabs, but never their PINs. Notes are private from friends, but not from the sheet owner.
- **Undoing mistakes:** if something goes wrong, use **File → Version history** in the sheet.

### Good to know
- **Class offerings** come from the sheet's term tabs.
  - To fix or add a class, edit the tab, then tap **↻ refresh** in Setup. Changes show up within about a minute.
  - Empty tabs show "waiting for offerings" on the *Start here* tab. Paste the classes in when they come out.
  - **New term:** duplicate a tab and rename it, e.g. `SY 28-29 1st sem`. Keep **0th**, **1st** or **2nd** in the name.
  - The site opens the tab that matches your IPS subjects. Everyone can switch tabs in Setup.
  - People with no subjects yet start on `DEFAULT_TAB` (set at the top of `Sync.gs`, currently `SY 26-27 2nd sem`).
- **IPS files are matched to the open tab automatically.**
  - The site finds every *Intersession / First Semester / Second Semester* list in your IPS. A **0th sem** tab uses Intersession, **1st sem** uses First Semester, and so on.
  - The year is worked out from the classes offered. Once *SY 26-27* matches your Third Year, *SY 27-28* uses Fourth Year, even before its classes are posted.
- **Electives are flexible slots.**
  - IPS lines like `IE 2`, `MGT Elective`, `CTM Elective`, `FREE Elective`, or `FAA 123 · Management Elective` (a code whose IPS description says "Management Elective") can be filled by any subject that fits the rule.
  - In **Pick**, tap *Choose a subject* to see only the eligible subjects offered in the open tab. Or leave it to **Auto-build**, which tries them all.
  - **Nothing is doubled:** a subject fills only one line, and subjects required anywhere in your IPS never fill an elective.
  - Rules live in the sheet's **Electives** tab (Elective | Counts | Except | Notes). *Counts* can be subject codes (`ENE 13.03i`), code prefixes (`MKTG`), `ends in i`, `any`, or another elective's name (`Management Elective`).

  | Elective | Counts |
  |---|---|
  | IE 1 | ENE 13.03i, 13.04i, 13.05i, 13.06i |
  | IE 2, IE 3 | any code ending in **i**, except those four |
  | Management | MKTG, LLAW, FAA, LAS, ITMGT, OPMAN, FINN, ACCT, DECSC, QUANT |
  | CTM | any management elective, or any ECON, CSCI or COMM subject |
  | ECON | any ECON subject |
  | FAA | any FAA subject |
  | FREE | anything not required anywhere in your IPS |
  | LEAD/BUSETH | any subject, until the real rule is known |

  The ECON, FAA and LEAD/BUSETH rules are assumptions. Edit the Electives tab if they're wrong.
- **Forgot your PIN and lost the recovery code?** The sheet owner can delete your row in **EH Profiles** so you can make a new profile. Your synced plan is lost, so re-pick your sections.
- **Owner stats:** the *Start here* tab has a **📊 Hub stats** area: profiles, people active this week, rooms, average room size, archived rooms, and the most picked sections. The script refreshes it about every 15 minutes while people use the site, or run **`EH_refreshStats`** in Apps Script to refresh it now.
  - Older sheets without that heading get it added at the bottom of *Start here*.
- **Old rooms tidy themselves up:** a room nobody has opened for about a term (150 days, `ARCHIVE_DAYS` in `Sync.gs`) moves to the hidden **EH Archive** tab and disappears from everyone's room list. Joining with the old room code brings it back for everyone who was in it. Run **`EH_archiveOldRooms`** to tidy up right away.
- **Signing out** of a device keeps a local copy of your plan. Your synced plan stays in the sheet.
- **The ticks in the sheet's Select columns** aren't updated by the site. Picks are saved per person in the *EH Profiles* tab instead.

---

## 4. Features

- **Pick:**
  - tap sections to add them, with clash warnings before you pick
  - in a room: 💌 join-me requests, 💬 room notes and reactions
  - ★ favorites, private notes, 👍/👎 profs, and Plan B/C backups
  - a clash fixer, 🚶 tight-walk and 🍱 lunch warnings, and saved drafts
- **Auto-build:**
  - every clash-free schedule, with filters for Saturdays, earliest and latest class, hours per day, classes in a row, a free weekday, lunch, and avoided profs
  - **friends together** finds combos with the most shared sections
- **Week:** everyone's timetable in lanes, with busy times shaded. Tap an empty slot to see what's offered then. Includes week-in-numbers stats and saving as an image.
- **Compare:** the room's *What's new* feed, then match up shared subjects, see classes together, and find free time together.
- **Checklist:** Plan A, B and C for every IPS subject. Copy it as text or save it as an image.
- **Day / night:** the ☀ / ☾ switch at the top right.
- **Without syncing:** everything also works offline on one device, with up to 4 people and share links / QR codes.

## Sheet format

- **Columns:** Select | Select | Subject | Section | Day | Time | Room | Instructor | Remarks | Pair Subject. The header row is found by name, so repeated header blocks are fine.
- **Days:** `Mon`, `Monday`, `SAT`, `Mon, Thu`, or `Daily`.
- **Times:** `0730-0900`, `0930–1100`, `7:30-9:00`, or `1:00-2:30`. Times before 7:00 count as PM.
