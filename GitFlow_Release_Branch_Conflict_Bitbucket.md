
# 6. Release Branch Conflict Due to Last-Minute Change Requests (Using Bitbucket)

**Scenario**: During testing of the `release/v2.0.0` branch, several new critical change requests are added at the last minute. This creates a situation where multiple developers are working on different fixes simultaneously, causing merge conflicts in the release branch.

---

## Step-by-Step Process with Detailed Commands and Bitbucket Integration:

### 1. Create a Release Branch from `develop`
The Release Manager creates a new release branch named `release/v2.0.0` from the `develop` branch to start preparing for deployment.

```bash
# Switch to the 'develop' branch
git checkout develop

# Pull the latest changes to ensure it's up-to-date
git pull origin develop

# Create and switch to a new release branch
git checkout -b release/v2.0.0

# Push the release branch to the remote repository
git push origin release/v2.0.0
```

### 2. Multiple Bugfix Branches are Created from the Release Branch
Three separate bugfix branches are created to address different change requests:

#### Bugfix Branch 1: `bugfix/ui-fix`
```bash
# Create and switch to a new bugfix branch from release
git checkout -b bugfix/ui-fix release/v2.0.0

# Push the bugfix branch to the remote repository
git push origin bugfix/ui-fix
```

#### Bugfix Branch 2: `bugfix/api-endpoint`
```bash
# Create and switch to a new bugfix branch from release
git checkout -b bugfix/api-endpoint release/v2.0.0

# Push the bugfix branch to the remote repository
git push origin bugfix/api-endpoint
```

#### Bugfix Branch 3: `bugfix/db-connection`
```bash
# Create and switch to a new bugfix branch from release
git checkout -b bugfix/db-connection release/v2.0.0

# Push the bugfix branch to the remote repository
git push origin bugfix/db-connection
```

### 3. Implement Fixes and Create Separate PRs for Each Bugfix Branch
Each developer implements their respective fixes in their own bugfix branches and creates a PR targeting `release/v2.0.0`.

1. Go to the **Bitbucket** web interface.
2. Navigate to the **"Pull Requests"** tab.
3. Click **"Create pull request"**.
4. Choose the **source branch** (e.g., `bugfix/ui-fix`) and set the **destination branch** as `release/v2.0.0`.
5. Fill in the required fields:
   - **Title**: "Bugfix: UI Fix for Release v2.0.0"
   - **Description**: "Fixes UI alignment and layout issues identified during UAT testing."
6. Assign reviewers and **submit the pull request**.

Repeat this process for each of the bugfix branches (`bugfix/api-endpoint` and `bugfix/db-connection`).

### 4. Merge the First Two PRs Successfully into `release/v2.0.0`
The `bugfix/ui-fix` and `bugfix/api-endpoint` branches are reviewed, approved, and merged into the `release/v2.0.0` branch.

```bash
# Switch to the release branch
git checkout release/v2.0.0

# Merge the first bugfix branch
git merge bugfix/ui-fix

# Merge the second bugfix branch
git merge bugfix/api-endpoint

# Push changes to the remote repository
git push origin release/v2.0.0
```

### 5. Conflict Occurs While Merging `bugfix/db-connection` into `release/v2.0.0`
When the third bugfix (`bugfix/db-connection`) is merged, a conflict occurs due to changes made in the previous bugfix branches.

```bash
# Attempt to merge the third bugfix branch into release
git merge bugfix/db-connection
```

Git outputs a **merge conflict** message, indicating that there are conflicting files that need to be resolved manually.

### 6. Resolve the Merge Conflict
The developer working on the `bugfix/db-connection` branch needs to resolve the conflict manually:

```bash
# Open the conflicting files in a text editor and resolve the conflicts
# Manually edit the conflicting files to retain the correct changes from both branches

# After resolving the conflicts, stage the resolved files
git add <resolved-file>
```

### 7. Commit the Resolved Changes and Push the Updated Release Branch
After resolving the conflicts, the developer commits the changes and pushes the updated `release/v2.0.0` branch.

```bash
# Commit the changes with a descriptive message
git commit -m "Resolve merge conflict between bugfix branches in release/v2.0.0"

# Push the updated release branch to the remote repository
git push origin release/v2.0.0
```

### 8. Continue Testing and Finalize the Release
Once all bugfixes are merged and conflicts are resolved, the release branch undergoes final testing. If everything is validated successfully, the Release Manager proceeds with the release.

### 9. Merge `release/v2.0.0` into `main` and Tag the Release
After testing is complete, the Release Manager merges `release/v2.0.0` into `main` and tags the release:

```bash
# Switch to the 'main' branch
git checkout main

# Merge the release branch into main
git merge release/v2.0.0

# Tag the new release version
git tag -a v2.0.0 -m "Release version 2.0.0: Multiple bugfixes applied"

# Push the changes and tags to the remote repository
git push origin main
git push origin v2.0.0
```

### 10. Merge `release/v2.0.0` Back into `develop`
Finally, merge the `release/v2.0.0` branch back into `develop` to synchronize the development branch.

```bash
# Switch to the 'develop' branch
git checkout develop

# Merge the release branch into develop
git merge release/v2.0.0

# Push the changes to the remote repository
git push origin develop
```

### 11. Delete All Bugfix and Release Branches in Bitbucket
After completing the release, delete all the merged branches (`bugfix/ui-fix`, `bugfix/api-endpoint`, `bugfix/db-connection`, and `release/v2.0.0`) to keep the repository clean.

1. Go to the **"Branches"** section in Bitbucket.
2. Locate each of the merged branches.
3. Click **"Delete"** for each branch.

---

## Key Points for Bitbucket Integration:
1. **Create separate bugfix branches** for each critical issue to avoid conflicts.
2. **Merge changes sequentially** to reduce the risk of merge conflicts in the release branch.
3. **Resolve conflicts** carefully and keep a clear history for each resolved issue.
4. **Always merge the release branch back into `develop`** to avoid branch drift.

This detailed process should help your team handle last-minute change requests and release branch conflicts using GitFlow in Bitbucket.
