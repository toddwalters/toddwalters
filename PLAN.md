# GitHub Profile README — Build & Deploy Plan

**Goal:** Stand up an awesome profile README at `github.com/toddwalters` using the
playful/animated/skills-forward design, plus the contribution-snake animation.

**Target machine:** Mac Studio M4 Max · tools: `gh`, `git`, Claude Code
**Project folder:** `/Users/toddwalters/Documents/Projects/Claude`

---

## Files in this project

| File | Current location | Destination in repo | Purpose |
|------|------------------|---------------------|---------|
| `README.md` | project folder root | repo root | The profile banner GitHub renders |
| `snake.yml` | project folder root | `.github/workflows/snake.yml` | Daily-regenerated contribution snake SVG |

> Note: `snake.yml` currently sits at the project root. Step 1 moves it into
> `.github/workflows/` — GitHub Actions only detects workflows in that path.

---

## Step 1 — Stage the files into repo layout

The final repo needs this structure:

```
toddwalters/
├── README.md
└── .github/
    └── workflows/
        └── snake.yml
```

From the project folder, create the workflow path and move snake.yml into it:

```bash
cd ~/Documents/Projects/Claude
mkdir -p .github/workflows
mv snake.yml .github/workflows/snake.yml
```

## Step 2 — Create the repo and push

> ⚠️ The repo MUST be named exactly `toddwalters` (matching the username) for
> GitHub to treat it as the profile README repo.

```bash
git init -b main
git add .
git commit -m "Add profile README + contribution snake workflow"
gh repo create toddwalters --public --source=. --remote=origin --push
```

If `gh` is not authenticated yet: run `gh auth login` first, then retry.
If a `toddwalters` repo already exists: either delete it (`gh repo delete toddwalters`)
or add it as a remote and push to the existing one.

## Step 3 — Activate the snake animation

- The workflow runs on push, daily (midnight UTC), and on demand.
- If the snake image is still blank after ~1 min:
  - Repo → **Actions** tab → if prompted, click **"I understand my workflows, enable them"**
  - Select **"Generate Snake"** → **Run workflow** → run on `main`
- First run takes ~30s; it writes the SVG to an `output` branch, which the README references.

## Step 4 — Pin repositories (manual, web UI)

On `github.com/toddwalters` → **Customize your pins** → select:
- `configs-guides-and-cheatsheets`
- `aiml-python-coding-examples`
- `waltodders-hugo`

This makes the native profile pins match the README's project cards.

## Step 5 — Verify the live page

Visit `github.com/toddwalters` and confirm:
- [ ] Animated typing header renders and cycles taglines
- [ ] Status badges + visitor counter show
- [ ] `class Todd` code block displays
- [ ] Skill icons + tech badges load
- [ ] Stats / top-langs / streak cards populate (may take a moment on first load)
- [ ] Three project cards render and link correctly
- [ ] Trophy cabinet shows achievements
- [ ] Snake animation appears (after Step 3)

---

## Known caveats

- **`waltodders-clawbot`** is mentioned in the README text but has NO project card,
  because it appears to be private and card generators can only read public repos.
  If it goes public later, a 4th card can be added.
- **Streak-stats card** runs on a free third-party host that occasionally goes down;
  a temporarily broken image there is the service, not your setup.
- All stat/card/snake images are live widgets — they self-update, no maintenance.

## Optional follow-ups

- Set the profile **bio** line (separate from README) at github.com/settings/profile.
- Swap trophy cabinet for more project cards, or reorder sections, anytime.
