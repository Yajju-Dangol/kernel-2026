# AI-Assisted Coding & AI Agents — Student Handbook

Six short pages. Each one ends with something you run or something you see.

1. Install OpenCode
2. Add treg (3,800+ tools)
3. Add a skill
4. Plan & Build
5. `AGENTS.md`
6. Build the quiz app

---

## 1. Install OpenCode

OpenCode is a free, open-source AI coding agent. You talk to it in a chat window; it
reads your files, edits them, and runs your commands.

### Download the desktop app

Go to **https://opencode.ai/download** and pick your system:

| System | Install |
|--------|---------|
| Windows | Download the `.exe` installer |
| macOS | Download the `.dmg`, or `brew install --cask opencode-desktop` |
| Linux | Download the `.deb` or `.rpm` |

Open it. On first launch it asks you to sign in — choose **OpenCode Zen** (simplest)
or connect a provider you already pay for (Claude, GPT, Gemini, Copilot).

### Open your project

Click **Open Folder** and choose your project directory. That folder is now the
workspace — OpenCode only sees and changes files inside it.

### Make your first project

1. Make an empty folder called `my-project`.
2. Open it in OpenCode.
3. In the chat, type:

```
Create a simple to-do app in one HTML file. Three tasks, an input box, an add
button, and a way to delete a task. Dark theme, rounded blue buttons.
```

4. Open `index.html` — the file is on your disk. The code exists.

### Two things to know

| Key / symbol | Does |
|--------------|------|
| **Tab** | Switch between **Build** and **Plan** mode (page 4) |
| **@** | Attach a file — `@index.html`, or `@src/App.tsx#L20-40` |

Type `/` to see every command. The two you will use most: `/init` (writes
`AGENTS.md`) and `/undo` (reverts the last change).

---

## 2. Add treg — 3,800+ tools in one line

treg is an MCP server. MCP is a bridge that gives OpenCode tools it doesn't have
built in (slide 17). With treg, OpenCode can reach SEO data, backlinks, social and
trends, company data, ads, scraping, and image/video generation — with no API keys
of your own, billed in fractions of a cent.

### Step 1 — Get your treg API key

1. Go to **https://treg.to** and sign up (GitHub or email).
2. Create a team (any name — "class-project" is fine).
3. Open the dashboard → your team → **API key**.
4. Copy the key. It looks like `trg_...`

New teams get **$1.00 free**, once. That is plenty for everything in this handbook.

### Step 2 — Paste this prompt into the OpenCode chat

Replace `<YOUR_KEY>` with the key you copied:

```
Set up treg for me using this one-line installer, with my API key attached:

curl -fsSL https://treg.to/install.sh | sh -s -- --token <YOUR_KEY>

That single command installs the treg CLI, signs me in, and registers treg as an
MCP server in OpenCode. After it finishes, confirm it worked and list the new tools
I now have.
```

OpenCode runs it, then reports back what you gained. You should see ten new tools:
`catalog_search`, `catalog_get`, `call`, `balance`, `my_tools`, and the rest.

> No key to hand? Paste this instead and OpenCode will walk you through signing in:
> `Set up treg - https://treg.to/llms.txt`

### Step 3 — Restart OpenCode

**Quit the app completely and open it again.** Tools are only discovered at startup.

### Step 4 — Prove it works

Type this in the chat:

```
Use the treg MCP. Call the balance tool and tell me how much credit I have left.
```

Then try a real one:

```
Use the treg MCP. Search the catalog for "linkedin job listings" and show me the
options with their price per call. Don't call anything yet.
```

### The three rules

1. **Search → read the price → call.** Never guess a tool name.
2. **Say the price out loud** before spending more than a cent.
3. **A failed search is free.** A wrong request is not — read the price first.

---

## 3. Add a skill

A skill is a small instruction file that teaches OpenCode how to do one job well —
how your team writes code, how you run tests, how your design system looks. It's
plain text. You install it once and it stops the AI guessing every time.

### Step 1 — Browse the directory

Go to **https://agenticskills.io/skills** — 193+ curated skills.

Good first ones for this class:

| Skill | What it does |
|-------|--------------|
| **react-best-practices** | Hooks, composition, performance |
| **frontend-design** | Stops generic AI-looking interfaces |
| **webapp-testing** | Tests your app in a real browser |
| **systematic-debugging** | Finds the root cause before fixing |
| **deploy-to-vercel** | Ships your app |

