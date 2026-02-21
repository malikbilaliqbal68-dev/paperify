# AI Mentor - Final Setup Guide

## ✅ What You Have Now

An AI chat mentor that works **in the background** on your website - users never leave your site!

## 🚀 Quick Setup (5 Minutes)

### Step 1: Get Free Gemini API Key
```
1. Go to: https://makersuite.google.com/app/apikey
2. Sign in with Google
3. Click "Create API Key"
4. Copy the key
```

### Step 2: Add API Key
Open: `views/ai-mentor.ejs`

Find line 155:
```javascript
const GEMINI_API_KEY = 'YOUR_API_KEY_HERE';
```

Replace with your key:
```javascript
const GEMINI_API_KEY = 'AIzaSyC...your_actual_key';
```

### Step 3: Test
```bash
node index.js
```

Go to: `http://localhost:3000/ai-mentor`

## 🎯 How It Works

1. User visits `/ai-mentor`
2. Types: "I want to become a web developer"
3. **AI responds in background** (never leaves your site)
4. User gets complete guidance:
   - Career explanation
   - Week-by-week plan
   - Free resources
   - Projects to build
   - Hosting platforms
   - Freelancing sites

## 💡 Features

✅ **Works in background** - AI calls happen behind the scenes
✅ **Never leaves your site** - Users stay on your domain
✅ **Free API** - 60 requests/minute (Gemini)
✅ **Fallback system** - Works even without API key
✅ **Beautiful chat UI** - Professional design
✅ **Mobile responsive** - Works on all devices

## 🆓 Free API Details

**Google Gemini:**
- Free tier: 60 requests/minute
- No credit card required
- Fast responses
- High quality

**Fallback:**
If API fails or no key provided, shows pre-written guidance for:
- Web Developer
- Graphic Designer
- Generic careers

## 📱 User Experience

```
User: "I want to become a web developer"
  ↓
AI (in background): Calls Gemini API
  ↓
Response appears in chat:
  ✅ Career explanation
  ✅ Week-by-week plan (24 weeks)
  ✅ Free resources with links
  ✅ 5 projects to build
  ✅ Free hosting platforms
  ✅ Freelancing sites
  ✅ Account creation guide
```

## 🔧 Files

1. `views/ai-mentor.ejs` - Chat interface
2. `index.js` - Route added (`/ai-mentor`)

## 🎓 Access Points

Add link anywhere:
```html
<a href="/ai-mentor">Chat with AI Mentor</a>
```

Or button:
```html
<button onclick="window.location='/ai-mentor'">
    💬 AI Career Mentor
</button>
```

## ✨ What Makes This Special

1. **Background processing** - AI works behind the scenes
2. **No redirects** - Users never leave your site
3. **Free forever** - Gemini API is free
4. **Smart fallback** - Works without API too
5. **Professional UI** - Looks like ChatGPT

## 🎯 Summary

**Before:** Users had to go to ChatGPT/Gemini websites

**Now:** AI mentor works directly on YOUR website in the background!

**Setup time:** 5 minutes
**Cost:** $0 (free forever)
**User experience:** Professional and seamless

---

**Ready to use! Just add your Gemini API key and test it!** 🚀
