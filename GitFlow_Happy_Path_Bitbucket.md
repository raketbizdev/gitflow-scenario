
# 1. Happy Path: Feature Development and Release (Using Bitbucket)

**Scenario**: A developer needs to create a new feature (`login-form`) for an upcoming release using Bitbucket and following the GitFlow workflow. This includes creating a feature branch, making changes, creating a pull request (PR), merging into `develop`, and preparing for a formal release.

---

## Step-by-Step Process with Detailed Commands and Bitbucket Integration:

### 1. Create a Feature Branch from `develop`
The developer starts by switching to the `develop` branch locally and creates a new feature branch named `feature/login-form`.

```bash
# Ensure you are on the 'develop' branch
git checkout develop

# Create and switch to a new feature branch
git checkout -b feature/login-form
```

### 2. Develop the Feature and Commit Changes Locally
The developer writes code to implement the new feature (e.g., adding a login form UI component). Once development is complete, the developer stages and commits the changes.

```bash
# Stage the changes
git add .

# Commit the changes with a descriptive message
git commit -m "Add login form to the application"
```

### 3. Push the `feature/login-form` Branch to the Remote Bitbucket Repository
Now the developer pushes the newly created `feature/login-form` branch to the remote repository in Bitbucket.

```bash
# Push the local branch to the remote repository in Bitbucket
git push origin feature/login-form
```

### 4. Create a Pull Request (PR) to Merge `feature/login-form` Back into `develop` in Bitbucket
1. Go to the **Bitbucket** web interface.
2. Navigate to the **"Pull Requests"** tab.
3. Click **"Create pull request"**.
4. Choose the **source branch** as `feature/login-form` and the **destination branch** as `develop`.
5. Fill in the required fields:
   - **Title**: "Feature: Add login form"
   - **Description**: "This feature adds a new login form to the user interface. Includes validation and error handling."
6. Assign reviewers (other developers or a tech lead) and **submit the pull request** for review.

### 5. The PR is Reviewed by Other Developers, and Unit Tests Pass
During the review process:
- Other developers or team leads review the code and suggest any changes.
- Automated unit tests (if configured via **Bitbucket Pipelines**) run on the PR.
- The developer addresses feedback and makes additional commits to the `feature/login-form` branch if necessary.

Once all reviews are approved, and tests pass, the PR is marked as **ready to merge**.

### 6. Merge the `feature/login-form` Branch into `develop`
Once the PR is approved in Bitbucket, use the **"Merge"** button on the Bitbucket PR page to merge `feature/login-form` into `develop`.

- Check the option to **delete the feature branch** after merging to keep the repository clean.

Alternatively, if using the command line:

```bash
# Checkout develop
git checkout develop

# Merge the feature branch into develop
git merge feature/login-form

# Push changes to the remote Bitbucket repository
git push origin develop
```

### 7. Release Manager Creates a Release Branch (`release/v1.0.0`) from `develop`
After all feature development is complete and merged into `develop`, the Release Manager creates a new `release` branch to prepare for the release version `v1.0.0`.

```bash
# Ensure the latest changes are pulled to the 'develop' branch
git checkout develop
git pull origin develop

# Create and switch to a new release branch
git checkout -b release/v1.0.0

# Push the release branch to the Bitbucket remote repository
git push origin release/v1.0.0
```

In Bitbucket, the Release Manager can also use the **"Create Branch"** feature to create a `release/v1.0.0` branch from `develop` if needed.

### 8. The Release Branch is Tested
- **QA** and **UAT** teams perform testing on the `release/v1.0.0` branch.
- Any final changes, bug fixes, or tweaks are made directly on the `release/v1.0.0` branch.
- Each change is **committed and pushed** as necessary:

```bash
git add .
git commit -m "Final bug fixes and tweaks for v1.0.0"
git push origin release/v1.0.0
```

### 9. Release Manager Merges `release/v1.0.0` into `main` and Tags the Release
Once the `release/v1.0.0` branch is thoroughly tested and validated, the Release Manager merges it into the `main` branch and creates a tag for the release:

```bash
# Switch to main branch
git checkout main

# Merge the release branch into main
git merge release/v1.0.0

# Tag the new release
git tag -a v1.0.0 -m "Release version 1.0.0: Initial login form feature"

# Push the changes and tags to the remote repository in Bitbucket
git push origin main
git push origin v1.0.0
```

Alternatively, this step can be done via the **"Pull Requests"** feature in Bitbucket by creating a new **PR** from `release/v1.0.0` to `main`, completing the merge, and creating a tag through the Bitbucket UI.

---

## Key Points for Bitbucket Integration:
1. **Use Bitbucket Pipelines** for automated testing and deployment triggers.
2. **Set up branch permissions** to enforce proper reviews on the `develop` and `main` branches.
3. **Use Pull Requests** for all merges to maintain code quality and visibility.
4. **Tag releases** and **create new releases** using the Bitbucket **"Releases"** feature to track versions.

This detailed process with Bitbucket-specific steps should help your team understand the full lifecycle using GitFlow, from feature development to merging the release into `main`.
