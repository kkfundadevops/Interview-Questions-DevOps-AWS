## Q1. How did you set up version control when starting a new project in your organization?
**Scenario:**  
While starting a new microservices-based project for an eCommerce client, we had to maintain proper version control from Day 1.

**Issue/Need:**  
We wanted to track all developer activities module-wise and prevent code overwrites.

**Concept Used:**  
Git initialization, local repo setup, and first commit.

**Commands & Steps:**
```bash
git init
git config user.name "kkuser"
git config user.email "kkuser@vianth.com"
touch README.md
git add .
git commit -m "Initial commit: Project structure and README"
````

**Project Justification During Interview:**
“In our real project, we started by setting up Git in each microservice module separately. This gave us isolated control over feature development. We added a README in each repo to define the service purpose and onboard developers.”

---

## Q2. Describe a situation where you had to resolve a Git conflict during a merge.

**Scenario:**
Two developers worked on the `user-service` module. One changed the password validation logic; another updated logging in the same function.

**Issue/Need:**
When merging `feature/password-validation` into `develop`, we got a merge conflict in `auth.js`.

**Concept Used:**
Conflict resolution during merge.

**Commands & Steps:**

```bash
git checkout develop
git merge feature/password-validation
# Conflict in auth.js
# Manually edited auth.js
git add auth.js
git commit -m "Resolved merge conflict in auth.js"
```

**Project Justification During Interview:**
“I resolved a real conflict where two teammates had edited the same function differently. I reviewed both changes, merged the logic manually, tested it locally, and committed the resolved code.”

---

## Q3. How did you generate and use SSH keys to connect to GitHub securely in production systems?

**Scenario:**
We had EC2-based automation scripts that interacted with GitHub repos using Git commands.

**Issue/Need:**
Avoid storing GitHub credentials in shell scripts and automate clone/pull operations securely.

**Concept Used:**
SSH key generation and GitHub integration.

**Commands & Steps:**

```bash
ssh-keygen -t ed25519 -C "ec2-github-access"
cat ~/.ssh/id_ed25519.pub
# Added public key in GitHub > Settings > SSH & GPG keys
git clone git@github.com:org-name/repo-name.git
```

**Project Justification During Interview:**
“We used SSH authentication in our automation scripts on Red Hat EC2. This avoided the need for password-based access and made GitHub integration secure.”

---

## Q4. Describe a situation where you used a feature branch and raised a pull request.

**Scenario:**
I was assigned to implement login throttling in `user-service`.

**Issue/Need:**
We follow GitHub flow; all changes must go through PR and review.

**Concept Used:**
Feature branching, pull request, and code review.

**Commands & Steps:**

```bash
git checkout -b feature/login-throttle
# Code changes
git add .
git commit -m "Add login throttle logic"
git push origin feature/login-throttle
# Create PR via GitHub UI
```

**Project Justification During Interview:**
“I created a feature branch named `feature/login-throttle`, implemented the logic, pushed the code, and raised a PR. After peer review and approval, it was merged into `develop`.”

---

## Q5. Explain a time you needed to roll back a faulty commit in Git.

**Scenario:**
One developer pushed an incorrect API key to the repo accidentally.

**Issue/Need:**
Remove sensitive data from Git history.

**Concept Used:**
Git revert and reset (soft, hard), BFG Repo Cleaner (if needed).

**Commands & Steps:**

```bash
git log --oneline
git revert <commit-id>
# Or if it's the last commit:
git reset --hard HEAD~1
```

**Project Justification During Interview:**
“We found a commit that accidentally exposed secrets. We used `git revert` to undo the change safely and later rewrote history in GitHub using force push and secret scanning tools.”

---

## Q6. How did you manage team access securely when using GitHub repositories?

**Scenario:**
Our organization onboarded new developers to work on different microservices like `cart-service`, `order-service`.

**Issue/Need:**
Ensure only the right team members had access to relevant repositories (read/write/maintain).

**Concept Used:**
GitHub repository roles and team permissions.

**Steps Taken:**

* Created teams in GitHub under organization settings.
* Assigned developers to respective microservices.
* Granted role-based permissions (write for developers, admin for leads).

**Project Justification During Interview:**
“In our GitHub organization, we followed least-privilege access. Teams were mapped to specific repos, and developers had write access while only leads and DevOps had admin access.”

---

## Q7. Explain a situation where you used Git tags in production releases.

**Scenario:**
We needed to mark specific commits as production releases for rollback and traceability.

**Issue/Need:**
Identify stable builds in Git history for deployments.

**Concept Used:**
Git lightweight/annotated tags.

**Commands & Steps:**

```bash
git tag -a v1.0.0 -m "Release for Prod June 2025"
git push origin v1.0.0
```

**Project Justification During Interview:**
“We used annotated tags to mark production-ready commits. It helped our CI/CD pipelines deploy specific versions and allowed easy rollbacks during hotfixes.”


## Q8. Share your experience of forking a public repository and customizing it for internal use.
**Scenario:**  
We wanted to use an open-source Helm chart from Bitnami and customize it for our Kubernetes setup.

**Issue/Need:**  
Customize and manage our version without affecting upstream changes.

**Concept Used:**  
Forking and periodic syncing with upstream.

**Steps Taken:**  
- Forked the repo under our GitHub org.  
- Made changes under `our-org/helm-charts`.  
- Synced with upstream via:
```bash
git remote add upstream https://github.com/bitnami/helm-charts.git
git fetch upstream
git merge upstream/main
````

