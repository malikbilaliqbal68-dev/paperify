# AI Mentor Chat System - No Hosting Required

## 🎯 What You Got

A **ChatGPT-like AI mentor** that guides people conversationally about their career goals.

## 🚀 How to Use

### Option 1: Use the Built-in Chat (Requires Free API)

1. **Get Free API Key:**
   - Go to: https://huggingface.co/settings/tokens
   - Sign up (free)
   - Create new token
   - Copy it

2. **Add to the file:**
   - Open: `views/ai-mentor.ejs`
   - Find line: `const HF_TOKEN = 'hf_YOUR_TOKEN_HERE';`
   - Replace with your token

3. **Test:**
   - Start server: `node index.js`
   - Go to: `http://localhost:3000/ai-mentor`
   - Chat with AI mentor!

### Option 2: Use Without Any Hosting (Recommended)

**Just use these free tools directly:**

#### A) ChatGPT Free
- Go to: https://chat.openai.com
- Copy this prompt:

```
You are an expert career mentor. When I tell you my career goal, guide me step-by-step:

1. Explain what that career is
2. Explain future prospects
3. Give week-by-week learning plan (specific weeks, hours, resources with links)
4. Suggest 5 practical projects
5. Tell where to learn FREE (specific sites)
6. Tell where to host projects FREE
7. Tell where to find freelance work
8. Tell what accounts to create

Be conversational and specific. Use emojis.

My goal: [USER TYPES HERE]
```

#### B) Hugging Face Chat (No API needed)
- Go to: https://huggingface.co/chat
- Free, no login required
- Use same prompt above

#### C) Google Gemini
- Go to: https://gemini.google.com
- Free, unlimited
- Use same prompt

## 📁 Files Created

1. **`views/ai-mentor.ejs`** - Chat interface (needs API key)
2. **`index.js`** - Added route `/ai-mentor`

## 🎓 How It Works

### User visits: `/ai-mentor`
1. Sees chat interface
2. Types: "I want to become a web developer"
3. AI responds with:
   - Career explanation
   - Future prospects
   - Week-by-week plan
   - Free resources
   - Tasks
   - Hosting platforms
   - Freelancing sites

### Fallback System
If API fails, it shows pre-written guidance for common careers.

## 🆓 Free AI Options (No Hosting)

| Tool | Link | Cost | Login |
|------|------|------|-------|
| ChatGPT | chat.openai.com | Free | Yes |
| Gemini | gemini.google.com | Free | Yes |
| HuggingChat | huggingface.co/chat | Free | No |
| Claude | claude.ai | Free | Yes |

## 💡 Best Approach

**Don't host anything!** Just:

1. Create a simple page with a button
2. Button says "Chat with AI Mentor"
3. Button opens: https://huggingface.co/chat
4. Or opens ChatGPT with pre-filled prompt

**No servers, no APIs, no hosting needed!**

## 🔧 Quick Implementation

Add this to your `answer.ejs`:

```html
<a href="https://huggingface.co/chat" target="_blank" class="btn-hero">
    💬 Chat with AI Mentor
</a>
```

Or use ChatGPT:
```html
<a href="https://chat.openai.com" target="_blank" class="btn-hero">
    💬 Chat with AI Mentor
</a>
```

## ✅ Summary

**You have 3 options:**

1. **Use built-in chat** (needs free API key)
2. **Link to HuggingChat** (no setup needed)
3. **Link to ChatGPT/Gemini** (no setup needed)

**Recommendation:** Option 2 or 3 - zero setup, works forever, completely free!
