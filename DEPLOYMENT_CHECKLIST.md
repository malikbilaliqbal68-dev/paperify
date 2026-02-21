# ✅ Railway Deployment Checklist

Quick checklist to deploy Paperify on Railway.

---

## Before You Start

- [ ] Code is ready in `d:\Real web` folder
- [ ] Video file deleted (65MB demo.mp4)
- [ ] All Punjab files split (under 1MB each)
- [ ] GitHub account created
- [ ] Railway account created (sign up at railway.app)

---

## Deployment Steps

### 1️⃣ Push to GitHub
```bash
cd "d:\Real web"
git init
git add .
git commit -m "Deploy Paperify"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/paperify.git
git push -u origin main
```
- [ ] Code pushed to GitHub successfully

---

### 2️⃣ Generate Secrets
```bash
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
```
Run twice and save both outputs:
- [ ] SESSION_SECRET generated
- [ ] PAYMENT_SECRET generated

---

### 3️⃣ Deploy on Railway
1. Go to https://railway.app
2. Login with GitHub
3. Click "New Project"
4. Select "Deploy from GitHub repo"
5. Choose your repository

- [ ] Project created on Railway
- [ ] Initial deployment started

---

### 4️⃣ Add Environment Variables

Go to Variables tab and add:

```
NODE_ENV=production
SESSION_SECRET=<your first secret>
PAYMENT_SECRET=<your second secret>
SUPERUSER_EMAIL=bilal@paperify.com
PAYMENT_NUMBER=03448007154
PORT=3000
```

- [ ] All 6 variables added
- [ ] Deployment restarted automatically

---

### 5️⃣ Generate Domain

1. Go to Settings tab
2. Scroll to "Networking"
3. Click "Generate Domain"

- [ ] Domain generated
- [ ] Site is live!

---

### 6️⃣ Test Your Site

Visit your Railway URL and test:

- [ ] Homepage loads
- [ ] Can register new account
- [ ] Can login
- [ ] Can generate demo paper
- [ ] Payment links work
- [ ] Referral code shows
- [ ] Database persists data

---

## 🎉 Done!

Your site is live at: `https://your-project.up.railway.app`

**Cost:** ~$5-7/month

**Updates:** Just push to GitHub, Railway auto-deploys!

---

## Quick Commands

### Update site:
```bash
cd "d:\Real web"
git add .
git commit -m "Update"
git push
```

### View logs:
Go to Railway → Deployments → View Logs

### Change payment number:
Railway → Variables → Edit PAYMENT_NUMBER → Deploy

---

## Need Help?

Read full guide: `RAILWAY_DEPLOYMENT.md`
