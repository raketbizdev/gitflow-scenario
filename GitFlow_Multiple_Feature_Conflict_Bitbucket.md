
# 3. Multiple Feature Integration Conflict (Using Bitbucket)

**Scenario**: Two developers are working on different features simultaneously and both try to merge into the `develop` branch, causing conflicts. This scenario demonstrates how to resolve integration conflicts when multiple feature branches are being merged into `develop`.

---

## Step-by-Step Process with Detailed Commands and Bitbucket Integration:

### 1. Create Two Feature Branches from `develop`
Two developers, Developer A and Developer B, start by creating separate feature branches from `develop`. Developer A creates `feature/user-login`, and Developer B creates `feature/cart-system`.

#### Developer A: Create the `feature/user-login` branch
```bash
# Switch to the 'develop' branch
git checkout develop

# Create and switch to a new feature branch
git checkout -b feature/user-login

# Push the branch to Bitbucket
git push origin feature/user-login
```

#### Developer B: Create the `feature/cart-system` branch
```bash
# Switch to the 'develop' branch
git checkout develop

# Create and switch to a new feature branch
git checkout -b feature/cart-system

# Push the branch to Bitbucket
git push origin feature/cart-system
```

### 2. Developer A Completes Their Feature and Creates a Pull Request (PR)
Developer A completes the `user-login` feature and creates a pull request to merge `feature/user-login` into `develop`.

1. Go to the **Bitbucket** web interface.
2. Navigate to the **"Pull Requests"** tab.
3. Click **"Create pull request"**.
4. Choose the **source branch** as `feature/user-login` and the **destination branch** as `develop`.
5. Fill in the required fields:
   - **Title**: "Feature: User login"
   - **Description**: "Adds a user login feature with authentication and validation."
6. Assign reviewers and **submit the pull request**.

### 3. Developer A's PR is Merged into `develop`
The `feature/user-login` branch is reviewed, approved, and successfully merged into the `develop` branch.

```bash
# Switch to the 'develop' branch
git checkout develop

# Merge the feature branch into develop
git merge feature/user-login

# Push changes to the remote repository
git push origin develop
```

### 4. Developer B Attempts to Merge `feature/cart-system` into `develop` and Encounters a Conflict
After Developer A's feature is merged, Developer B tries to merge their `feature/cart-system` into `develop` and encounters a **merge conflict**.

```bash
# Switch to the 'develop' branch
git checkout develop

# Attempt to merge the cart-system feature branch into develop
git merge feature/cart-system
```

Git outputs a **merge conflict** message, indicating that there are conflicting files that need to be resolved manually.

### 5. Resolve the Merge Conflict
Developer B switches back to their `feature/cart-system` branch, pulls the latest changes from `develop`, and resolves the conflicts.

```bash
# Switch to the 'feature/cart-system' branch
git checkout feature/cart-system

# Pull the latest changes from the updated develop branch
git pull origin develop
```

- Open the conflicting files in a text editor.
- Manually resolve the conflicts by choosing the correct version of the code or combining changes.
- After resolving the conflicts, stage the resolved files:

```bash
# Stage the resolved files
git add <resolved-file>
```

### 6. Commit the Resolved Changes and Push the Updated Branch
After resolving the conflicts, Developer B commits the changes and pushes the updated `feature/cart-system` branch.

```bash
# Commit the changes with a descriptive message
git commit -m "Resolve merge conflict with develop"

# Push the updated branch to Bitbucket
git push origin feature/cart-system
```

### 7. Create a New PR for `feature/cart-system` in Bitbucket
Developer B creates a new PR to merge `feature/cart-system` into `develop` with the resolved conflicts.

1. Go to the **Bitbucket** web interface.
2. Navigate to the **"Pull Requests"** tab.
3. Click **"Create pull request"**.
4. Choose the **source branch** as `feature/cart-system` and the **destination branch** as `develop`.
5. Fill in the required fields:
   - **Title**: "Feature: Cart System"
   - **Description**: "Integrates cart system with add-to-cart and checkout features."
6. Assign reviewers and **submit the pull request**.

### 8. The PR is Reviewed and Merged into `develop`
The updated `feature/cart-system` branch is reviewed, approved, and merged into `develop`.

```bash
# Switch to the 'develop' branch
git checkout develop

# Merge the feature branch into develop
git merge feature/cart-system

# Push changes to the remote repository
git push origin develop
```

### 9. Delete the Resolved Feature Branches in Bitbucket
After both features are successfully merged into `develop`, delete the feature branches to keep the repository clean.

1. Go to the **"Branches"** section in Bitbucket.
2. Locate the `feature/user-login` and `feature/cart-system` branches.
3. Click **"Delete"** for both branches.

---

## Key Points for Bitbucket Integration:
1. **Create separate feature branches** for each new feature to avoid conflicts.
2. **Always pull the latest `develop` changes** before merging your feature branch to avoid unnecessary conflicts.
3. **Resolve merge conflicts** in a separate commit to keep the history clean.
4. **Delete merged branches** to keep the repository organized.

This detailed process should help your team understand how to handle multiple feature integration conflicts using GitFlow in Bitbucket.
