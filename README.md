# 📚BSITOUMN 1-A — Group Repository Guide

Welcome! This organization is where every **group** in our section keeps its project code. Each group gets **its own repository** here. This guide shows you, step by step, how to:

1. Join the organization
2. Create your group's repository
3. Clone it into VS Code
4. Commit and push your work
5. Collaborate with your groupmates remotely

> 💡 Replace anything written like `<ORG-NAME>` with the real name of our organization.

---

## 🧰 Before You Start (One-Time Setup)

Every member needs these installed:

| Tool | Download | Check it works |
|------|----------|----------------|
| **Git** | https://git-scm.com/downloads | `git --version` |
| **VS Code** | https://code.visualstudio.com | Open the app |
| **GitHub account** | https://github.com/signup | Log in on github.com |

### Tell Git who you are (only once per computer)

Open a terminal (in VS Code: **Terminal → New Terminal**) and run:

```bash
git config --global user.name "Your Full Name"
git config --global user.email "the-email-you-used-on-github@example.com"
```

---

## Step 1 — Join the Organization

1. Check your email (or go to https://github.com/settings/organizations) for the **invitation** to `<ORG-NAME>`.
2. Click **Accept invitation**.
3. Confirm you can see the organization at `https://github.com/<ORG-NAME>`.

> Didn't get an invite? Send your **GitHub username** to the organization owner.

---

## Step 2 — Create Your Group's Repository

> ⚠️ **Only ONE person per group** (the group leader) does this step. Everyone else skips to Step 3.

1. Go to `https://github.com/<ORG-NAME>`.
2. Click the **Repositories** tab → **New repository** (green button).
3. Fill in the form:
   - **Owner:** `<ORG-NAME>` (make sure it's the organization, *not* your personal account)
   - **Repository name:** use this format → `group-<number>-<project-name>`
     Example: `group-3-inventory-system`
   - **Description:** short summary of your project
   - **Visibility:** choose what the instructor asked for (Private is recommended)
   - ✅ Check **Add a README file**
   - ✅ (Optional) Add a **.gitignore** template — pick **Node** if you use JavaScript/Node.js
4. Click **Create repository**.

### Add your groupmates

1. Inside your new repo, go to **Settings → Collaborators and teams**.
2. Click **Add people**.
3. Type each groupmate's GitHub username and send the invite.
4. Set their role to **Write** so they can push code.

Groupmates must **accept the invitation** (check email or GitHub notifications) before they can push.

---

## Step 3 — Clone the Repository into VS Code

Every member (including the leader) does this **once**.

### Option A: Using VS Code (easiest)

1. Open the repository page on GitHub and click the green **Code** button.
2. Copy the **HTTPS** URL, e.g. `https://github.com/<ORG-NAME>/group-3-inventory-system.git`
3. Open **VS Code**.
4. Press `Ctrl + Shift + P` (Mac: `Cmd + Shift + P`) to open the Command Palette.
5. Type **Git: Clone** and press Enter.
6. Paste the URL and press Enter.
7. Choose a folder on your computer to save it in.
8. When asked **"Would you like to open the cloned repository?"** click **Open**.
9. If a browser window pops up asking you to sign in to GitHub, click **Authorize**.

### Option B: Using the terminal

```bash
cd path/to/your/projects-folder
git clone https://github.com/<ORG-NAME>/group-3-inventory-system.git
cd group-3-inventory-system
code .
```

✅ You now have a full copy of the project on your computer.

---

## Step 4 — Daily Workflow: Pull → Work → Commit → Push

Follow this loop **every time** you work on the project.

### 4.1 Pull first (get your groupmates' latest work)

Always do this **before you start coding**:

```bash
git pull
```

In VS Code: click the **Source Control** icon (left sidebar) → click the **⋯** menu → **Pull**.

### 4.2 Do your work

Edit, add, or delete files as needed.

### 4.3 Stage and commit your changes

**Using VS Code:**

1. Open **Source Control** (`Ctrl + Shift + G`).
2. You'll see a list of changed files. Click the **+** beside a file to stage it (or **+** next to "Changes" to stage all).
3. Type a clear message in the box, e.g. `Add login form`.
4. Click **✓ Commit**.

**Using the terminal:**

```bash
git add .
git commit -m "Add login form"
```

### 4.3 Push to GitHub

**VS Code:** click **Sync Changes** (or **Push**) in the Source Control panel.

**Terminal:**

```bash
git push
```

Refresh the repo page on GitHub — your changes are now online for the whole group. 🎉

### ✍️ Writing good commit messages

| ❌ Bad | ✅ Good |
|-------|--------|
| `update` | `Fix navbar overlap on mobile` |
| `asdf` | `Add student registration page` |
| `final final v2` | `Connect form to database` |

---

## Step 5 — Collaborating Remotely

### ⚡ About "real-time" collaboration

Git and GitHub are **not** real-time like Google Docs. Instead, each person works on their own copy, then shares changes by **pushing** and **pulling**. The more often you commit, push, and pull, the closer to "real-time" you get.

**Good habits:**
- 🔄 **Pull before you start** working
- 💾 **Commit small and often** (after each finished task)
- ⬆️ **Push at least at the end of every work session**
- 💬 **Tell your group** in your chat when you push big changes

### Option 1 (Recommended): Use branches

Branches let each person work without breaking each other's code.

```bash
# Create and switch to your own branch
git checkout -b feature/login-page

# ...work, commit as usual...
git add .
git commit -m "Add login page"

# Push your branch to GitHub
git push -u origin feature/login-page
```

Then on GitHub:

1. Click **Compare & pull request** (yellow banner on the repo page).
2. Write what you changed.
3. Ask a groupmate to review it.
4. Click **Merge pull request** once approved.
5. Everyone runs `git checkout main` then `git pull` to get the merged update.

**Branch naming ideas:** `feature/login`, `fix/navbar-bug`, `docs/update-readme`

### Option 2: Everyone works on `main` (simple, but riskier)

Fine for small groups, as long as everyone **pulls before every push**:

```bash
git pull
git add .
git commit -m "Your message"
git push
```

### Option 3: Live coding together with VS Code Live Share

For actual real-time editing (like Google Docs, but for code):

1. In VS Code, open **Extensions** (`Ctrl + Shift + X`).
2. Search for **Live Share** (by Microsoft) and install it.
3. Click **Live Share** in the status bar and sign in with GitHub.
4. Click **Share** and send the generated link to your groupmate.
5. They open the link and can edit your code live, even from another location.

> Live Share is great for pair programming and debugging calls. Still **commit and push** afterward. Live Share doesn't save to GitHub by itself!

---

## 🔥 Fixing Common Problems

### "Merge conflict" 😱

This happens when two people edit the **same lines** of the same file.

1. VS Code will highlight the conflict with options: **Accept Current Change**, **Accept Incoming Change**, **Accept Both Changes**.
2. Talk to your groupmate to decide which code to keep.
3. Save the file, then:

```bash
git add .
git commit -m "Resolve merge conflict in login.js"
git push
```

### "Push rejected / failed to push"

Someone pushed before you. Pull first, then push again:

```bash
git pull
git push
```

### "Permission denied" or "Repository not found"

- Make sure you **accepted** the collaborator invitation.
- Make sure you're logged in to the **right GitHub account** in VS Code.
- Ask the group leader to confirm you have **Write** access.

### "Authentication failed"

- In VS Code, click the **Accounts** icon (bottom-left) → **Sign out** → sign in again with GitHub.
- GitHub no longer accepts account passwords for Git. Use the browser sign-in popup or a **Personal Access Token**.

### I accidentally committed the wrong file

Don't panic! Message your group or instructor **before** pushing again. For files that shouldn't be shared (passwords, `.env`), tell your leader right away.

---

## ✅ Rules for Our Organization

1. **One repo per group.** Follow the naming format `group-<number>-<project-name>`.
2. **Never commit secrets** — passwords, API keys, `.env` files. Add them to `.gitignore`.
3. **Never commit `node_modules/`** — it's huge. Use a `.gitignore` and run `npm install` instead.
4. **Pull before you push.** Always.
5. **Write clear commit messages.**
6. **Everyone must contribute commits.** Your commit history shows your participation.
7. **Don't delete or edit other groups' repositories.**
8. **Ask for help early** — don't wait until the deadline.

---

## 🧾 Quick Command Cheat Sheet

| What you want to do | Command |
|---------------------|---------|
| Copy a repo to your PC | `git clone <url>` |
| See what changed | `git status` |
| Get latest changes | `git pull` |
| Stage all changes | `git add .` |
| Save a snapshot | `git commit -m "message"` |
| Upload to GitHub | `git push` |
| Create a new branch | `git checkout -b branch-name` |
| Switch branch | `git checkout branch-name` |
| See commit history | `git log --oneline` |

---

## 🙋 Need Help?

- Ask your **group leader** first.
- Then post in our **section group chat**.
- Still stuck? Contact the **organization owner / instructor**.

Happy coding! 🚀