### Step 2 — Copy the one-liner

Open any skill's page. It shows one copy-paste command, something like:

```
npx skills add vercel-labs/skills@react-best-practices
```

### Step 3 — Paste it into the OpenCode chat

Don't run it yourself — give it to OpenCode:

```
Install this skill for me:

npx skills add vercel-labs/skills@react-best-practices

Then make sure OpenCode can use it: the skill must end up at
.opencode/skills/<skill-name>/SKILL.md, where <skill-name> matches the `name`
field in its frontmatter and is lowercase-with-hyphens. Don't edit the skill's
instructions. Show me what you added.
```

OpenCode installs it and shows you every file it wrote. Read that before you accept.

### Step 4 — Restart OpenCode

Quit and reopen the app. Skills are discovered at startup.

### Step 5 — Use it

Skills are not slash commands. Ask for the job in normal words:

```
Use the react-best-practices skill. Review src/components/LiveLeaderboard.tsx and
list every rules violation with its line number.
```

OpenCode loads the skill, then follows only that skill's rules. That's the whole
point: one skill, one job, every time.

> **Skill not showing up?** Check the file is `SKILL.md` (all caps), has `name` and
> `description` in its frontmatter, and that the folder name matches `name`.

---

## 4. Plan & Build

Two modes, one key.

| Mode | Press | What it does |
|------|-------|--------------|
| **Build** | Tab | Does the work. Full access to edit files and run commands. |
| **Plan** | Tab | Explains and plans. Asks before changing anything. |

### Do it the right way

**1. Switch to Plan** (Tab until the corner shows plan).

```
How do I add a countdown timer to each question in this quiz app? Read the existing
components first, then give me a plan and the files you would touch. Don't write any
code yet.
```

**2. Push back.**

```
Step 3 looks risky — what happens if the tab is closed mid-question? Redo the plan
with that handled.
```

**3. Switch to Build** (Tab again).

```
Good plan. Go ahead and make the changes.
```

Planning costs one extra message and saves you from undoing a wrong turn.

### Subagents — a second pair of eyes

Type `@` to see them. Use them for big jobs, not one-line edits.

| Type | Type this | Good for |
|------|-----------|----------|
| **explore** | `@explore Where is the score calculated?` | Finding things. Read-only. |
| **general** | `@general Audit all components for accessibility` | Bigger jobs that need focus |

```
@explore Find every place a Pusher channel is subscribed or triggered. Give me file
paths and line numbers.
```

It searches in a fresh, narrow space and brings back only the answer — your chat
stays clean.

**Don't** chain `explore` → `plan` → `build` → review on one small task. That's how a
30-second job becomes a slow, expensive one.

---

## 5. `AGENTS.md`

One file, in your project root. OpenCode reads it before every task. It's why you
stop repeating yourself.

### The five fields

```
[APP_NAME]. What your app is called.

[ONE_LINE_DESCRIPTION]. A single sentence on what the app does.

[FEATURE_LIST]. Three to seven core features, as a bulleted list.

[EXAMPLE_COMPONENT_NAMES]. Two or three real components from your app.

[EXAMPLE_STATE_FIELDS]. Two or three pieces of state your app needs.
```

Three to seven features. Real component names. Real state fields. Nothing invented —
if the agent makes up a filename that doesn't exist, you get the wrong answer.

### Filled in

```markdown
# Live Quiz

A real-time multiplayer quiz where teams join a lobby, answer multiple-choice
questions, and watch a live leaderboard update instantly.

## Features
- Team lobby: players enter a team name and pick an avatar
- Multiple-choice question view with four choices (A, B, C, D)
- Host panel to start the quiz, advance questions, and end the game
- Live leaderboard that reorders the moment a score changes
- Score sync across every device, no refresh
- Mobile-first layout that works on a phone

## Components
- `src/components/TeamJoinScreen.tsx` — the lobby form
- `src/components/LiveLeaderboard.tsx` — the ranked team list
- `src/components/HostControlPanel.tsx` — host-only controls

## State
- `teams: Team[]` — `{ id, name, avatar, score }`
- `currentQuestion: Question | null` — the question on screen now
- `gameState: 'lobby' | 'question' | 'results'` — which screen is showing
```