**Project Justification During Interview:**
“We forked the Helm charts repo to tailor it to our infrastructure needs while still periodically syncing with upstream to get security patches.”

---

## Q9. Describe a situation where you used GitHub Issues for project tracking.

**Scenario:**
Our QA team reported a bug in the login module during UAT.

**Issue/Need:**
Track it, assign it, and ensure it's resolved and tested before the next release.

**Concept Used:**
GitHub Issues and Labels.

**Steps Taken:**

* Created an issue titled: "Login fails on special character password"
* Assigned to a developer
* Added labels: `bug`, `priority-high`, `module-user-service`
* Linked it to the relevant PR

**Project Justification During Interview:**
“We used GitHub Issues for cross-team tracking. This helped us avoid miscommunication and improved transparency in sprint planning.”

---

## Q10. Tell me about a time you used `git log` and `git blame` for debugging production issues.

**Scenario:**
A recent commit introduced a bug in `cart-service` pricing logic.

**Issue/Need:**
Identify which commit caused it and who made the change.

**Concept Used:**
`git log`, `git blame`, and `git show`.

**Commands Used:**

```bash
git log -p cart/price.js
git blame cart/price.js
git show <commit-id>
```

**Project Justification During Interview:**
“We traced a pricing bug to a specific commit using `git blame`. This helped us fix the logic quickly and add test cases to prevent recurrence.”

---

## Q11. How did you create a README file that helped onboard new developers?

**Scenario:**
New joiners were struggling to understand the project structure and setup steps.

**Issue/Need:**
Improve onboarding speed and reduce mentor dependency.

**Concept Used:**
Creating detailed `README.md`.

**Content Included:**

* Project architecture diagram
* Module-wise responsibilities
* Setup steps (Git clone, environment variables, DB setup)
* Branching strategy

**Project Justification During Interview:**
“We maintained a standardized README for each repo, which helped new developers get started independently in less than an hour.”

---

## Q12. Describe how you handled a hotfix in production using Git.

**Scenario:**
A prod crash occurred due to a null pointer in `payment-service`.

**Issue/Need:**
Fix it urgently without disrupting main development.

**Concept Used:**
Hotfix branch from main.

**Steps Taken:**

```bash
git checkout main
git pull
git checkout -b hotfix/null-check
# Fix applied
git commit -am "Add null check for transaction ID"
git push origin hotfix/null-check
# Raised PR to main → Merge → Deploy
```

**Project Justification During Interview:**
“We used hotfix branching to isolate and quickly patch production bugs without interfering with ongoing features on the `develop` branch.”

---

## Q13. How did you automate GitHub access using Personal Access Tokens (PAT) for shell scripts?

**Scenario:**
We had to automate repo cloning and release tagging in a Jenkins pipeline.

**Issue/Need:**
Avoid manual GitHub login and keep authentication secure.

**Concept Used:**
GitHub PAT for automation.

**Steps Taken:**

* Generated PAT with `repo` scope from GitHub settings
* Stored securely in Jenkins credentials
* Used in shell scripts:

```bash
git clone https://<token>@github.com/org-name/repo.git
```

**Project Justification During Interview:**
“In CI/CD, we used PATs to clone private repos and push tags securely without exposing developer credentials.”

---

## Q14. Tell me about a situation where multiple developers committed to the same branch. How did you manage?

**Scenario:**
During sprint closure, 4 developers pushed to the same `feature/cart-discount` branch.

**Issue/Need:**
Avoid merge chaos and maintain clean commit history.

**Concept Used:**
Team coordination, squash commits, pull regularly.

