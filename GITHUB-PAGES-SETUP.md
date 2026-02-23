# GitHub Pages Setup Guide

## 🚨 Fix "Pages not enabled" Error

If you're seeing this error in GitHub Actions:
```
Error: Get Pages site failed. Please verify that the repository has Pages enabled
Error: HttpError: Not Found
```

Follow these steps to enable GitHub Pages:

---

## ✅ Method 1: Enable via Repository Settings (Recommended)

### Step 1: Go to Repository Settings
1. Navigate to your repository: `https://github.com/JatinLodhi/jatinlodhi2002.github.io`
2. Click **Settings** tab at the top
3. Scroll down to **Pages** section in the left sidebar (under "Code and automation")

### Step 2: Configure GitHub Pages
1. Under **Source**, select: **GitHub Actions**
   
   ![GitHub Actions Source](https://docs.github.com/assets/cb-47267/mw-1440/images/help/pages/select-github-actions-source.webp)

2. **DO NOT** select "Deploy from a branch" - we're using GitHub Actions workflow

### Step 3: Save and Verify
1. The setting saves automatically
2. You should see a success message
3. Your site URL will appear: `https://jatinlodhi2002.github.io`

---

## ✅ Method 2: Automatic Enablement (Already Applied)

I've updated your workflow file (`.github/workflows/deploy.yml`) to automatically enable Pages:

```yaml
- name: Setup Pages
  uses: actions/configure-pages@v4
  with:
    enablement: true  # This will auto-enable Pages
```

---

## 🔧 Required Permissions

### Check Workflow Permissions

1. Go to **Settings** → **Actions** → **General**
2. Scroll to **Workflow permissions**
3. Select: **Read and write permissions**
4. Check: ✅ **Allow GitHub Actions to create and approve pull requests**
5. Click **Save**

This ensures the workflow has permission to deploy to Pages.

---

## 🚀 Deploy Now

After enabling Pages, push your changes:

```bash
# Commit the workflow fix
git add .github/workflows/deploy.yml
git commit -m "Fix: Enable GitHub Pages in workflow"
git push origin main
```

Or if everything is already pushed:

```bash
# Trigger workflow manually
# Go to: Actions → Deploy DevOps Portfolio → Run workflow → Run workflow
```

---

## 🔍 Verify Deployment

### Check GitHub Actions
1. Go to **Actions** tab: `https://github.com/JatinLodhi/jatinlodhi2002.github.io/actions`
2. You should see your workflow running
3. Wait for all jobs to complete (Validate → Build → Deploy → Performance Test)

### Check Pages Status
1. Go to **Settings** → **Pages**
2. You should see: **"Your site is live at https://jatinlodhi2002.github.io"**
3. Click the **Visit site** button

### Expected Timeline
- ✅ Workflow runs: 2-3 minutes
- ✅ Pages deployment: 1-2 minutes
- ✅ DNS propagation: 1-5 minutes
- **Total:** ~5-10 minutes for first deployment

---

## ❌ Common Issues & Fixes

### Issue 1: "Pages is not enabled"
**Fix:** Manually enable Pages in Settings (Method 1 above)

### Issue 2: "403 Forbidden" or "Permission denied"
**Fix:** 
- Check workflow permissions (see Required Permissions above)
- Ensure repository is public (or you have GitHub Pro for private repos)

### Issue 3: "404 Not Found" after deployment
**Fix:**
- Clear browser cache
- Wait 5 minutes for DNS propagation
- Check that `index.html` exists in root directory

### Issue 4: Workflow keeps failing
**Fix:**
```bash
# Make sure you're on main branch
git checkout main

# Pull latest changes
git pull origin main

# Re-push to trigger deployment
git commit --allow-empty -m "Trigger deployment"
git push origin main
```

### Issue 5: Branch not protected
If you see: "Branch 'main' is not protected"
**Fix:** This is just a warning, deployment will still work. To fix:
1. Settings → Branches → Add branch protection rule
2. Branch name pattern: `main`
3. Save changes

---

## 🎯 Quick Checklist

Before deployment, verify:

- [x] Repository is public (or GitHub Pro for private)
- [x] Pages enabled in Settings → Pages
- [x] Source set to "GitHub Actions"
- [x] Workflow permissions set to "Read and write"
- [x] `.github/workflows/deploy.yml` exists
- [x] `index.html` exists in root directory
- [x] Changes pushed to `main` branch

---

## 📞 Still Having Issues?

### Check Workflow Logs
1. Go to Actions tab
2. Click on the failed workflow run
3. Click on the failed job
4. Expand the step that failed
5. Read the error message

### Common Error Messages

**"refusing to allow a Personal Access Token"**
- Fix: Use `secrets.GITHUB_TOKEN` (already configured in workflow)

**"Resource not accessible by integration"**
- Fix: Enable workflow write permissions (see above)

**"No such file or directory"**
- Fix: Ensure all files are committed and pushed

---

## 🎉 Success!

Once deployed, your site will be available at:
**https://jatinlodhi2002.github.io**

Test the following:
- ✅ Homepage loads
- ✅ Dark mode toggle works
- ✅ All sections visible
- ✅ Responsive on mobile
- ✅ Navigation works
- ✅ Links are clickable

---

## 🔄 Future Deployments

After initial setup, deployments are automatic:

1. Make changes to your files
2. Commit and push to `main` branch
3. GitHub Actions automatically deploys
4. Site updates in 2-3 minutes

```bash
# Standard workflow
git add .
git commit -m "Update portfolio content"
git push origin main
# Deployment happens automatically!
```

---

## 📚 Additional Resources

- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Troubleshooting GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/troubleshooting-404-errors-for-github-pages-sites)

---

**Last Updated:** February 24, 2026
