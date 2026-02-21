# Payment Gateway Upgrade Guide

## When to Upgrade from Manual to Automated

Upgrade when you hit ANY of these milestones:
- 50+ transactions per day
- Can't manually review all payments
- Need instant activation
- Want to scale business
- Getting fraud attempts

## Step-by-Step Upgrade Path

### Phase 1: Apply for Merchant Account (Week 1-2)

**EasyPaisa:**
1. Visit https://easypaisa.com.pk/business
2. Apply for merchant account
3. Submit business documents
4. Wait for approval (7-14 days)

**JazzCash:**
1. Visit https://jazzcash.com.pk/business
2. Register as merchant
3. Complete KYC verification
4. Get API credentials

### Phase 2: Get API Credentials (Week 2-3)

You'll receive:
- Merchant ID
- API Key
- API Secret
- Webhook URL endpoint
- Test environment access

### Phase 3: Code Integration (Week 3-4)

**Install SDK:**
```bash
npm install easypay-sdk
# or
npm install jazzcash-api
```

**Replace manual flow with API:**

```javascript
// OLD: Manual verification
await submitPaymentProof(linkId, transactionId, screenshot);

// NEW: Automatic verification
const payment = await easypaisa.createPayment({
  amount: 1200,
  orderId: linkId,
  customerEmail: userEmail,
  webhookUrl: 'https://yoursite.com/webhook/payment'
});
```

### Phase 4: Webhook Handler (Week 4)

```javascript
app.post('/webhook/payment', async (req, res) => {
  const { transactionId, status, orderId } = req.body;
  
  // Verify webhook signature
  if (!verifyWebhookSignature(req)) {
    return res.status(401).send('Invalid signature');
  }
  
  if (status === 'SUCCESS') {
    // Auto-activate subscription
    await markPaymentComplete(orderId);
    await activateSubscription(orderId);
  }
  
  res.status(200).send('OK');
});
```

### Phase 5: Remove Manual Steps (Week 5)

Delete/disable:
- Screenshot upload requirement
- Admin approval endpoint
- Manual verification UI

### Phase 6: Testing (Week 5-6)

1. Test in sandbox environment
2. Try small real transactions
3. Verify webhooks work
4. Test refund flow
5. Load test with multiple payments

### Phase 7: Go Live (Week 6)

1. Switch to production API keys
2. Update environment variables
3. Monitor first 100 transactions closely
4. Keep manual system as backup for 1 month

## Cost Comparison

### Current System (Manual)
- Setup: PKR 0
- Per transaction: PKR 0
- Admin time: 5 min/payment
- Monthly cost: Your time only

### EasyPaisa/JazzCash Gateway
- Setup: PKR 5,000 - 20,000
- Per transaction: 1.5% - 2.5%
- Admin time: 0 min/payment
- Monthly cost: Transaction fees only

### Example at 1000 transactions/month:
- Manual: 5000 minutes = 83 hours of your time
- Gateway: PKR 18,000 - 30,000 in fees
- **Gateway becomes cheaper when your time is valuable**

## Code Changes Required

### 1. Update payment-page.ejs
```html
<!-- Remove screenshot upload -->
<!-- Add payment gateway redirect button -->
<button onclick="redirectToGateway()">
  Pay with EasyPaisa
</button>
```

### 2. Update index.js
```javascript
// Remove manual submission endpoint
// Add gateway redirect endpoint
app.post('/api/payment/initiate', async (req, res) => {
  const paymentUrl = await gateway.createPayment({...});
  res.json({ redirectUrl: paymentUrl });
});

// Add webhook handler
app.post('/webhook/payment', verifyWebhook, async (req, res) => {
  // Auto-activate on success
});
```

### 3. Remove admin approval
```javascript
// Delete or comment out
// app.post('/api/payment/confirm/:linkId', ...)
```

## Testing Checklist

- [ ] Sandbox payment works
- [ ] Webhook receives callbacks
- [ ] Subscription activates automatically
- [ ] Failed payments handled correctly
- [ ] Refunds work
- [ ] Multiple simultaneous payments
- [ ] Payment link expiration
- [ ] Duplicate payment prevention

## Rollback Plan

If gateway integration fails:
1. Keep manual system code
2. Add feature flag: `USE_MANUAL_PAYMENTS=true`
3. Switch back to manual if needed
4. Fix issues in staging
5. Try again

## Support Resources

**EasyPaisa:**
- Docs: https://easypaisa.com.pk/developers
- Support: merchant@easypaisa.com.pk
- Phone: 111-003-947

**JazzCash:**
- Docs: https://developer.jazzcash.com.pk
- Support: merchant@jazzcash.com.pk
- Phone: 111-124-444

**Stripe (if available):**
- Docs: https://stripe.com/docs
- Support: https://support.stripe.com
- Very detailed documentation

## Timeline Summary

| Week | Task | Status |
|------|------|--------|
| 1-2 | Apply for merchant account | ⏳ |
| 2-3 | Get API credentials | ⏳ |
| 3-4 | Code integration | ⏳ |
| 4 | Webhook setup | ⏳ |
| 5 | Remove manual steps | ⏳ |
| 5-6 | Testing | ⏳ |
| 6 | Go live | ⏳ |

**Total time: 6-8 weeks**

## Final Notes

- Don't rush the upgrade
- Test thoroughly in sandbox
- Keep manual system as backup initially
- Monitor closely after launch
- Have rollback plan ready

Good luck! 🚀
