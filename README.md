# GitHub for ADO Developers — Demo Script

## Session Setup

- **Presenters**: Presenter A and Kevin M  
- **Demo Repo**: https://github.com/yortch/ (pick or create a repo like `github-ado-workshop`)
- **ADO Reference**: https://dev.azure.com/octodemo-msft/msft-common-demos-adogh-crispy-carnival/
- **Duration**: 90 minutes total
- **Pre-requisites**: Both presenters have GitHub accounts, repo write access, a simple project with a few files (e.g., a README, an app file, and a config file)

---

## Section 1: GitHub Fundamentals & Enterprise Setup (25 min)

### Demo 1.1 — GitHub UI Walkthrough (Presenter A, 10 min)

**Goal**: Orient ADO users to the GitHub interface by showing equivalent features.

1. **Open the demo repo** at `https://github.com/yortch/github-for-ado`
2. **Code tab tour**:
   - Show the file browser, branch dropdown, "Go to file" search
   - Click into a file → show the Raw, Blame, History buttons
   - Compare: "In ADO this is Repos > Files"
3. **Issues tab**:
   - Click on Projects tab
   - Show unrelated project: https://github.com/users/yortch/projects/3
   - Compare: In ADO this is a board
   - Go back to demo repo.
   - Show issue list (remove open filter), labels, milestones
   - Create a quick issue: "Add contributing guidelines"
   - Assign to Presenter B, add label `documentation`
   - Compare: "In ADO this is Boards > Work Items"
4. **Pull Requests tab**:
   - Show open/closed PRs, filters
   - Compare: "In ADO this is Repos > Pull Requests"
5. **Actions tab**:
   - Show any existing workflow run (or show the starter workflow UI)
   - Compare: "In ADO this is Pipelines"
6. **Settings → Branches**:
   - Show branch protection rules
   - Compare: "In ADO this is Project Settings > Repos > Policies"

### Demo 1.2 — Organization & Teams (Presenter A, 5 min)

1. Navigate to **Organizations** (from User profile - top right corner)
2. Click on MSFT-Demos organization
2. Click the **Teams** tab → how teams are created and assigned repos
3. Show a team's **Members** and **Repositories** sub-tabs
4. Explain: "Unlike ADO where teams are per-project, GitHub teams span all repos"

### Demo 1.3 — ADO Side-by-Side (Presenter B, 10 min)

1. **Open ADO** at `https://dev.azure.com/octodemo-msft/msft-common-demos-adogh-crispy-carnival/_git/adogh-crispy-carnival-migrate` (optional)
2. Walk through the same concepts:
   - Repos > Files (compare to Code tab)
   - Repos > Pull Requests (compare to PR tab)
   - Pipelines (compare to Actions)
   - Project Settings > Repos > Branch Policies (compare to branch protection)
3. **Key callout**: "ADO has Projects as the boundary; GitHub uses Organizations"
4. **Key callout**: "ADO branch policies are per-branch per-repo; GitHub branch protection rules support pattern matching (e.g., `release/*`)"

---

## Section 2: Working in GitHub for ADO Developers (35 min)

### Demo 2.1 — The GitHub Flow: Branch, Edit, PR (Presenter A, 12 min)

**Goal**: Show the complete GitHub Flow from the browser — no local clone needed.

1. **Create a branch from the UI**:
   - Go to Code tab → branch dropdown → type `feature/add-contributing` → "Create branch"
   - Compare: "In ADO you'd create a branch from the branch dropdown too, or link it to a work item"

2. **Edit a file in the browser**:
   - Click `README.md` → pencil icon → make a small edit
   - Show the commit message dialog → commit to the feature branch
   - Compare: "ADO has a similar web editor, but watch this..."

3. **Open github.dev**:
   - Press `.` (period) on the repo page
   - Show the full VS Code interface in the browser
   - Make an edit, stage, commit using the Source Control panel
   - **Key callout**: "This is unique to GitHub — a full IDE with no setup!"

4. **Create a Pull Request**:
   - Go back to the repo → notice the "Compare & pull request" banner
   - Click it → fill in title, add description referencing `Fixes #1`
   - Assign Presenter B as reviewer
   - **Key callout**: "The issue will auto-close when this PR merges"

### Demo 2.2 — Forks & InnerSource (Presenter B, 8 min)

**Goal**: Show the fork-based contribution model unique to GitHub.

1. **Fork the repo**:
   - From Presenter B's account, click "Fork" on the demo repo
   - Show that it creates a copy under Presenter B's namespace

2. **Make changes on the fork**:
   - Edit a file directly on the fork (e.g., add a new file `CONTRIBUTORS.md`)
   - Commit to main on the fork

3. **Create a cross-fork PR**:
   - Click "Contribute" → "Open pull request"
   - Show the PR targets the upstream repo from the fork
   - **Key callout**: "This is InnerSource — you contributed without needing write access to the original repo. ADO has no equivalent."

4. **Presenter A receives the PR**:
   - Switch to Presenter A's screen showing the incoming PR from a fork

### Demo 2.3 — History, Blame, and Permalinks (Presenter A, 5 min)

1. Navigate to any file in the repo
2. Click **Blame** → show line-by-line attribution
   - Click a commit SHA to see the full diff
3. Click **History** → show the commit log for that specific file
4. **Create a permalink**:
   - Click a line number → the URL updates with `#L15`
   - Press `Y` → URL changes to include the commit SHA (permanent link)
   - **Key callout**: "Share this link in Slack/Teams — it'll always point to that exact version"

---

