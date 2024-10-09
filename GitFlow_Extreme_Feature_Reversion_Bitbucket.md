
# 4. Extreme Path: Feature Reversion After Multiple Releases (Using Bitbucket)

**Scenario**: A feature (`feature/payment-gateway`) was introduced in release `v1.1.0`, but it caused intermittent issues in production. This feature has already been carried over through two releases (`v1.1.0` and `v1.2.0`). Due to the complexity and risks, the decision is made to remove the feature from production and revert it completely.

---

## Step-by-Step Process with Detailed Commands and Bitbucket Integration:

### 1. Identify All Commits Related to the Problematic Feature
The developer needs to identify all commits related to `feature/payment-gateway` across multiple releases. This can be done using `git log` and `git grep`:

```bash
# Check commit history for the feature across all branches
git log --all --grep="payment-gateway"
```

Identify each commit that was made specifically for `feature/payment-gateway` and note down the commit hashes.

### 2. Create a Reversion Branch from the Latest `main`
Create a new branch named `revert/feature-payment-gateway` from the latest `main` branch.

```bash
# Switch to the 'main' branch
git checkout main

# Pull the latest changes to ensure it's up-to-date
git pull origin main

# Create and switch to a new reversion branch
git checkout -b revert/feature-payment-gateway
```

### 3. Revert the Identified Commits
Use `git revert` to undo each commit related to `feature/payment-gateway`. The `git revert` command creates new commits that effectively reverse the changes made by the original commits.

```bash
# Revert each commit one by one
git revert <commit-hash-1>
git revert <commit-hash-2>
git revert <commit-hash-3>
```

Continue reverting until all problematic commits have been reversed. If there are merge conflicts during this step, resolve them manually and commit the resolved changes.

### 4. Push the `revert/feature-payment-gateway` Branch to the Remote Bitbucket Repository
Once all the reversions are complete, push the new reversion branch to the remote repository.

```bash
# Push the reversion branch to Bitbucket
git push origin revert/feature-payment-gateway
```

### 5. Create a Pull Request (PR) to Merge `revert/feature-payment-gateway` into `main` in Bitbucket
1. Go to the **Bitbucket** web interface.
2. Navigate to the **"Pull Requests"** tab.
3. Click **"Create pull request"**.
4. Choose the **source branch** as `revert/feature-payment-gateway` and the **destination branch** as `main`.
5. Fill in the required fields:
   - **Title**: "Revert: Remove payment gateway feature"
   - **Description**: "This reversion removes the payment gateway feature introduced in v1.1.0, due to persistent issues in production."
6. Assign reviewers and **submit the pull request** for review.

### 6. The PR is Reviewed and Approved
The reversion PR should be carefully reviewed by other developers and QA to ensure that removing the feature does not introduce new issues.

### 7. Merge the `revert/feature-payment-gateway` Branch into `main`
Once the PR is approved in Bitbucket, use the **"Merge"** button on the Bitbucket PR page to merge `revert/feature-payment-gateway` into `main`.

Alternatively, if using the command line:

```bash
# Switch to the 'main' branch
git checkout main

# Merge the reversion branch into main
git merge revert/feature-payment-gateway

# Push changes to the remote repository
git push origin main
```

### 8. Tag the New Release in `main`
After merging the reversion into `main`, the release manager should tag the new release to track the reversion.

```bash
# Tag the new release to indicate the reversion
git tag -a v1.3.1 -m "Reversion v1.3.1: Remove payment gateway feature"

# Push the new tag to the remote repository
git push origin v1.3.1
```

### 9. Merge the `revert/feature-payment-gateway` Branch into `develop`
To keep the `develop` branch synchronized with `main`, the reversion branch needs to be merged into `develop`.

```bash
# Switch to develop
git checkout develop

# Merge the reversion branch into develop
git merge revert/feature-payment-gateway

# Push changes to the remote repository in Bitbucket
git push origin develop
```

### 10. Delete the Reversion Branch in Bitbucket
After the reversion has been merged into both `main` and `develop`, delete the `revert/feature-payment-gateway` branch from Bitbucket to keep the repository clean.

1. Go to the **"Branches"** section in Bitbucket.
2. Locate the `revert/feature-payment-gateway` branch.
3. Click **"Delete"**.

---

## Key Points for Bitbucket Integration:
1. **Carefully identify all commits** related to the feature to ensure a complete reversion.
2. **Use a separate branch** for complex reverts to keep the history clean.
3. **Always merge reversion branches into both `main` and `develop`** to maintain consistency.
4. **Tag reversion releases** clearly to track changes in production.

This detailed process should help your team understand how to handle extreme feature reversions using GitFlow in Bitbucket.
