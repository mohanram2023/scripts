## 🔍 Step 1: Run a Basic Query

Start with a simple query to see recent IIS traffic:

```kql
W3CIISLog
| where TimeGenerated > ago(1h)
| summarize Hits = count() by csUriStem
| order by Hits desc
```

This shows which URLs were accessed most in the past hour.

---

## 🔐 Step 2: Identify Errors or Failures

To find HTTP errors (like 404 or 500):

```kql
W3CIISLog
| where scStatus >= 400
| summarize Count = count() by scStatus, csUriStem
| order by Count desc
```

This helps you spot broken links or server issues.

---

## 📈 Step 3: Visualize Traffic Over Time

```kql
W3CIISLog
| summarize Hits = count() by bin(TimeGenerated, 1h)
| render timechart
```

This gives you a timechart of traffic volume — great for spotting spikes or drops.

---

## 🚨 Step 4: Create Alerts (Optional)

If you want to be notified when something goes wrong:

1. Run a query that detects an issue (e.g., `scStatus == 500`)
2. Click **“New Alert Rule”**
3. Set:
   - **Condition**: e.g., result count > 5
   - **Action Group**: email, SMS, webhook
   - **Severity**: choose based on impact

---

## 📊 Step 5: Build a Dashboard (Optional)

1. Save your favorite queries
2. Click **“Pin to Dashboard”**
3. Use charts and tables to monitor IIS activity visually

Let me know what kind of insights you're looking for — performance, errors, suspicious activity — and I’ll help you craft the perfect query. You're in full control now!