### Have OpenCode write it

```
Read this project and write AGENTS.md at the root using this template:

[APP_NAME]. What your app is called.
[ONE_LINE_DESCRIPTION]. A single sentence on what the app does.
[FEATURE_LIST]. Three to seven core features, as a bulleted list.
[EXAMPLE_COMPONENT_NAMES]. Two or three real components from your app.
[EXAMPLE_STATE_FIELDS]. Two or three pieces of state your app needs.

Read the real files first. Every component and state field must already exist in
the repo — no placeholders. Keep it under 60 lines.
```

Then check it: open those three files. If the names aren't real, fix them.

### Add the working rules

The five fields say *what the app is*. Add *how to work in it*:

```markdown
## Commands
- Install: npm install
- Dev: npm run dev  (http://localhost:5173)
- Check: npx tsc --noEmit
- Build: npm run build

## Conventions
- TypeScript strict mode. No `any`.
- One component per file, PascalCase filenames.
- Tailwind classes only. No hardcoded hex colours — use the theme tokens.

## Never
- Don't restructure the files named above.
- Don't commit .env files.
```

Commit it. Your future self and your teammates get the same rules.

---

## 6. Build the quiz app — 10 steps

Build a live quiz: teams join a lobby, answer questions, and a leaderboard updates
in real time. Commit after every step.

| Step | What | Prompt needed? |
|------|------|----------------|
| 1 | Generate the app | Yes |
| 2 | Apply a design | Yes |
| 3 | Save files locally | No |
| 4 | Run it | No |
| 5 | Team join form | Yes |
| 6 | Live scores | Yes |
| 7 | Test it | Yes |
| 8 | Polish | Yes |
| 9 | Push to GitHub | No |
| 10 | Deploy | No |

Every prompt from here follows the same three-part shape. Learn it once:

```
Read AGENTS.md first. In <exact file>, <one change>. Don't touch anything else.
```

---

### Step 1 — Generate the app

Open **https://aistudio.google.com** and paste:

```
Act as a web developer. Make a working starting setup for a React + TypeScript +
Tailwind CSS Live Quiz WebApp.

Please include:
- A clean folder structure (components, store, assets, types).
- An AGENTS.md file at the root listing project rules, color theme, and app logic.
- A simple list of hardcoded temporary multiple-choice questions.
- Core working screens: Join Lobby, Live Leaderboard, Question View (showing
  multiple-choice questions with choices A, B, C, D), and Host Control Panel.
```

**Check:** all four screens render in the preview. The folder structure matters —
every later step names a path.

### Step 2 — Apply a design

Upload 2–3 reference screenshots, then:

```
Keep all generated features, but update the styling so the buttons, dark background,
and overall layout match these design images.
```

**Check:** the preview now looks like your references. If AI Studio ignores the
images, be specific instead — name the exact colours:

```
Keep every feature. Use this palette: background #0F1115, card #1A1D23, accent
#A3B18A, text #F2F1EF, muted #A3A39B. Rounded buttons (8px radius, full pill on
buttons). 16px body text. Dark theme only, 4.5:1 contrast. Put these in one theme
file and use the tokens everywhere — no hex codes inside components.
```

Do this now, while the code is still small.

### Step 3 — Save the files locally

No prompt — this is copy and paste.

1. Download from AI Studio and unzip to `projects/live-quiz-app`.
2. **Check for the double-folder mistake:** you want
   `live-quiz-app/index.html`, not `live-quiz-app/live-quiz-app/index.html`.
3. Create `.gitignore`:

```
node_modules/
dist/
.env
.env.local
.vercel
*.log
```

**Check:** `AGENTS.md`, `src/components/`, `src/data/questions.json` and
`src/store/` all sit directly inside the folder. Then commit.

### Step 4 — Run it

In OpenCode's chat:

```
Read AGENTS.md first. Install the dependencies and start the dev server so the app
runs on my machine. Don't change any code.
```

Or in a terminal: `npm install` then `npm run dev`.

**Check:** http://localhost:5173 loads and you can move between screens.

**If it's blank:** ask OpenCode to read the browser console and fix the error. Don't
paste the error here — let it find the file.

### Step 5 — Team join form

```
Read AGENTS.md first. In TeamJoinScreen.tsx, build a form where players can type
their team name and select an avatar. When submitted, add the team to the lobby
list. Do not alter any existing screen layout.
```

