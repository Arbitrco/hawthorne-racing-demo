# Build Your Cortex

This guide allows you to setup a Cortex.

There are three types of setup:

- **Path A: Build from scratch.** You're starting clean and designing your organisations structure.
- **Path B: Start from the template.** You copy the Hawthorne Racing demo Cortex and adjust it to your own content.
- **Path C: Join an existing Cortex.** Your organisation already has one and you need it on your machine.

Everyone does Part 1 (the tools) and Part 4 (wiring in Claude Code). Parts 2 and 3 depend on your path. Follow the steps in order. Don't skip ahead.

---

# Part 1: Install the Tools

You'll do this once per machine. If you already have Git or Node.js, skip those steps.

## Step 1: Install Git

Git tracks every change to every file in your Cortex. It's what turns a pile of documents into an asset with a history.

1. Go to https://git-scm.com/download/win
2. Download the installer and run it
3. Click Next through everything. Use the default settings.
4. When it asks about the default editor, pick whatever you want (Notepad is fine)
5. When it asks about PATH, pick "Git from the command line and also from 3rd-party software"
6. Finish the install
7. Open a new Command Prompt or PowerShell and type:

```
git --version
```

You should see something like `git version 2.44.0`. If you do, Git is installed.

## Step 2: Install Node.js

Node.js runs Claude Code. You need version 18 or higher.

1. Go to https://nodejs.org
2. Download the LTS version (the big green button)
3. Run the installer. Use default settings.
4. Close and reopen your terminal
5. Verify:

```
node --version
```

You should see `v20` or higher.

Also check npm (it comes with Node):

```
npm --version
```

You should see a version number. Both working means you're good.

## Step 3: Install Python

Python runs graphify, which indexes your Cortex into a knowledge graph so Claude doesn't have to read every file every session.

1. Go to https://www.python.org/downloads/
2. Download the latest version
3. **Important:** On the first screen of the installer, check the box that says "Add python.exe to PATH"
4. Click Install Now
5. Close and reopen your terminal
6. Verify:

```
python --version
```

## Step 4: Install Claude Code

Open your terminal and run:

```
npm install -g @anthropic-ai/claude-code
```

Wait for it to finish. Then verify:

```
claude --version
```

You should see a version number. Claude Code is installed.

## Step 5: Get a GitHub account

Your Cortex lives on GitHub. That's what makes it shared, backed up, and available on every machine you work from.

1. Go to https://github.com/signup and create a free account (skip this if you have one)
2. Use your work email if this Cortex belongs to your organisation

That's the tooling done. Now the interesting part.

---

# Part 2: Design the Structure with the AI Strategy Canvas

Before you create a single folder, fill in the AI Strategy Canvas (the nine-block model from INGRAIN AI). If you attended the session, you've already done a first pass. If not, block out 45 minutes with the people who know the business best.

The canvas asks nine questions:

1. **Target Audience.** Who do you serve?
2. **Company.** Who are you?
3. **Products/Services.** What do you offer?
4. **Context.** What's going on right now that the AI needs to know?
5. **Role.** What job should the AI play?
6. **Style/Brand Voice.** How do you sound?
7. **Resources.** What source material exists?
8. **Rules.** What must the AI always and never do?
9. **Request.** What tasks will you actually run?

Here's the reframe that matters: the canvas isn't a workshop artefact. It's a schema. Every block you filled in becomes a home in your folder tree. The canvas stops being a poster and becomes a directory.

## The block-to-folder map

| Canvas block | Where it lives in the Cortex |
|---|---|
| Company | `company/profile.md`, `company/divisions.md` |
| Products/Services | `company/offerings.md` |
| Target Audience | `clients/` (one file per client or segment) |
| Context | `processes/` and `decisions/` |
| Role | `CLAUDE.md` (top section) |
| Style/Brand Voice | `company/brand-voice.md` |
| Resources | The whole repo, plus `resources/` for source documents |
| Rules | `CLAUDE.md` (rules section) |
| Request | `skills/` (one folder per repeatable task) |

## The reference tree

This is the shape, using Hawthorne Racing (a fictional F1 constructor) as the worked example:

```
hawthorne-racing/
  CLAUDE.md
  01-global/
    01-context/
    02-skills/
    03-data/
    04-automations/
    05-deliverables/
  02-workspaces/
    01-commercial/
      01-context/
      02-skills/
      03-data/
      04-automations/
      05-deliverables/
    02-race-operations
      01-context/
      02-skills/
      03-data/
      04-automations/
      05-deliverables/
  03-personal/
  


```

Swap `01-commercial/` for `clients/`, `suppliers/`, or whatever your business actually finds as the best dimension to segment workspaces by. The names should be boring and predictable. Boring names beat clever ones, because your newest hire and your AI agent both need to guess where things live.

Two files deserve a special mention:

