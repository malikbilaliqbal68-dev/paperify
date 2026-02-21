# Fraud Protection Features

## ✅ Implemented Protections

### 1️⃣ Transaction ID Uniqueness Check
**Status:** ✅ Active

**What it does:**
- Checks if transaction ID was already used
- Prevents receipt reuse (common fraud)
- Searches both payment_links and payments tables

**Code location:** `index.js` - `/api/payment/submit/:linkId`

**Error message:** "Transaction ID already used. Each payment must be unique."

### 2️⃣ Payment Time Validation (Recommended)
**Status:** ⚠️ Not implemented yet

**How to add:**
```javascript
// In payment submission
const { transactionId, paymentTime } = req.body;

// Check if payment is recent (within 30 minutes)
const paymentDate = new Date(paymentTime);
const now = new Date();
const diffMinutes = (now - paymentDate) / (1000 * 60);

if (diffMinutes > 30) {
  return res.status(400).json({
    success: false,
    error: 'Payment must be within last 30 minutes. Old receipts not accepted.'
  });
}
```

**Why it helps:**
- Fraudsters often upload old receipts
- Forces fresh payments only
- Easy to verify in admin panel

### 3️⃣ Admin Fraud Flags (Recommended)
**Status:** ⚠️ Not implemented yet

**How to add to admin panel:**

Add these buttons in `admin-payments.ejs`:

```html
<button onclick="flagSuspicious('${payment.link_id}')" 
        class="px-3 py-1 bg-orange-500 text-white rounded text-xs">
    🚩 Flag Suspicious
</button>
<button onclick="requestNewProof('${payment.link_id}')" 
        class="px-3 py-1 bg-yellow-500 text-white rounded text-xs">
    🔁 Request New Proof
</button>
<button onclick="blockUser('${payment.user_email}')" 
        class="px-3 py-1 bg-red-500 text-white rounded text-xs">
    🚫 Block User
</button>
```

Add API endpoints:

```javascript
// Flag suspicious payment
app.post('/api/admin/flag-suspicious/:linkId', async (req, res) => {
  // Admin only check
  await updatePaymentLink(linkId, 'flagged_suspicious');
  res.json({ success: true });
});

// Request new proof
app.post('/api/admin/request-new-proof/:linkId', async (req, res) => {
  // Admin only check
  await updatePaymentLink(linkId, 'proof_requested');
  // Send email to user
  res.json({ success: true });
});

// Block user
app.post('/api/admin/block-user', async (req, res) => {
  const { email } = req.body;
  // Add to blocked_users table
  res.json({ success: true });
});
```

## 🛡️ Additional Protections to Consider

### 4️⃣ Rate Limiting
Prevent spam submissions:
```bash
npm install express-rate-limit
```

```javascript
import rateLimit from 'express-rate-limit';

const paymentLimiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 3, // 3 payment submissions per 15 min
  message: 'Too many payment attempts. Try again later.'
});

app.post('/api/payment/submit/:linkId', paymentLimiter, upload.single('screenshot'), ...);
```

### 5️⃣ Screenshot Metadata Check
Check if image was recently taken:

```javascript
import exif from 'exif-parser';

const buffer = fs.readFileSync(screenshot.path);
const parser = exif.create(buffer);
const result = parser.parse();

if (result.tags.CreateDate) {
  const imageDate = new Date(result.tags.CreateDate * 1000);
  const now = new Date();
  const hoursDiff = (now - imageDate) / (1000 * 60 * 60);
  
  if (hoursDiff > 1) {
    // Screenshot is old, flag for review
  }
}
```

### 6️⃣ Amount Verification
Cross-check submitted amount with plan amount:

```javascript
// Already in payment link
if (link.amount !== expectedAmount) {
  return res.status(400).json({
    error: 'Payment amount mismatch'
  });
}
```

### 7️⃣ User Behavior Tracking
Track suspicious patterns:
- Multiple failed payments
- Different transaction IDs for same amount
- Rapid submission attempts
- Using VPN/proxy

## 📊 Fraud Detection Checklist

When reviewing payments, check:

- [ ] Transaction ID format looks valid
- [ ] Screenshot shows correct amount
- [ ] Screenshot shows correct payment number
- [ ] Screenshot timestamp is recent
- [ ] User email matches payment details
- [ ] No previous fraud from this user
- [ ] Transaction ID not found in your wallet yet
- [ ] Image quality is good (not blurry/edited)

## 🚨 Red Flags to Watch For

1. **Blurry screenshots** - Often edited
2. **Old timestamps** - Reused receipts
3. **Wrong amount** - Trying to pay less
4. **Multiple submissions** - Testing the system
5. **Suspicious email patterns** - temp-mail services
6. **VPN usage** - Hiding location
7. **Mismatched details** - Name/email don't match

## 💡 Best Practices

1. **Always verify in your actual wallet** before approving
2. **Keep records** of all transaction IDs
3. **Document fraud attempts** to spot patterns
4. **Respond quickly** to legitimate users
5. **Be strict** with suspicious cases
6. **Refund genuine mistakes** to build trust

## 🎯 Current Protection Level

| Protection | Status | Effectiveness |
|------------|--------|---------------|
| Transaction ID uniqueness | ✅ Active | High |
| Screenshot required | ✅ Active | Medium |
| Admin verification | ✅ Active | High |
| Payment time check | ⚠️ Recommended | Medium |
| Fraud flags | ⚠️ Recommended | Medium |
| Rate limiting | ❌ Not added | High |
| Metadata check | ❌ Not added | Low |

**Overall:** Good for MVP, improve as you scale.