**Steps Taken:**

* Set team guidelines to `pull --rebase` before pushing
* Used squash during merge to clean history:

```bash
git merge --squash feature/cart-discount
```

**Project Justification During Interview:**
“We coordinated well to avoid stepping on each other’s changes. Squashing commits helped us maintain a clean, meaningful commit log.”

---

## Q15. Share a time when you used `.gitignore` to avoid committing sensitive or large files.

**Scenario:**
Node modules, environment files, and logs were mistakenly pushed initially.

**Issue/Need:**
Prevent unnecessary file tracking and repo bloat.

**Concept Used:**
`.gitignore` best practices.

**Steps Taken:**

```bash
echo "node_modules/" >> .gitignore
echo ".env" >> .gitignore
echo "logs/" >> .gitignore
git rm -r --cached node_modules .env logs
git commit -m "Apply .gitignore rules"
```

**Project Justification During Interview:**
“We used `.gitignore` to keep our repos clean and secure. It helped reduce clone time and avoided sensitive info leakage.”



## Q16. How did you handle switching between multiple Git branches during parallel development?
**Scenario:**  
While fixing a bug in `feature/cart-validation`, I also had to test a new feature from `feature/wishlist-module`.

**Issue/Need:**  
Avoid mixing code or uncommitted changes when switching.

**Concept Used:**  
`git stash`, branch switching, and context isolation.

