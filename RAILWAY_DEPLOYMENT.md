# 🚀 Railway Deployment Guide - Paperify

Complete step-by-step guide to deploy your website on Railway.

---

## 📋 STEP 1: Push Code to GitHub

### Option A: Git Command Line (Recommended)
```bash
cd "d:\Real web"
git init
git add .
git commit -m "Initial deployment"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
git push -u origin main
```

### Option B: GitHub Web Upload
1. Go to https://github.com/new
2. Create new repository (e.g., "paperify")
3. Drag and drop your `Real web` folder
4. Click "Commit changes"

---

## 🔐 STEP 2: Generate Secret Keys

Open Command Prompt and run:

```bash
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
```

Run this command **TWICE** to get two different secrets:
- First output = SESSION_SECRET
- Second output = PAYMENT_SECRET

**Save these somewhere safe!** You'll need them in Step 4.

---

## 🚂 STEP 3: Deploy on Railway

1. **Go to Railway**
   - Visit: https://railway.app
   - Click "Login" → Sign in with GitHub

2. **Create New Project**
   - Click "New Project"
   - Select "Deploy from GitHub repo"
   - Choose your repository (e.g., "paperify")
   - Railway will start deploying automatically

3. **Wait for Initial Deploy**
   - This will take 2-3 minutes
   - You'll see build logs in real-time
   - **It will FAIL first time** - that's normal! (Missing environment variables)

---

## ⚙️ STEP 4: Add Environment Variables

1. **Click on your project** in Railway dashboard

2. **Go to Variables tab**

3. **Add these variables** (click "New Variable" for each):

```
NODE_ENV=production
SESSION_SECRET=<paste your first secret from Step 2>
PAYMENT_SECRET=<paste your second secret from Step 2>
SUPERUSER_EMAIL=bilal@paperify.com
PAYMENT_NUMBER=03448007154
PORT=3000
```

**Important:** Replace the secrets with YOUR generated values from Step 2!

4. **Click "Deploy"** or wait for auto-redeploy

---

## 🌐 STEP 5: Get Your Live URL

1. **Go to Settings tab** in Railway

2. **Scroll to "Networking" section**

3. **Click "Generate Domain"**

4. **Copy your URL** (e.g., `paperify-production.up.railway.app`)

5. **Visit your live site!** 🎉

---

## ✅ STEP 6: Verify Everything Works

Test these features on your live site:

### 1. Homepage
- [ ] Visit your Railway URL
- [ ] Check if page loads correctly

### 2. User Registration
- [ ] Click "Sign Up"
- [ ] Create a test account
- [ ] Verify you can login

### 3. Demo Papers
- [ ] Select Punjab board
- [ ] Select Class 9
- [ ] Generate a demo paper
- [ ] Verify it generates correctly

### 4. Payment System
- [ ] Click "Pricing"
- [ ] Select a plan
- [ ] Verify payment link generates
- [ ] Check payment number shows: 03448007154

### 5. Referral System
- [ ] Login to your account
- [ ] Check if referral code is displayed
- [ ] Verify referral progress shows "0/10"

### 6. Database Persistence
- [ ] Create an account
- [ ] Logout and login again
- [ ] Verify your account still exists (data persists)

---

## 🔧 STEP 7: Update Payment Number (Optional)

If you want to change the payment number:

1. Go to Railway dashboard
2. Click "Variables" tab
3. Find `PAYMENT_NUMBER`
4. Change to your number
5. Click "Deploy"

---

## 📊 Monitor Your Site

### View Logs
1. Click "Deployments" tab
2. Click on latest deployment
3. Click "View Logs"
4. Monitor for errors

### Check Database
- Railway automatically creates SQLite database
- Data persists between restarts
- Located at: `/app/data/paperify.db`

---

## 🐛 Troubleshooting

### Site Not Loading?
- Check deployment logs for errors
- Verify all environment variables are set
- Make sure PORT=3000 is set

### Database Errors?
- Railway creates `data/` folder automatically
- Database initializes on first run
- Check logs for "Database initialized" message

### Payment Links Not Working?
- Verify PAYMENT_SECRET is set (32+ characters)
- Check PAYMENT_NUMBER is correct
- Test with a real user account

### Session Errors?
- Verify SESSION_SECRET is set (32+ characters)
- Clear browser cookies
- Try incognito/private mode

---

## 🔄 Update Your Site

When you make changes:

```bash
cd "d:\Real web"
git add .
git commit -m "Update description"
git push
```

Railway automatically redeploys when you push to GitHub!

---

## 💰 Pricing

Railway offers:
- **$5/month** for Hobby plan
- **$0.000231/GB-hour** for database storage
- **Free trial** with $5 credit

Your site should cost **~$5-7/month** depending on traffic.

---

## 📞 Support

If you need help:
1. Check Railway logs first
2. Review this guide
3. Check Railway documentation: https://docs.railway.app

---

## ✨ Your Site is Live!

**Congratulations!** Your Paperify website is now deployed on Railway! 🎊

Share your URL with users and start generating papers!

**Live URL:** `https://your-project.up.railway.app`

---

## 🎯 Next Steps

1. ✅ Test all features thoroughly
2. ✅ Share your site with friends
3. ✅ Monitor usage and errors
4. ✅ Update pricing if needed
5. ✅ Add more syllabus content
6. ✅ Promote your site!

**Your educational platform is ready to help students! 🎓**
