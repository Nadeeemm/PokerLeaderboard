# 🚀 Automated GitHub Pages Deployment Guide

## Overview
This project uses **GitHub Actions** to automatically deploy the latest code to GitHub Pages whenever a pull request (PR) is merged into the `main` branch.

---

## How It Works

### Deployment Workflow
```
PR Created on Feature Branch
         ↓
    Code Review
         ↓
    Approve PR
         ↓
   Merge to Main
         ↓
GitHub Actions Triggers
         ↓
Checkout Code
         ↓
Configure GitHub Pages
         ↓
Upload Artifact
         ↓
Deploy to GitHub Pages
         ↓
🎉 Live on https://nadeeemm.github.io/PokerLeaderboard/
```

---

## Workflow File Location
```
.github/workflows/deploy.yml
```

### File Structure
```
PokerLeaderboard/
├── .github/
│   └── workflows/
│       └── deploy.yml          ← Deployment configuration
├── index.html                   ← Main HTML file (deployed)
├── data.json                    ← Data file (deployed)
└── [other project files]        ← All files are deployed
```

---

## Workflow Triggers

### ✅ When Deployment RUNS:
- Any **push to the `main` branch**
- Typically happens when a PR is **merged** into main
- Can also be triggered manually by direct commits to main

### ❌ When Deployment DOES NOT RUN:
- Commits to feature branches (e.g., `patch-19`, `feature-x`)
- Commits to other branches like `develop`, `staging`

---

## Deployment Steps (In Order)

### Step 1: Checkout Repository Code
- Downloads your repository code
- Makes all files available for deployment
- Action: `actions/checkout@v4`

### Step 2: Configure GitHub Pages
- Prepares the GitHub Pages environment
- Sets up hosting configuration
- Action: `actions/configure-pages@v4`

### Step 3: Upload Artifact
- Packages all repository files as a deployment artifact
- Includes: HTML, CSS, JavaScript, JSON, images, etc.
- Uploads the entire root directory (`./`)
- Action: `actions/upload-pages-artifact@v3`

### Step 4: Deploy to GitHub Pages
- Publishes the artifact to your GitHub Pages URL
- Makes your site live on the internet
- Outputs the deployment URL
- Action: `actions/deploy-pages@v4`

---

## Prerequisites & Setup

### ✅ Requirements:
1. **GitHub Pages Enabled**
   - Go to: Repository Settings → Pages
   - Source: Select "GitHub Actions"
   - Click Save

2. **Repository Visibility**
   - Public repositories: GitHub Pages works automatically
   - Private repositories: GitHub Pages available with GitHub Pro

3. **Main Branch Protection** (Recommended)
   - Require PR reviews before merging
   - Ensures code quality before automatic deployment

### 📋 Setup Checklist:
- [ ] Enable GitHub Pages in repository settings
- [ ] Set deployment source to "GitHub Actions"
- [ ] Create feature branches for changes
- [ ] Create PRs from feature branches to main
- [ ] Get code reviewed and approved
- [ ] Merge PR to main → Automatic deployment!

---

## Making Changes & Deploying

### Standard Workflow:
```bash
# 1. Create feature branch
git checkout -b feature/my-changes

# 2. Make your changes
# (edit files, add new files, etc.)

# 3. Commit changes
git add .
git commit -m "Add my awesome changes"

# 4. Push to GitHub
git push origin feature/my-changes

# 5. Create Pull Request on GitHub
# - Go to repository on GitHub
# - Click "New Pull Request"
# - Select your branch
# - Add description
# - Submit PR

# 6. Code Review
# - Team reviews your changes
# - Discusses improvements
# - Approves changes

# 7. Merge to Main
# - Click "Merge pull request" on GitHub
# - Workflow automatically triggers! 🎉
# - Site is deployed in ~2-3 minutes

# 8. Monitor Deployment
# - Go to repository → Actions tab
# - Watch the workflow run
# - See success/failure status
```

---

## Monitoring Deployments

### View Workflow Status:
1. Go to your GitHub repository
2. Click **"Actions"** tab
3. Click **"Deploy to GitHub Pages"** workflow
4. View recent runs with status:
   - ✅ **Green checkmark** = Deployment successful
   - ❌ **Red X** = Deployment failed

### View Deployment URL:
- After successful deployment, workflow shows the URL
- Typically: `https://nadeeemm.github.io/PokerLeaderboard/`
- Always accessible after deployment

---

## Troubleshooting

### Deployment Failed?
1. Check **Actions** tab for error messages
2. Common issues:
   - GitHub Pages not enabled in settings
   - Branch protection rules preventing merge
   - File size limits (100GB max for GitHub Pages)

### Changes Not Showing Live?
1. Wait 2-3 minutes for deployment to complete
2. Hard refresh browser: `Ctrl+Shift+R` (or `Cmd+Shift+R` on Mac)
3. Check that you merged to `main` branch
4. Verify deployment succeeded in Actions tab

### Can't Merge to Main?
1. Ensure all branch protection rules are met:
   - PR reviews approved
   - All checks passing
   - Branches up to date
2. Check GitHub Actions status

---

## Permissions Used

The workflow requires these GitHub permissions:

| Permission | Purpose | Used By |
|-----------|---------|----------|
| `contents: read` | Read repository files | Checkout action |
| `pages: write` | Deploy to GitHub Pages | Deploy Pages action |
| `id-token: write` | Generate secure tokens | GitHub's secure deployment |

---

## Performance Notes

- **Deployment Time:** Typically 1-3 minutes
- **Site Availability:** Always live (no downtime)
- **File Size:** Entire repository deployed (no size limit restrictions in this setup)
- **Caching:** GitHub Pages caches for performance; hard refresh if needed

---

## Best Practices

### ✅ DO:
- Create feature branches for changes
- Use descriptive commit messages
- Request code reviews before merging
- Test changes locally before creating PR
- Write meaningful PR descriptions

### ❌ DON'T:
- Commit directly to `main` without PR (avoid if using branch protection)
- Push large binary files (>100MB)
- Merge PRs without review
- Make changes after "Deploy to Pages" starts

---

## Emergency: Manual Deployment

If needed, you can manually trigger the workflow:
1. Go to Actions tab
2. Select "Deploy to GitHub Pages"
3. Click "Run workflow"
4. Confirm deployment

---

## Related Files
- [SECURITY_SETUP.md](./SECURITY_SETUP.md) - Security configuration
- [JSON_GUIDE.md](./JSON_GUIDE.md) - Data structure guide
- [.github/workflows/deploy.yml](./.github/workflows/deploy.yml) - Workflow configuration

---

## Questions?
For GitHub Actions documentation:
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [GitHub Pages Documentation](https://docs.github.io)

---

**Last Updated:** April 19, 2026  
**Workflow Version:** v1.0
