# Proxy template to decompress data from CDL for ingestion into Azure Sentinel

## About
This application leverages the Azure HTTP Data Collector API (depreciated) to send log data to Azure Monitor from a REST API client. This API and Web Application has been depreciated and will no longer be functional as of 9/14/2026.  
[Send log data to Azure Monitor by using the HTTP Data Collector API | Microsoft Learn](https://learn.microsoft.com/en-us/previous-versions/azure/azure-monitor/logs/data-collector-api?tabs=python)


### Deploy a Python (Flask) web app to Azure App Service - Sample Application

This is the sample Flask application for the Azure Quickstart [Deploy a Python (Django or Flask) web app to Azure App Service](https://docs.microsoft.com/en-us/azure/app-service/quickstart-python).  For instructions on how to create the Azure resources and deploy the application to Azure, refer to the Quickstart article.

A Django sample application is also available for the article at [https://github.com/Azure-Samples/msdocs-python-django-webapp-quickstart](https://github.com/Azure-Samples/msdocs-python-django-webapp-quickstart).

If you need an Azure account, you can [create one for free](https://azure.microsoft.com/en-us/free/).


## Pre-Requisties:

Configure the following variables (Store the secrets in Key vault or directly pass the values) for Azure Sentinel interaction after navigating to application settings (Web app -> Configuration -> Application Settings),

Name: WORKSPACE_ID  
Value: @Microsoft.KeyVault(SecretUri=<vault URI>)  

Name: SHARED_KEY  
Value: @Microsoft.KeyVault(SecretUri=<vault URI>)  

Key vault settings: 
https://docs.microsoft.com/en-us/azure/app-service/overview-managed-identity?tabs=portal%2Chttp


### Deploying through Visual Studio Code:

1. Install Visual Studio Code Version >= 1.64.1  
2. Install Extensions Azure Tools, Azure App Service in Visual Studio Code  
3. git clone https://github.com/PaloAltoNetworks/cdl-decompress-proxy-sentinel-ingest.git  
4. Open the folder cdl-decompress-proxy-sentinel-ingest in Visual Studio Code  
5. Click the Azure Icon, Sign Into Azure -> `Create new Web App`  
6. Right Click the Web App created and chose `Deploy to Web App`


## Additional Resources
[Set Up HTTPS Log Forwarding to Microsoft Sentinel | Prisma Access](https://docs.paloaltonetworks.com/strata-logging-service/administration/forward-logs/forward-logs-to-an-https-server#id4a2daeef-8e7d-4d7c-a5ac-3b37338592af_ul-rgq_fdt_11c)  
[Forward Logs to an HTTPS Server | Strata Logging Service](https://docs.paloaltonetworks.com/prisma-access/integration/microsoft-integrations-with-prisma-access/set-up-https-log-forwarding-to-microsoft-sentinel)  
[Configure a Linux Python app for Azure App Service | Microsoft Learn](https://learn.microsoft.com/en-us/azure/app-service/configure-language-python)