**Steps Taken:**
```bash
git stash
git checkout feature/wishlist-module
# Work on wishlist
git checkout feature/cart-validation
git stash pop
````

**Project Justification During Interview:**
“To prevent conflicts, I used `git stash` before switching branches. This helped me isolate tasks while working in a fast-paced environment with multiple features.”

---

## Q17. Describe how you implemented Git Flow strategy in a real project.

**Scenario:**
Our project followed structured releases and hotfixes using Git Flow.

**Issue/Need:**
Standardize development, testing, and production releases.

**Concept Used:**
Git Flow (main → develop → feature → release/hotfix)

**Branch Strategy:**

* `main`: Production
* `develop`: Integration
* `feature/*`: New features
* `release/*`: Pre-prod testing
* `hotfix/*`: Emergency fixes

**Project Justification During Interview:**
“In our team, we used Git Flow to handle feature development, scheduled releases, and urgent fixes. This streamlined our CI/CD and reduced merge conflicts.”

---

## Q18. How did you deal with accidental commits to the main branch?

**Scenario:**
A junior developer accidentally committed directly to `main` instead of `develop`.

**Issue/Need:**
Undo the commit and move changes to the correct branch.

**Concept Used:**
`git revert`, `git reset`, and cherry-pick.

**Steps Taken:**

```bash
git checkout main
git revert <commit-id>
git checkout develop
git cherry-pick <commit-id>
```

**Project Justification During Interview:**
“We protected the `main` branch but had one accidental push. We reverted the commit in `main` and cherry-picked it into `develop` for proper testing.”

---

## Q19. Explain how you performed a rollback using Git in a production deployment.

**Scenario:**
A faulty deployment was traced to a buggy commit in `v1.4.2`.

**Issue/Need:**
Quick rollback to last stable version.

**Concept Used:**
Tags and `git checkout`, `git revert`.

**Steps Taken:**

```bash
git checkout tags/v1.4.1
# Optional: create rollback branch
git checkout -b rollback-fix
```

**Project Justification During Interview:**
“We tagged all releases. When v1.4.2 failed, we checked out v1.4.1, tested it, and redeployed. Tagging helped us manage rollbacks cleanly.”

---

## Q20. How did you use GitHub Actions or CI/CD with Git branches?

**Scenario:**
We used GitHub Actions to automatically deploy changes pushed to `main` and run tests on `develop`.

**Issue/Need:**
Automate testing and deployment without manual intervention.

**Concept Used:**
GitHub Actions workflow, branch-based triggers.

**Example `main.yml`:**

```yaml
on:
  push:
    branches: [main, develop]

jobs:
  build-and-test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - run: npm install && npm test
```

**Project Justification During Interview:**
“Our GitHub Actions workflow ensured that any code pushed to `develop` was tested automatically. Once merged into `main`, deployment was triggered.”

---

## Q21. How did you rename a Git branch that was incorrectly named?

**Scenario:**
A teammate named a branch `feature/logiin-page` instead of `feature/login-page`.

**Issue/Need:**
Rename the branch locally and on the remote without losing commits.

**Concept Used:**
Branch rename with Git.

**Steps Taken:**

```bash
git branch -m feature/logiin-page feature/login-page
git push origin --delete feature/logiin-page
git push origin feature/login-page
git push --set-upstream origin feature/login-page
```

**Project Justification During Interview:**
“We maintained strict naming conventions like `feature/*`. We renamed incorrect branches early to maintain consistency and automation rules.”

---

## Q22. Share an experience where you recovered deleted Git commits.

**Scenario:**
One of our developers ran a hard reset and lost unpushed commits.

**Issue/Need:**
Recover the commit using Git’s reflog feature.

**Concept Used:**
`git reflog` and commit recovery.

**Steps Taken:**

```bash
git reflog
git checkout <commit-id>
git branch recovered-work
```

**Project Justification During Interview:**
“Thanks to `git reflog`, we recovered lost work after an unintended reset. This saved hours of developer effort.”

---

## Q23. How did you resolve the ‘detached HEAD’ state during testing?

**Scenario:**
I checked out a specific commit to test a bug fix but forgot to create a branch.

**Issue/Need:**
Avoid losing changes made in a detached state.

**Concept Used:**
Creating a new branch from a detached HEAD.

**Steps Taken:**

```bash
git checkout -b bugfix/token-expiry
```

**Project Justification During Interview:**
“I was in a detached HEAD state while testing. After changes worked, I created a new branch to keep them safe and raise a PR.”

---

## Q24. Describe a time when you cleaned up unnecessary local Git branches.

**Scenario:**
Over time, my local repo had 20+ stale feature branches that were already merged.

**Issue/Need:**
Cleanup local repo and avoid confusion.

**Concept Used:**
Pruning merged branches.

**Steps Taken:**

```bash
git branch --merged
git branch -d feature/old-branch
git branch --merged | grep -v "\*" | xargs -n 1 git branch -d
```

**Project Justification During Interview:**
“I regularly cleaned up stale branches after successful merges to keep the workspace tidy and avoid redundant code base navigation.”

---

## Q25. How did you enforce branch protection rules in GitHub?

**Scenario:**
We wanted to prevent direct pushes to `main` and enforce PR reviews.

**Issue/Need:**
Avoid unreviewed or accidental changes to production.

**Concept Used:**
GitHub branch protection rules.

**Steps Taken:**

* GitHub → Repository Settings → Branches → Add Rule for `main`
* Enabled:

  * Require pull request before merging
  * Require status checks to pass
  * Restrict who can push

**Project Justification During Interview:**
“We used branch protection to secure our `main` branch. All code had to go through PRs, review, and CI validation before merge.”


## Q26. How did you handle a situation where a Git clone operation was failing due to authentication issues?

**Scenario:**  
One of our automation scripts running on a Red Hat EC2 was failing to clone a private GitHub repo.

**Issue/Need:**  
The `git clone` was prompting for credentials and failing in unattended mode.

**Concept Used:**  
Used Personal Access Token (PAT) or SSH key for non-interactive authentication.

**Steps Taken:**
```bash
# Option 1: SSH Setup
ssh-keygen -t ed25519 -C "ec2-user"
cat ~/.ssh/id_ed25519.pub
# Added public key to GitHub > Settings > SSH Keys

# Option 2: PAT usage
git clone https://<PAT>@github.com/org/repo.git
````

**Project Justification During Interview:**
“We faced clone failures in headless automation jobs. Switching from HTTPS to SSH or using a PAT resolved the issue securely and consistently.”

---

## Q27. Explain how you verified Git remote URL misconfiguration in a live CI/CD pipeline.

**Scenario:**
A Jenkins pipeline failed during a `git pull` due to a remote not found error.

**Issue/Need:**
Identify and correct incorrect remote origin configuration.

**Concept Used:**
Remote URL diagnostics and reset.

**Steps Taken:**

```bash
git remote -v
git remote set-url origin git@github.com:org/project.git
```

**Project Justification During Interview:**
“We debugged a failing Jenkins job and found the remote URL was misconfigured after branch migration. Resetting the origin fixed the build.”

---

## Q28. How did you use `git cherry-pick` to backport a fix to multiple branches?

**Scenario:**
A critical fix in `develop` needed to be applied to both `release/v1.0` and `release/v1.1`.

**Issue/Need:**
Avoid reimplementing; reuse the tested commit.

**Concept Used:**
`git cherry-pick`

**Steps Taken:**

```bash
git checkout release/v1.0
git cherry-pick <commit-id>

git checkout release/v1.1
git cherry-pick <commit-id>
```

**Project Justification During Interview:**
“We used cherry-pick to safely apply a tested fix to older release branches without rewriting logic or creating merge conflicts.”

---

## Q29. How did you clean up a large `.git` history that was bloated due to committed binaries?

**Scenario:**
A developer mistakenly pushed 100MB+ log and media files into the repo, affecting clone time.

**Issue/Need:**
Remove large files from entire Git history.

**Concept Used:**
BFG Repo Cleaner / Git filter-branch.

**Steps Taken:**

```bash
bfg --delete-files "*.log"
bfg --delete-folders media --no-blob-protection
git reflog expire --expire=now --all
git gc --prune=now --aggressive
```

**Project Justification During Interview:**
“We had to clean a polluted Git repo with media files. Using BFG and force push helped us reduce repo size from 200MB to 25MB.”

---

## Q30. Explain how you monitored contributors and PR activity in a GitHub organization.

**Scenario:**
As a team lead, I needed visibility into contributor performance and PR activity for reporting.

**Issue/Need:**
Track contributions and engagement without micromanaging.

**Concept Used:**
GitHub insights, contribution graphs, and API.

**Steps Taken:**

* GitHub → Insights → Contributors
* GitHub → Pull Requests → Filter by label/user
* Used GitHub API to extract stats for reports.

**Project Justification During Interview:**
“Using GitHub Insights and scripts, I monitored active contributors, PR timelines, and review cycles, which helped optimize sprint planning.”


## Q31. How did you use environment-specific branches like dev, qa, stage, and prod?

**Scenario:**  
Our team followed environment-based branching for an enterprise healthcare app.

**Issue/Need:**  
Each environment needed isolated deployments and approvals.

**Concept Used:**  
Environment branches: `dev`, `qa`, `stage`, `prod`

**Branch Strategy:**
- Developers merge features into `dev`
- QA tests from `qa` branch
- Approved builds go to `stage`, then `prod`

**Commands & Steps:**
```bash
git checkout dev
git merge feature/user-registration

# Promote from dev to qa
git checkout qa
git merge dev

# Promote from qa to stage
git checkout stage
git merge qa
````

**Project Justification During Interview:**
“We followed an environment branching model to ensure that each stage of the release cycle was isolated and verifiable before hitting production.”

---

## Q32. How did you enforce standard commit messages across teams?

**Scenario:**
Developers were pushing inconsistent commit messages like "fixed stuff", which made it hard to track history.

**Issue/Need:**
Enforce clear, structured commit messages using conventions.

**Concept Used:**
Conventional commits + commit message linting

**Strategy Used:**

* Set rule: type(scope): message
* Example: `feat(login): add throttle logic`

**Tool Used:**
`commitlint` in CI

**Project Justification During Interview:**
“We standardized commit messages using conventional commits to improve Git history clarity and automate changelogs for release notes.”

---

## Q33. Share a situation where you used GitHub CLI or API from a shell script.

**Scenario:**
As part of nightly jobs, we auto-tagged merged PRs and added release notes via script.

**Issue/Need:**
Automate GitHub tasks via shell scripts.

**Concept Used:**
GitHub CLI (`gh`) and GitHub REST API

**Shell Script Sample:**

```bash
gh pr list --state merged --json title,number
gh release create v1.2.3 --notes "Nightly Auto Release"
```

**Project Justification During Interview:**
“We used the GitHub CLI in shell scripts to tag and track releases automatically without manual GitHub UI access.”

---

## Q34. How did you use GitHub Actions to restrict production deployment only from the `prod` branch?

**Scenario:**
An accidental push to `main` once triggered a production deploy.

**Issue/Need:**
Restrict deployment only when changes are merged into `prod`.

**Concept Used:**
GitHub Actions branch-based workflow trigger

**Sample Workflow:**

```yaml
on:
  push:
    branches:
      - prod

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - run: ./deploy-to-prod.sh
```

**Project Justification During Interview:**
“We designed GitHub Actions to only deploy on pushes to the `prod` branch, preventing risky deployments from any other source.”

---

## Q35. How did you manage changelogs during a large release using Git commit history?

**Scenario:**
We were preparing for v2.0 release and needed clean changelogs for QA and business stakeholders.

**Issue/Need:**
Generate changelog automatically from commit messages.

**Concept Used:**
Conventional commits + changelog generator

**Tool Used:**
`standard-version`, `auto-changelog`

**Steps Taken:**

```bash
npx standard-version
```

**Project Justification During Interview:**
“We enforced commit message standards and used `standard-version` to auto-generate changelogs based on commit logs. This made it easy to publish release notes.”








