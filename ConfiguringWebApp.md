# Configuring the Web App in the Azure Portal

## Post VS Code Deployment
  
#### Get Log Analytics Workspace ID and Key
1. In Azure, navigate to the Log Analytics Workspace that is connected to your Sentinel.
2. From the menu on the left, under Settings, select **Agents > Linux servers > Log Analytics agent instructions**.
3. Copy the Workspace ID and Primary Key values as you will need them later.
  
#### Save Values to Key Vault (*optional*)
1. In Azure, navigate to the web app.  
2. Select **Settings > Identity > System assigned**, change **Status** to **On**.  
3. **Save** and acknowledge any further prompts.  
4. In Azure, navigate to the Azure Key Vault where you will store the values from the previous step.  
5. From the menu on the left, under Objects, select **Secrets > Generate/Import**. 
6. Enter a name for Workspace ID. eg *LogAnalytics-WorkspaceID*. 
7. Paste the Workspace ID  of your Log Analytics Workspace. 
8. Select **Create**.  
9. Again, select **Secrets > Generate/Import**. 
10. Enter a name for the Primary Key (this will later be referred to as the SHARED_KEY). eg *LogAnalytics-PrimaryKey*.
11. Paste the Primary Key for Log Analytics Workspace. 
12. Select **Create**.
13. For each secret, copy the *Secret Identifier URI*.  
14. Assign 'Secret-GET' permissions to the web app using the system assigned identity. This will either be done from Access Control or Access Policies.
For more information [About Azure Key Vault | Microsoft Learn](https://learn.microsoft.com/en-gb/azure/key-vault/general/overview)

#### Create Environment Variables
1. In Azure, navigate to the web app.  
2. Select **Settings > Environment Variables> Add**.
3. In the name field, enter "WORKSPACE_ID".
4. In the value field, paste the Workspace ID  of your Log Analytics Workspace 
   OR  
   If storing value in Key Vault, enter "@Microsoft.KeyVault(SecretUri=*https://yourkeyvaulturiforworkspaceid*)".
5. Select **Add**.
6. In the name field, enter "SHARED_KEY".
7. In the value field, paste the Primary Key of your Log Analytics Workspace. 
   OR  
   If storing value in Key Vault, enter "@Microsoft.KeyVault(SecretUri=*https://yourkeyvaulturifortheprimarykey*)"  
8. Select **Apply**.

#### Send Logs from your WebApp to your Log Analytics Workspace
1. In Azure, navigate to the web app.  
2. Select **Monitoring > Diagnostic Settings**.
3. Select *Add diagnostic setting*.
4. Enter a Diagnostic setting name.
5. Tick all boxes under Logs and Metrics.
6. Under Destination details, tick 'Send to Log Analytics Workspace' > Select the correct log analytic workspace from dropdown.
7. Select **Save**

## Post Configuring HTTPS Forwarding Profile

#### Secure your web app
Once you have configured the log forwarding profile and you can see logs in your Log Analytics, lock down access to the Public IP using networking rules.
1. In Azure, navigate to the Logs space of your Log Analytics Workspace.
2. Run the following search:

```
AppServiceHTTPLogs
| summarize by CIp

```
3. In Azure, navigate to the web app.
4. Select **Settings > Networking**.
5. Under **Inbound traffic configuration**, select *Enabled with no access restrictions*.
6. Under **App Access**, Select *'Enabled from select virtual netowrks and IP addresses'*.
7. Under **Site Access and Rules** > **Main site**.
8. Set 'Unmatched rule action' to **Deny**.
9. Select **Add**.
10. Add a rule to allow each IP address from the log search.
11.  Under **Site Access and Rules** > **Advanced tool site**.
12.  Set 'Unmatched rule action' to **Deny**.
13.  Select '*Use main site rules*'.
14.  Select **Save**.