- **README.md** is the front door for humans. What this Cortex is, who owns it, how to contribute.
- **CLAUDE.md** is the front door for the AI. It holds the Role and Rules blocks, and tells Claude how to behave inside this repo. Claude Code reads it automatically at the start of every session.

The Cortex will evolve over time and you will not get it right on the first pass, get the basics of context setup and then begin shifting your team into working from the cortex as their primary interface with their GenAI tool.

---

# Part 3: Choose Your Path

## Path A: Build your Cortex from scratch

Use this if you're designing your own structure from your canvas.

### A1. Create the folder

Give it a name with no spaces:

```
mkdir C:\Users\%USERNAME%\YourCortexName
```

### A2. Initialise Git

```
cd C:\Users\%USERNAME%\YourCortexName
git init
```

### A3. Build the skeleton from your canvas

Create the folders your block-to-folder map calls for. In your terminal:

```
mkdir strategy company clients processes decisions skills
```

Then create your first two files. In Notepad or any editor:

- `README.md` with three lines: what this Cortex is, who owns it, how to contribute
- `CLAUDE.md` with your Role and Rules blocks written out in plain sentences

Drop your completed canvas into `strategy/ai-strategy-canvas.md`. Then write one real file in `company/`. Your profile, in plain language, the way you'd brief a new starter.

### A4. First commit

```
git add -A
git commit -m "Initial Cortex structure from AI Strategy Canvas"
```

### A5. Put it on GitHub

1. Go to https://github.com/new
2. Name the repository the same as your folder
3. Set it to **Private**
4. **Do not** tick "Add a README", "Add .gitignore", or "Choose a license". The repo must be empty.
5. Click Create repository
6. Back in your terminal:

```
git remote add origin https://github.com/YOUR-USERNAME/YourCortexName.git
git branch -M main
git push -u origin main
```

Replace `YOUR-USERNAME` with your GitHub username or organisation. The first push opens a browser window asking you to sign in. Approve it and the push completes.

Refresh the repo page on GitHub. Your files should be there. Your Cortex now exists in two places, and Git keeps them in sync.

Go to Part 4.

## Path B: Start from the Hawthorne template

Use this if you'd rather refill a proven structure than design your own. The Hawthorne Racing demo Cortex is the same one shown in the session.

**Template repo:** `https://github.com/Arbitrco/hawthorne-racing-demo`

### B1. Copy the template into your own account

1. Open the template repo on GitHub
2. Click the green **Use this template** button, then **Create a new repository**
3. Name it, set it to **Private**, click Create

You now own a full copy with none of the template's history. If the green button says **Code** instead of **Use this template**, use this fallback:

```
cd C:\Users\%USERNAME%
git clone https://github.com/[HAWTHORNE-REPO-URL] YourCortexName
cd YourCortexName
rmdir /s /q .git
git init
git add -A
git commit -m "Initial Cortex from Hawthorne template"
```

Then create an empty private repo on GitHub (as in step A5) and push:

```
git remote add origin https://github.com/YOUR-USERNAME/YourCortexName.git
git branch -M main
git push -u origin main
```

### B2. Pull it to your machine (template button path only)

If you used the template button, the repo exists on GitHub but not on your machine yet:

```
cd C:\Users\%USERNAME%
git clone https://github.com/YOUR-USERNAME/YourCortexName.git
cd YourCortexName
```

### B3. Evict Hawthorne, move yourself in

Work through the tree with your canvas beside you:

1. Rewrite `CLAUDE.md` with your Role and Rules. This one matters most, because Claude reads it every session.
2. Replace `company/profile.md`, `divisions.md`, and `brand-voice.md` with your own
3. Rename `partners/` to whatever fits your business and replace the contents
4. Delete the example decisions and processes, or keep one as a formatting reference
5. Keep the `skills/` folders. Read them before deleting anything; the meeting-decision-analyst skill works for any organisation that holds meetings, which is all of them.
6. Drop your canvas into `strategy/ai-strategy-canvas.md`

Commit as you go:

```
git add -A
git commit -m "Replace Hawthorne content with our own"
git push
```

Go to Part 4.

## Path C: Join an existing Cortex

Use this if your organisation already runs a Cortex and you need it on your machine.

### C1. Get access

Ask the Cortex owner to add you as a collaborator. They do this on GitHub under **Settings, then Collaborators and teams**. You'll get an email invitation. Accept it.

### C2. Clone it

1. Open the repo page on GitHub
2. Click the green **Code** button and copy the HTTPS URL
3. In your terminal:

```
cd C:\Users\%USERNAME%
git clone https://github.com/YOUR-ORG/CortexName.git
cd CortexName
```

The first clone of a private repo asks you to sign in through your browser. Approve it once and you're done.

Verify it worked:

```
git status
```

You should see "On branch main" and "nothing to commit, working tree clean".

### C3. Learn the house rules

Before you change anything:

