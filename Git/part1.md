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


