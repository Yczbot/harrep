# Push to GitHub Instructions

## ✅ Git is initialized and ready!

Your code is committed locally. Now follow these steps:

## Option 1: Create Repository on GitHub (Recommended)

### Step 1: Create Repository on GitHub
1. Go to https://github.com/new
2. Repository name: `safe-report` (or any name you like)
3. Description: `Anonymous harassment reporting website with Firebase`
4. Choose **Public** or **Private**
5. **DO NOT** check "Initialize with README" (we already have one)
6. Click **"Create repository"**

### Step 2: Push Your Code

After creating the repository, GitHub will show you commands. Use these:

```bash
git remote add origin https://github.com/YOUR_USERNAME/safe-report.git
git branch -M main
git push -u origin main
```

**Replace `YOUR_USERNAME` with your actual GitHub username!**

## Option 2: Using GitHub CLI (if installed)

```bash
gh repo create safe-report --public --source=. --remote=origin --push
```

## 🎉 After Pushing

Your repository will be live at:
```
https://github.com/YOUR_USERNAME/safe-report
```

## 📝 Next Steps

1. **Add Topics** on GitHub: firebase, harassment-reporting, anonymous, web-app
2. **Enable GitHub Pages** (optional): Settings → Pages → Deploy from main branch
3. **Add Collaborators** (optional): Settings → Collaborators

## ⚠️ Important Security Note

Your Firebase config is in the code, which is SAFE because:
- Firebase API keys are meant to be public
- Security is enforced by Firestore rules, not by hiding keys
- The `.gitignore` file protects sensitive files like `serviceAccountKey.json`

However, if you want extra security, you can:
1. Set up Firebase App Check
2. Add domain restrictions in Firebase Console
3. Use environment variables for production

## 🔄 Future Updates

To push updates to GitHub:

```bash
git add .
git commit -m "Description of changes"
git push
```

## 🆘 Troubleshooting

**"Permission denied"**
- Make sure you're logged into GitHub
- Use HTTPS URL or set up SSH keys

**"Repository not found"**
- Check the repository name is correct
- Make sure you created the repository on GitHub first

**"Failed to push"**
- Try: `git pull origin main --rebase`
- Then: `git push origin main`