1. Read `README.md`. It tells you how this Cortex is organised and how to contribute.
2. Read `CLAUDE.md`. It tells you (and the AI) the rules everyone works under.
3. Respect ownership. Folders belong to the teams that maintain them. Update your own team's context freely. Changes to another team's files go through that team's owner first.

### C4. The sync habit

The Cortex only stays shared if everyone follows one rhythm:

```
git pull
```

before you start working, and

```
git add -A
git commit -m "Describe what changed"
git push
```

when you finish. Pull first, push when done. That's the entire discipline. Miss the pull and you'll end up editing stale files; miss the push and your work helps nobody but you.

Go to Part 4.

---

# Part 4: Wire in Claude Code

Everyone does this part, whichever path you took.

## Step 1: Install graphify

graphify builds a knowledge graph of your Cortex so Claude can understand how everything connects without reading every file every time.

```
pip install graphifyy
```

Then run it inside your Cortex:

```
cd C:\Users\%USERNAME%\YourCortexName
python -m graphify .
```

This creates a `graphify-out/` folder with your knowledge graph. Claude Code uses it automatically. Re-run it whenever the structure changes significantly.

## Step 2: Set up terminal aliases

Aliases let you launch Claude Code with a short command from anywhere. You'll use these every day.

- **cr** (Claude Run) launches Claude in full auto mode. This is your daily driver.
- **cs** (Claude Safe) launches Claude with permission prompts so you can review each action before it happens.

1. Open PowerShell (search for "PowerShell" in the Start menu)
2. Type this to create your profile file if it doesn't exist:

```
if (!(Test-Path -Path $PROFILE)) { New-Item -ItemType File -Path $PROFILE -Force }
notepad $PROFILE
```

3. Notepad will open. Paste this at the bottom of the file:

```
function cs {
    Write-Host "Starting Claude (safe mode)..." -ForegroundColor Cyan
    claude
}

function cr {
    Write-Host "Starting Claude (full auto mode)..." -ForegroundColor Yellow
    claude --dangerously-skip-permissions
}
```

4. Save and close Notepad
5. Close PowerShell completely and open a new PowerShell window
6. Test it by typing `cr` and pressing Enter. You should see "Starting Claude (full auto mode)..."

**If you get an error about execution policy**, run this first as Administrator, then close and reopen PowerShell and try again:

```
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```

**What the flag means:** `--dangerously-skip-permissions` tells Claude it can read files, write files, and run commands without asking you first. That's what makes `cr` fast. Only use it in your own Cortex on your own computer. When you're working in a shared Cortex and you're new, start with `cs` until you trust what's happening.

## Step 3: Launch Claude Code for the first time

Navigate to your Cortex and launch Claude in safe mode:

```
cd C:\Users\%USERNAME%\YourCortexName
cs
```

The first time you run it, Claude asks you to authenticate. Follow the prompts in your browser. This only happens once.

Once you see the prompt waiting for input, try this before you exit:

```
Read CLAUDE.md and company/profile.md, then tell me what this organisation does in two sentences.
```

If the answer comes back accurate, your Cortex is alive. The AI just briefed itself from your files. Nobody re-typed anything. Type `/exit` to quit.

---

# The Daily Rhythm

From here, every session looks the same:

1. Open your terminal
2. `cd` into your Cortex
3. `git pull` (if you share the Cortex with others)
4. `cr`
5. Work
6. `git add -A`, `git commit -m "what changed"`, `git push`

The canvas was a cost you paid once for a feeling. The Cortex is an asset that pays out every day, and every session makes it a little richer.

---

# Troubleshooting

**"git is not recognized" or "command not found"**
Close your terminal and open a new one. If still not working, restart your computer. The installer needs a fresh terminal to register.

**"node is not recognized"**
Same fix. Close terminal, open new one. Restart if needed.

**"npm ERR!" during Claude Code install**
Run the terminal as Administrator and try the install again:
```
npm install -g @anthropic-ai/claude-code
```

**"python is not recognized"**
You missed the "Add to PATH" checkbox during install. Reinstall Python and check that box.

**"Permission denied" or "Repository not found" when cloning or pushing**
Either you haven't accepted the collaborator invitation (check your email), or you're signed in to the wrong GitHub account. Run `git config user.email` to see which identity Git is using.

**Push rejected with "fetch first"**
Someone pushed changes since your last pull. Run `git pull`, resolve anything Git flags, then push again. This is the "pull first" habit earning its keep.

**Claude Code asks for an API key**
You need a Claude Pro subscription at claude.ai. Claude Code uses your Pro account, not a separate API key. Follow the authentication prompts.

**graphify fails to install**
Make sure Python is installed and working first (`python --version`). If pip is not found, try `python -m pip install graphifyy`.

---

You're set up. Everything from here happens inside your Cortex.

Questions, or want help designing the structure for your organisation? hello@arbitr.co