**Check:** type a name, click **Join Game**, the team appears in the lobby list.

**Also try:** an empty name (should be blocked) and a very long one (shouldn't break
the layout).

### Step 6 — Live scores

Without this, the leaderboard only updates on refresh. We'll use **Pusher** — the
server sends one event and every screen updates instantly.

**One-time setup:**

1. Sign up at **https://dashboard.pusher.com** and create a Channels app.
2. Copy the app id, key, secret and cluster.
3. Put them in a `.env.local` file in your project (already gitignored):

```
PUSHER_APP_ID=your-app-id
PUSHER_KEY=your-key
PUSHER_SECRET=your-secret
PUSHER_CLUSTER=us2
```

**The secret stays on the server. Never put it in the browser.**

**Then the prompt:**

```
Read AGENTS.md first. Connect Pusher to the app — trigger the score event from
api/leaderboard.js and subscribe to the quiz-score channel with pusher-js in
LiveLeaderboard.tsx — so a correct answer updates the host panel and every player
view without refreshing. Read the four PUSHER_ variables from the environment; the
secret must only be used server-side.
```

**Check:** open two browser tabs side by side. Answer in tab 1. Tab 2 updates
instantly, no refresh.

### Step 7 — Test it

```
Read AGENTS.md first. In TeamJoinScreen.tsx, players can click the submit button
twice quickly. Add a simple check to disable the join button immediately after the
first click.
```

**Check:** click fast — one team only. And make sure the button comes back if the
request fails, so the form never gets stuck.

Re-run the step 5 tests too. Step 6 changed state, so yesterday's results don't hold.

### Step 8 — Polish

```
Read AGENTS.md first. Update LiveLeaderboard.tsx so that score bars grow smoothly
using CSS transitions whenever team points change. Make sure answer choices look
clear on small mobile screens.
```

**Check:** trigger a score — the bars slide, they don't jump. Then narrow the browser
window to phone width and check nothing overlaps.

The short list: bars animate over ~500ms · 16px side padding on mobile · answer
buttons at least 44px tall · text readable on the dark background.

### Step 9 — Push to GitHub

In a terminal, inside the project folder:

```bash
git add .
git commit -m "feat: complete quiz app"
git branch -M main
git remote add origin https://github.com/<YOUR-USERNAME>/live-quiz-app.git
git push -u origin main
```

**Check:** open your GitHub profile. Your files, including `AGENTS.md`, are on
`main`. Confirm no `.env` file went up — if one did, remove it and change the key.

### Step 10 — Deploy

1. Go to **https://vercel.com** → **Add New → Project** → import your repo.
2. Framework: **Vite**. Build `npm run build`. Output `dist`.
3. **Environment Variables** → add all four Pusher keys.

**That step 3 is the one people forget.** The app works on your machine and breaks
online, because the server there can't see your `.env.local`.

**Check:** open the live URL **on your phone**. Join a team, answer a question,
watch the leaderboard move.

---

### Ship checklist

- [ ] `AGENTS.md` is accurate and committed
- [ ] All four screens work
- [ ] Joining a team works and can't double-submit
- [ ] Leaderboard updates with no refresh
- [ ] Works on a phone
- [ ] No secrets committed
- [ ] Live URL works

---

## If something goes wrong

| Problem | Fix |
|---------|-----|
| OpenCode won't open the folder | Reinstall from opencode.ai/download |
| No treg tools | You didn't restart. Quit and reopen the app. |
| treg says 401 | The key is wrong. Get a new one and set it up again. |
| treg says 402 | Out of credit. Add funds in the treg dashboard. |
| The installer failed on Windows | The one-liner needs a POSIX shell. Ask OpenCode to register treg as an MCP server directly, or run it in WSL. |
| Skill not listed | You didn't restart, or the file isn't `SKILL.md` with `name` + `description` |
| `/skill-name` doesn't work | Skills aren't slash commands. Name the skill in your message instead. |
| The agent ignores `AGENTS.md` | The rule is buried or contradicted. Move it to the top. |
| The AI made a mess | `/undo`, then re-ask with a clearer instruction. |

---

**Links:** opencode.ai/download · opencode.ai/docs · agenticskills.io/skills ·
treg.to · aistudio.google.com · dashboard.pusher.com · vercel.com