## Section 3: Pull Requests & Code Review (30 min)

### Demo 3.1 — PR Templates & Creating a PR (Presenter A, 5 min)

1. **Show/create a PR template**:
   - Create a branch named: `pr-template`
   - Navigate to `.github/PULL_REQUEST_TEMPLATE.md` (create if not exists)
   - Show the markdown template with checklist items:
     ```markdown
     ## Description
     <!-- What does this PR do? -->
     
     ## Checklist
     - [ ] Tests pass
     - [ ] Documentation updated
     - [ ] No breaking changes
     
     ## Related Issues
     Fixes #
     ```
   - **Key callout**: "Every new PR auto-populates with this template"

2. **Create a new PR** → show the template pre-filling the description

### Demo 3.2 — Branch Protection & CODEOWNERS (Presenter A, 5 min)

1. **Show branch protection settings**:
   - Settings → Branches → main rule
   - Toggle: "Require a pull request before merging"
   - Toggle: "Require approvals" → set to 1
   - Toggle: "Require status checks to pass" → select a check
   - Toggle: "Require review from Code Owners"
   
2. **Show CODEOWNERS file**:
   - Open `.github/CODEOWNERS`
   - Show examples:
     ```
     * @yortch
     docs/ @kevinkmanu
     ```
   - **Key callout**: "This auto-assigns reviewers based on what files are changed. ADO has 'Required reviewers' on policies, but CODEOWNERS is more granular."

3. **Try to merge without approval** → show the blocked state


### Demo 3.3 — Merge Strategies & Conflict Resolution (Presenter B, 10 min)

**Goal**: Show all three merge strategies and resolve a conflict in the browser.

**Setup** (pre-prepared): Have a PR ready that has a conflict.

1. **Show merge strategy dropdown** on a PR that's ready to merge:
   - "Create a merge commit" (default)
   - "Squash and merge" (combines all commits)
   - "Rebase and merge" (replays on top of main)
   - Compare: "ADO calls these 'Merge', 'Squash', 'Rebase' in the Complete dialog"

2. **Create a conflict** (live or pre-staged):
   - Both presenters edit the same line of the same file on different branches
   - Open a PR → GitHub shows "This branch has conflicts that must be resolved"
   - Use: https://github.com/yortch/github-for-ado/pull/2

3. **Resolve in the web editor**:
   - Click "Resolve conflicts" button
   - Show the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`)
   - Edit to resolve → "Mark as resolved" → "Commit merge"
   - **Key callout**: "Simple conflicts can be resolved entirely in the browser — no local checkout needed"

### Demo 3.4 — Code Review: Two Presenters Collaborate (Both, 15 min)

**This is the highlight demo — shows real collaboration.**

**Presenter A creates a PR:**
1. Push a branch with a code change (e.g., add a function with a minor issue)
2. Open PR, request review from Presenter B

**Presenter B reviews:**
3. Go to "Files changed" tab
4. **Add a line comment**: hover over a line → click `+` → write feedback
5. **Use "Suggest changes"**: click the ± icon in the comment box → write corrected code
6. **Start a review** (batch multiple comments)
7. Click "Review changes" → choose "Request changes" → submit

**Presenter A responds:**
8. View the review comments in "Conversation" tab
9. **Accept a suggested change** with one click → "Commit suggestion"
10. **Resolve conversations** after addressing

**Presenter B approves:**
11. Review the updates → "Approve"
12. **Key callout**: "Notice the green checkmark"


---

## Closing (5 min)

### Wrap-up Discussion Points

- "What ADO workflows are you most concerned about replicating in GitHub?"
- "Any features you saw today that you want to explore further?"

### Resources to Share

- Training manual: https://githubtraining.github.io/training-manual
- GitHub Skills (hands-on labs): https://skills.github.com
- GitHub Docs: https://docs.github.com
- MS Learn GitHub Path: https://learn.microsoft.com/training/github

---

## Pre-Session Preparation Checklist

- [ ] Create or select demo repo at github.com/yortch/
- [ ] Ensure both presenters have write access
- [ ] Create `.github/PULL_REQUEST_TEMPLATE.md` with sample template
- [ ] Create `.github/CODEOWNERS` with sample entries
- [ ] Set up at least one branch protection rule on `main`
- [ ] Create a simple GitHub Actions workflow (e.g., linting or echo)
- [ ] Pre-create an issue for the demo ("Add contributing guidelines")
- [ ] Pre-stage a conflict scenario (two branches editing same line)
- [ ] Have ADO repo open in a browser tab for comparison
- [ ] Test github.dev (press `.`) works from your network
- [ ] Ensure both presenters are logged into GitHub
- [ ] Prepare one branch with a code change ready for the review demo

---

## Timing Guide

| Section | Duration | Presenter |
|---------|----------|-----------|
| 1.1 GitHub UI Walkthrough | 10 min | A |
| 1.2 Organization & Teams | 5 min | A |
| 1.3 ADO Side-by-Side | 10 min | B |
| 2.1 GitHub Flow (branch, edit, PR) | 12 min | A |
| 2.2 Forks & InnerSource | 8 min | B |
| 2.3 History, Blame, Permalinks | 5 min | A |
| 2.4 Merge Strategies & Conflicts | 10 min | B |
| 3.1 PR Templates | 5 min | A |
| 3.2 Code Review Collaboration | 15 min | Both |
| 3.3 Branch Protection & CODEOWNERS | 5 min | A |
| 3.4 Status Checks & Auto-Merge | 5 min | B |
| **Total** | **90 min** | |
