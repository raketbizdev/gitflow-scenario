
# 5. Unplanned Merge of a Feature into `main` (Using Bitbucket)

**Scenario**: A developer mistakenly merges a feature branch into the `main` branch instead of `develop`. This situation needs to be resolved by reverting the erroneous commit and reapplying the feature to the correct branch (`develop`).

---

## Step-by-Step Process with Detailed Commands and Bitbucket Integration:

### 1. Identify the Erroneous Commit in the `main` Branch
Identify the specific commit that introduced the feature into `main`. Use `git log` to find the commit hash.

```bash
# View the commit history of the main branch
git log main
```

Locate the commit that should not have been merged. Note down the commit hash.

### 2. Create a Revert Commit on the `main` Branch
To undo the unplanned merge, create a new commit that reverses the changes introduced by the problematic commit.

```bash
# Switch to the 'main' branch
git checkout main

# Revert the erroneous commit
git revert <commit-hash>

# Push the revert commit to the remote repository
git push origin main
```

### 3. Create a New Pull Request (PR) for the Feature into `develop`
To ensure the feature is integrated into the right branch, the developer needs to create a new PR for the feature branch into `develop`.

1. Go to the **Bitbucket** web interface.
2. Navigate to the **"Pull Requests"** tab.
3. Click **"Create pull request"**.
4. Choose the **source branch** (e.g., `feature/experimental-ui`) and set the **destination branch** as `develop`.
5. Fill in the required fields:
   - **Title**: "Feature: Experimental UI"
   - **Description**: "This pull request correctly integrates the experimental UI feature into `develop`."
6. Assign reviewers and **submit the pull request**.

### 4. Merge the PR into `develop`
The PR is reviewed, approved, and merged into `develop` as intended.

```bash
# Switch to the 'develop' branch
git checkout develop

# Merge the feature branch into develop
git merge feature/experimental-ui

# Push changes to the remote repository
git push origin develop
```

### 5. Validate the `main` Branch to Ensure Stability
After reverting the erroneous commit in `main`, ensure that the `main` branch is still stable:

- Run any automated tests (if available).
- Verify that the application behaves correctly in production.

### 6. Communicate with the Team and Document the Incident
Notify the team of the unplanned merge and document it for future reference. Clearly state the following:

- **What happened**: A feature was merged into `main` instead of `develop`.
- **How it was resolved**: The erroneous commit was reverted, and the feature was re-applied to the `develop` branch.
- **Lessons learned**: Steps to prevent this mistake from happening again (e.g., adding branch protection rules).

### 7. Implement Branch Protection Rules in Bitbucket (Optional)
To prevent this issue from recurring, set up branch permissions and protection rules in Bitbucket:

1. Go to the repository settings in Bitbucket.
2. Navigate to **"Branch Permissions"**.
3. Add a new permission for the `main` branch:
   - Restrict direct merges to `main`.
   - Require pull request approvals before merging.
4. Save the changes.

---

## Key Points for Bitbucket Integration:
1. **Identify and revert erroneous commits** immediately to maintain branch stability.
2. **Create a new PR** to correctly merge the feature into the intended branch (`develop`).
3. **Validate `main` thoroughly** after reverts to avoid introducing side effects.
4. **Implement branch protection** to reduce the risk of future unplanned merges.

This detailed process should help your team handle unplanned merges into `main` using GitFlow in Bitbucket.
