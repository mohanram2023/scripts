
## 🧱 What You’ll Automate with Terraform

1. **Create a Log Analytics Workspace**
2. **Create a Data Collection Rule (DCR) for IIS logs**
3. **Install Azure Monitor Agent on the VM**
4. **Assign the DCR to your VM**

---

## 🚀 Step-by-Step Terraform Setup

### ✅ 1. Create Log Analytics Workspace
```hcl
resource "azurerm_log_analytics_workspace" "log_workspace" {
  name                = "my-log-workspace"
  location            = "Central India"
  resource_group_name = var.resource_group_name
  sku                 = "PerGB2018"
  retention_in_days   = 30
}
```

---

### ✅ 2. Create Data Collection Rule (DCR)
Terraform doesn’t yet support full DCR configuration natively, but you can use the **azapi_resource** workaround:

```hcl
resource "azapi_resource" "iis_dcr" {
  type      = "Microsoft.Insights/dataCollectionRules@2021-04-01"
  name      = "iis-dcr"
  location  = "Central India"
  parent_id = azurerm_resource_group.rg.id

  body = jsonencode({
    properties = {
      dataSources = {
        iisLogs = [
          {
            streams = ["Microsoft-W3CIISLog"]
            name    = "iislogsource"
          }
        ]
      }
      destinations = {
        logAnalytics = [
          {
            workspaceResourceId = azurerm_log_analytics_workspace.log_workspace.id
            name                = "loganalyticsdest"
          }
        ]
      }
    }
  })
}
```

---

### ✅ 3. Install Azure Monitor Agent on VM
Use the **VM extension** resource:

```hcl
resource "azurerm_virtual_machine_extension" "ama" {
  name                 = "AzureMonitorWindowsAgent"
  virtual_machine_id   = azurerm_windows_virtual_machine.vm.id
  publisher            = "Microsoft.Azure.Monitor"
  type                 = "AzureMonitorWindowsAgent"
  type_handler_version = "1.0"
}
```

---

### ✅ 4. Assign DCR to VM
Use another `azapi_resource` to bind the DCR:

```hcl
resource "azapi_resource" "dcr_assignment" {
  type      = "Microsoft.Insights/dataCollectionRuleAssociations@2021-04-01"
  name      = "dcr-assignment"
  parent_id = azurerm_windows_virtual_machine.vm.id

  body = jsonencode({
    properties = {
      dataCollectionRuleId = azapi_resource.iis_dcr.id
    }
  })
}
```

---

## 🧠 Pro Tips

- Use **Terraform modules** to organize your workspace, VM, and monitoring setup.
- Use **remote state** (e.g., Azure Storage) for team collaboration.
- Consider using **Terraform Cloud** or **Azure DevOps Pipelines** for CI/CD.

---

Would you like me to help you build a complete `.tf` file or integrate this into a pipeline? You're on the edge of full automation!
