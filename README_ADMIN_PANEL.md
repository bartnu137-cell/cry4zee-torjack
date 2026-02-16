# Padayon Portal – Admin Panel (Inline)

This build adds an **inline Admin Panel** inside `index.html` (no separate admin HTML page).

✅ This ZIP is a **full bundle** (includes `index.html`, `style.css`, `admin.js`, `script.js`, `database.js`).
Keep all files in the **same folder** so buttons like `goToLevel1()` work correctly.

## Default Admin Account

- **Username:** `ADMIN`
- **Password:** `admin123`

> ⚠️ Accounts are stored in **localStorage** (plain text). This is **NOT secure** for real production hosting.

---

## What the Admin Panel Can Do

### 1) Quiz Set (Question Builder)
- Create quiz sets in ANY folder path (e.g. `UNDERGROUNDS/TERMS & OBJECTIVES/ESAS PAST BOARD (UG)`).
- Add questions manually.
- **Import questions from a `.json` file**.
- Export a selected quiz set into `.json`.

### 2) Notes (PDF Upload)
- Upload and attach PDFs to **ANY folder path**, including:
  - `EXHALE FILE/NOTES`
  - `PAWER-LAYN FILE/NOTES`
  - `UNDERGROUNDS/FORMULAS`
  - `UNDERGROUNDS/CALCULATOR TECHNIQUES`
  - `T-AY-PI/OTHER`
  - …and any new folder you create

> PDFs are stored in **IndexedDB** (browser storage). If you clear browser storage/site data, PDFs will be lost.

### 3) Archive Folder Builder
- Create folders in **any category/subcategory/sub-subcategory**, even future “new” folders.
- Use **Target folder path** + **Folder name**, then click **CREATE ARCHIVE FOLDER**.

### 3.1) Folder Tools (Rename / Move / Delete)
- **Rename folder** (recursive): renames the folder in *Target folder path* and moves all its contents.
- **Move folder** (recursive): moves the folder in *Target folder path* to a new parent path.
- **Delete folder** (recursive): deletes a folder and everything under it (built-in sets are protected).

> ⚠️ Folder delete is destructive. Use Backup first.

### 3.2) Quiz Set Tools (Move / Delete)
- **Move selected quiz set** to another folder path.
- **Delete selected quiz set**, with an option to also delete its stored questions.

### 4) Accounts
- Create user accounts
- Delete accounts (you can’t delete your own currently logged-in account)

### 5) Online + Logs
- Shows “online users” and their activity.
- **Important:** Because this is a static/offline app, “online users” only tracks sessions in the **same device + same browser profile** (multiple tabs).

### 6) Admin Search
- Search **folder paths**, **quiz sets**, and **PDFs**.
- Click results to quickly set the target path, open folders, select quiz sets, or open PDFs.

### 7) Remember Me + Forgot Password
- **Remember** keeps you logged in on the same device/browser (stored in localStorage).
- **Forgot password** opens your email app (mailto) to contact the admin: `bartnu137@gmail.com`.

### 8) One-account-per-session (Best-effort)
This build prevents multiple tabs in the **same browser profile** from logging in to the **same account at the same time**.

> ⚠️ Without a server/database, it is **NOT possible** to enforce “one device only” globally.

### 9) Screenshot Prevention (Reality Check)
Browsers **cannot reliably block screenshots**. This build only adds **best-effort** protections (disables right-click outside inputs, blocks some shortcuts).

---

## JSON Import Format for Quiz Questions

You can import JSON in **two formats**:

### Format A – Import into the currently selected quiz set
A JSON file that is simply an array of questions:

```json
[
  {
    "topic": "Algebra",
    "q": "What is 2 + 3?",
    "options": { "a": "4", "b": "5", "c": "6", "d": "7" },
    "key": "b",
    "soln": "2 + 3 = 5",
    "caltech": ""
  }
]
```

### Format B – Create a new quiz set from the JSON file
An object with a `set` block + a `questions` array:

```json
{
  "set": {
    "title": "PAST BOARD 4 (UG)",
    "path": "UNDERGROUNDS/TERMS & OBJECTIVES/ESAS PAST BOARD (UG)"
  },
  "questions": [
    {
      "topic": "Thermo",
      "q": "A sample question…",
      "options": { "a": "Choice A", "b": "Choice B", "c": "Choice C", "d": "Choice D" },
      "key": "a",
      "soln": "Solution text (supports HTML + MathJax).",
      "caltech": "Calculator steps (optional)."
    }
  ]
}
```

---

## Question Fields (Required vs Optional)

### Required
- `q` – question text
- `options` – either:
  - object: `{ "a": "...", "b": "...", "c": "...", "d": "..." }`
  - OR array: `["A", "B", "C", "D"]`
- `key` – correct option letter: `"a" | "b" | "c" | "d"`

### Optional
- `topic` – string
- `soln` – explanation/solution (HTML + MathJax OK)
- `caltech` – calculator technique text
- `id` – number (if missing, the system will auto-number questions)

### Notes about `ans`
The app internally stores `ans` as the **answer text** (not the letter).  
If you don’t provide `ans`, the importer automatically uses `options[key]`.

---

## Tips

- For best consistency, use paths from the **Quick pick** dropdown in Admin Panel.
- If you type a brand-new path, the app will auto-create folders along that path.
- Built-in sets (`math`, `esas`, `ug1`, `ug2`, `ug3`) are **read-only** (they come from `database.js`).

