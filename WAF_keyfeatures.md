## 🛡️ Key Features of Azure WAF

### ✅ 1. **Protection Against OWASP Top 10**
- Blocks threats like SQL injection, cross-site scripting (XSS), and remote file inclusion
- Built-in rulesets aligned with OWASP standards

### ✅ 2. **Custom Rules**
- Define your own match conditions based on IP, headers, query strings, or request body
- Supports rate limiting and geo-blocking

### ✅ 3. **Bot Protection**
- Detects and mitigates malicious bots using behavioral analysis
- Integrates with Microsoft Threat Intelligence

### ✅ 4. **DDoS Integration**
- Works seamlessly with **Azure DDoS Protection** for multi-layered defense

### ✅ 5. **TLS Termination and SSL Offloading**
- Handles HTTPS traffic at the edge
- Simplifies certificate management and reduces backend load

### ✅ 6. **Global Deployment via Azure Front Door or Application Gateway**
- Deploy WAF policies across regions for global apps
- Works with both **Front Door** (global edge) and **App Gateway** (regional)

### ✅ 7. **Logging and Monitoring**
- Logs all WAF activity to **Log Analytics**, **Storage**, or **Event Hub**
- Supports diagnostics and alerting via **Azure Monitor**

### ✅ 8. **Managed Rule Sets**
- Microsoft-managed rulesets updated automatically
- Includes **DefaultRuleSet**, **BotRuleSet**, and **CoreRuleSet**

### ✅ 9. **Anomaly Scoring Mode**
- Assigns scores to suspicious requests instead of outright blocking
- Useful for tuning and testing policies

### ✅ 10. **Policy Versioning and Staging**
- Test new rules in staging before enforcing them in production
- Helps avoid false positives

---

Would you like help choosing between **WAF on Front Door vs Application Gateway**, or deploying WAF using Terraform or Bicep? I can guide you through that next.
