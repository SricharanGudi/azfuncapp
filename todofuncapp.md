
# Azure Function App Deployment Guide (VS Code)

 create a Python-based Azure Function App and deploy it to **Azure** using **Visual Studio Code (VS Code)**.

---

## Prerequisites

Before starting, ensure the following are installed:

- [Python 3.9+](https://www.python.org/)
- [Node.js (LTS)](https://nodejs.org/)
- [Azure Functions Core Tools](https://learn.microsoft.com/en-us/azure/azure-functions/functions-run-local)
- [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli)
- [VS Code](https://code.visualstudio.com/)
- VS Code Extensions:
  - Azure Functions
  - Azure Account
  - Python

---

## 1 Sign In to Azure

```bash
# Sign in using Azure CLI
az login
```

1. Open VS Code.
2. Click the **Azure icon** on the left Activity Bar.
3. Click **"Sign in to Azure"**.
4. Complete login in the browser popup.
5. You should now see your Azure subscriptions listed.

---

## 2 Create a Python Azure Function App (Locally)

```bash
# Create a function app project
func init my-function-app --python
cd my-function-app

# Create a new HTTP-triggered function
func new
# Choose: HTTP trigger, name: TodoFunction, Authorization level: Anonymous
```

---

## 3 Run & Test Your App Locally

```bash
# Start local server
func start
```

Visit in browser or Postman:

```http
http://localhost:7071/api/TodoFunction
```

---

## 4 Create Azure Resources (Optional)

You’ll need:

```bash
# Create resource group
az group create --name myResourceGroup --location eastus

# Create storage account (if not already created)
az storage account create --name mystorageacct --location eastus --resource-group myResourceGroup --sku Standard_LRS

# Create the Function App
az functionapp create --resource-group myResourceGroup --consumption-plan-location eastus --runtime python --runtime-version 3.9 --functions-version 4 --name todo-charan-func --storage-account mystorageacct
```

---

## 5 Deploy to Azure from VS Code

1. Open the **Azure tab** in VS Code.
2. Click the **“Deploy to Function App…”** icon (cloud with up arrow).
3. Select your project folder.
4. Select:
   - Existing Function App, or
   - **+ Create New Function App**
     - Name: `todo-charan-func`
     - Runtime: Python
     - Region: East US
     - Use existing Storage Account
5. Confirm deployment when prompted.

---

## 6 Get the Function URL

In the Azure portal:

```text
Azure Portal → Function App → Functions → Click your Function → Get Function URL
```

Example URL:

```
https://todo-charan-func.azurewebsites.net/api/TodoFunction
```

---

## 7 Test Function App (Deployed)

Using Postman:

- Method: **GET** or **POST**
- URL: `https://todo-charan-func.azurewebsites.net/api/TodoFunction`
- For POST: raw JSON body
```json
{ "name": "Sricharan" }
```

Expected Output:

```
Hello, Sricharan. This HTTP triggered function executed successfully.
```

---

## Project Structure

```bash
my-function-app/
├── TodoFunction/
│   ├── __init__.py
│   └── function.json
├── host.json
├── requirements.txt
```

---

## Useful CLI Commands

```bash
# Login to Azure
az login

# Create a resource group
az group create --name myResourceGroup --location eastus

# Create a storage account
az storage account create --name mystorageacct --location eastus --resource-group myResourceGroup --sku Standard_LRS

# Create a Function App
az functionapp create --resource-group myResourceGroup --consumption-plan-location eastus --runtime python --runtime-version 3.9 --functions-version 4 --name todo-charan-func --storage-account mystorageacct

# Deploy manually from terminal (optional)
func azure functionapp publish todo-charan-func
```

---

> by Sricharan
