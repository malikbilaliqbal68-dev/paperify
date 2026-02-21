# Free AI APIs for Career Guidance System

## 🤖 Best Free AI APIs for Testing & Production

### 1. **Hugging Face Inference API** ⭐ RECOMMENDED
- **Free Tier:** Yes (Rate limited)
- **Models:** GPT-2, BLOOM, Llama, Mistral, and more
- **Setup:**
  ```javascript
  // Get free API key from: https://huggingface.co/settings/tokens
  
  async function getAIFeedback(task, description) {
    const response = await fetch('https://api-inference.huggingface.co/models/mistralai/Mistral-7B-Instruct-v0.1', {
      method: 'POST',
      headers: {
        'Authorization': 'Bearer YOUR_HF_TOKEN',
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({
        inputs: `Review this ${task}: ${description}. Provide strengths, improvements, and score out of 10.`
      })
    });
    return await response.json();
  }
  ```
- **Pros:** Free, many models, good for testing
- **Cons:** Rate limits, slower response
- **Link:** https://huggingface.co/inference-api

### 2. **Google Gemini API** ⭐ BEST FOR PRODUCTION
- **Free Tier:** 60 requests/minute (very generous)
- **Models:** Gemini 1.5 Flash (fast & free)
- **Setup:**
  ```javascript
  // Get free API key from: https://makersuite.google.com/app/apikey
  
  async function getGeminiFeedback(task, description) {
    const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=YOUR_API_KEY`, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        contents: [{
          parts: [{
            text: `You are a career mentor. Review this task: "${task}". Description: "${description}". Provide: 1) Strengths 2) Improvements 3) Next Steps 4) Score (1-10). Be specific and helpful.`
          }]
        }]
      })
    });
    return await response.json();
  }
  ```
- **Pros:** Fast, reliable, generous free tier
- **Cons:** Requires Google account
- **Link:** https://ai.google.dev/

### 3. **OpenAI API** (Limited Free)
- **Free Tier:** $5 credit for new accounts
- **Models:** GPT-3.5-turbo, GPT-4 (paid)
- **Setup:**
  ```javascript
  // Get API key from: https://platform.openai.com/api-keys
  
  async function getOpenAIFeedback(task, description) {
    const response = await fetch('https://api.openai.com/v1/chat/completions', {
      method: 'POST',
      headers: {
        'Authorization': 'Bearer YOUR_OPENAI_KEY',
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({
        model: 'gpt-3.5-turbo',
        messages: [{
          role: 'user',
          content: `Review this task: ${task}. Description: ${description}. Provide strengths, improvements, next steps, and score.`
        }]
      })
    });
    return await response.json();
  }
  ```
- **Pros:** Best quality responses
- **Cons:** Limited free tier, requires payment after $5
- **Link:** https://platform.openai.com/

### 4. **Cohere API**
- **Free Tier:** 100 requests/minute
- **Models:** Command, Generate
- **Setup:**
  ```javascript
  // Get free API key from: https://dashboard.cohere.com/api-keys
  
  async function getCohereFeedback(task, description) {
    const response = await fetch('https://api.cohere.ai/v1/generate', {
      method: 'POST',
      headers: {
        'Authorization': 'Bearer YOUR_COHERE_KEY',
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({
        model: 'command',
        prompt: `Review this task: ${task}. Description: ${description}. Provide feedback.`,
        max_tokens: 300
      })
    });
    return await response.json();
  }
  ```
- **Pros:** Good free tier, fast
- **Cons:** Less popular than others
- **Link:** https://cohere.com/

### 5. **Anthropic Claude API** (Limited Free)
- **Free Tier:** Limited trial credits
- **Models:** Claude 3 Haiku (fastest)
- **Link:** https://www.anthropic.com/api

---

## 🎯 RECOMMENDED IMPLEMENTATION

### Use Google Gemini (Best Free Option)

**Step 1: Get API Key**
1. Go to: https://makersuite.google.com/app/apikey
2. Click "Create API Key"
3. Copy the key

**Step 2: Update index.js**

```javascript
// Add this to your index.js

app.post('/api/task-review', async (req, res) => {
  try {
    const { task, url, description, goal } = req.body;
    
    const GEMINI_API_KEY = process.env.GEMINI_API_KEY || 'YOUR_API_KEY_HERE';
    
    const prompt = `You are an expert career mentor for ${goal}. 
    
A student completed this task: "${task}"
Project URL: ${url || 'Not provided'}
Description: ${description}

Provide detailed feedback in this exact format:
STRENGTHS: [List 2-3 specific things done well]
IMPROVEMENTS: [List 3-4 specific areas to improve]
NEXT_STEPS: [List 2-3 actionable next steps]
SCORE: [Give a score from 1-10]`;

    const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${GEMINI_API_KEY}`, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        contents: [{ parts: [{ text: prompt }] }]
      })
    });
    
    const data = await response.json();
    const aiResponse = data.candidates[0].content.parts[0].text;
    
    // Parse AI response
    const feedback = {
      strengths: aiResponse.match(/STRENGTHS:(.*?)(?=IMPROVEMENTS:|$)/s)?.[1]?.trim() || 'Good work!',
      improvements: aiResponse.match(/IMPROVEMENTS:(.*?)(?=NEXT_STEPS:|$)/s)?.[1]?.trim() || 'Keep practicing',
      nextSteps: aiResponse.match(/NEXT_STEPS:(.*?)(?=SCORE:|$)/s)?.[1]?.trim() || 'Continue learning',
      score: parseInt(aiResponse.match(/SCORE:\s*(\d+)/)?.[1]) || 8
    };
    
    res.json({ success: true, feedback });
  } catch (error) {
    console.error('AI Error:', error);
    // Fallback to rule-based feedback
    res.json({
      success: true,
      feedback: {
        strengths: 'Good effort on completing the task!',
        improvements: 'Add error handling, improve UI/UX, add comments, make it responsive',
        nextSteps: 'Deploy it, add to portfolio, share on LinkedIn',
        score: 8
      }
    });
  }
});
```

**Step 3: Add to .env file**
```
GEMINI_API_KEY=your_actual_api_key_here
```

---

## 📊 Comparison Table

| API | Free Tier | Speed | Quality | Best For |
|-----|-----------|-------|---------|----------|
| **Google Gemini** | 60 req/min | ⚡⚡⚡ | ⭐⭐⭐⭐ | Production |
| **Hugging Face** | Rate limited | ⚡⚡ | ⭐⭐⭐ | Testing |
| **OpenAI** | $5 credit | ⚡⚡⚡ | ⭐⭐⭐⭐⭐ | Premium |
| **Cohere** | 100 req/min | ⚡⚡⚡ | ⭐⭐⭐ | Alternative |

---

## 🚀 Quick Start (5 Minutes)

1. **Get Gemini API Key:**
   - Visit: https://makersuite.google.com/app/apikey
   - Sign in with Google
   - Click "Create API Key"
   - Copy the key

2. **Add to your project:**
   - Create `.env` file in project root
   - Add: `GEMINI_API_KEY=your_key_here`
   - Update `index.js` with the code above

3. **Test it:**
   - Go to `/roadmap?goal=web developer`
   - Submit a task
   - Get AI-powered feedback!

---

## 💡 Tips

1. **Always have a fallback:** If AI API fails, use rule-based feedback
2. **Cache responses:** Store common feedback to reduce API calls
3. **Rate limiting:** Implement rate limiting to avoid hitting API limits
4. **Error handling:** Always catch errors and provide user-friendly messages
5. **Environment variables:** Never commit API keys to GitHub

---

## 🔒 Security Best Practices

```javascript
// ✅ GOOD - Use environment variables
const API_KEY = process.env.GEMINI_API_KEY;

// ❌ BAD - Never hardcode API keys
const API_KEY = 'AIzaSyC...'; // DON'T DO THIS!

// ✅ GOOD - Add to .gitignore
// .gitignore file:
.env
.env.local
```

---

## 📞 Support Links

- **Gemini API Docs:** https://ai.google.dev/docs
- **Hugging Face Docs:** https://huggingface.co/docs/api-inference
- **OpenAI Docs:** https://platform.openai.com/docs
- **Cohere Docs:** https://docs.cohere.com/

---

**Recommendation:** Start with **Google Gemini API** - it's free, fast, and perfect for your use case!
