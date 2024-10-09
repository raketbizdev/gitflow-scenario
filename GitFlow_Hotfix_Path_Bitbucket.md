
# 2. Hotfix Path: Critical Bug Found in Production (Using Bitbucket)

**Scenario**: A critical bug is discovered in production, and it requires an immediate fix. This scenario demonstrates how to handle a hotfix using GitFlow in Bitbucket, ensuring that the fix is applied directly to the `main` branch and then synchronized back to `develop`.

---

## Step-by-Step Process with Detailed Commands and Bitbucket Integration:

### 1. Create a Hotfix Branch from `main`
The developer starts by creating a new hotfix branch from the `main` branch. The hotfix branch should follow the naming convention: `hotfix/<issue-description>`. In this example, we use `hotfix/critical-bug`.

```bash
# Switch to the 'main' branch
git checkout main

# Pull the latest changes from the remote repository to ensure it's up-to-date
git pull origin main

# Create a new hotfix branch
git checkout -b hotfix/critical-bug
```

### 2. Implement the Fix and Commit Changes Locally
The developer then implements the necessary bug fix and commits the changes with a clear commit message indicating the fix.

```bash
# Stage the changes
git add .

# Commit the changes with a descriptive message
git commit -m "Fix critical bug causing system crash on login"
```

### 3. Push the `hotfix/critical-bug` Branch to the Remote Bitbucket Repository
Now the developer pushes the newly created `hotfix/critical-bug` branch to the remote repository in Bitbucket.

```bash
# Push the hotfix branch to Bitbucket
git push origin hotfix/critical-bug
```

### 4. Create a Pull Request (PR) to Merge `hotfix/critical-bug` into `main` in Bitbucket
1. Go to the **Bitbucket** web interface.
2. Navigate to the **"Pull Requests"** tab.
3. Click **"Create pull request"**.
4. Choose the **source branch** as `hotfix/critical-bug` and the **destination branch** as `main`.
5. Fill in the required fields:
   - **Title**: "Hotfix: Fix critical bug in production"
   - **Description**: "This hotfix addresses a critical bug that causes a system crash on login. The fix ensures proper handling of invalid login inputs."
6. Assign reviewers and **submit the pull request** for review.

### 5. The PR is Reviewed and Approved
During the review process:
- Other developers or tech leads review the hotfix and suggest any changes.
- The hotfix should be tested rigorously to ensure it resolves the issue without introducing new bugs.
- The developer addresses any feedback if necessary.

Once all reviews are approved, the PR is marked as **ready to merge**.

### 6. Merge the `hotfix/critical-bug` Branch into `main`
Once the PR is approved in Bitbucket, use the **"Merge"** button on the Bitbucket PR page to merge `hotfix/critical-bug` into `main`.

- Check the option to **delete the hotfix branch** after merging to keep the repository clean.

Alternatively, if using the command line:

```bash
# Switch to the 'main' branch
git checkout main

# Merge the hotfix branch into main
git merge hotfix/critical-bug

# Push changes to the remote repository
git push origin main
```

### 7. Tag the New Release in `main`
After merging the hotfix into `main`, the developer or release manager should tag the new release to track the hotfix.

```bash
# Tag the new hotfix release
git tag -a v1.0.1 -m "Hotfix v1.0.1: Critical bug fix for system crash on login"

# Push the tag to the remote repository
git push origin v1.0.1
```

### 8. Merge the `hotfix/critical-bug` Branch into `develop`
To keep the `develop` branch in sync with `main`, the developer merges the `hotfix/critical-bug` branch into `develop` to ensure that the fix is available in the ongoing development branch.

```bash
# Switch to develop
git checkout develop

# Merge the hotfix branch into develop
git merge hotfix/critical-bug

# Push changes to the remote repository in Bitbucket
git push origin develop
```

### 9. Delete the Hotfix Branch in Bitbucket
After the hotfix has been merged into both `main` and `develop`, delete the `hotfix/critical-bug` branch from Bitbucket to keep the repository clean.

1. Go to the **"Branches"** section in Bitbucket.
2. Locate the `hotfix/critical-bug` branch.
3. Click **"Delete"**.

---

## Key Points for Bitbucket Integration:
1. **Create separate hotfix branches** for each critical issue.
2. **Always merge hotfixes into both `main` and `develop`** to avoid branch drift.
3. **Use Pull Requests** for all merges to maintain code quality and visibility.
4. **Tag hotfix releases** to keep track of all patches applied to the production environment.

This detailed process should help your team understand the full lifecycle of handling a critical hotfix using GitFlow in Bitbucket.
