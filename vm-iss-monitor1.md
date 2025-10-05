

## 🚀 Step-by-Step: Connect IIS Logs to Log Analytics Workspace

### ✅ Step 1: Install Azure Monitor Agent on the VM
1. Go to **Azure Portal**
2. Navigate to your **Virtual Machine**
3. In the left menu, click **Extensions + applications**
4. Click **+ Add**
5. Select **Azure Monitor Agent** and install it

> This agent is required to send logs to your workspace.

---

### 📋 Step 2: Create a Data Collection Rule (DCR)
1. Go to **Monitor** > **Data Collection Rules**
2. Click **+ Create**
3. Fill in:
   - **Name**: e.g., `IISLogDCR`
   - **Platform**: Windows
   - **Data Sources**: Select **IIS Logs**
   - **Destination**: Choose your **Log Analytics Workspace**
4. Assign the rule to your VM

> This rule tells Azure what data to collect and where to send it.

---

### 🔍 Step 3: Verify IIS Logging Is Enabled
On your VM:
1. Open **IIS Manager**
2. Select your site > Click **Logging**
3. Ensure **W3C format** is selected
4. Confirm log files are being written locally

---

### 📊 Step 4: Check Logs in Log Analytics
After a few minutes, go to your **Log Analytics Workspace** > **Logs**, and run:
```kql
W3CIISLog
| where csUriStem contains "/"
| summarize Hits = count() by csUriStem
```



