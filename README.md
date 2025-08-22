# AEM Azure Project – Portfolio Deployment 🚀

This project demonstrates **building and deploying an ASP.NET Core web app** to **Azure App Service** with **GitHub Actions (CI/CD)**.  
It is part of my academic project work on **cloud-based deployment automation**.

---

## 📌 Overview
- **Framework**: ASP.NET Core (.NET 8 LTS)  
- **Cloud Provider**: Azure App Service  
- **CI/CD Tool**: GitHub Actions  
- **App Name**: `shreyakwebapp`  
- **Deployment URL**: [https://shreyakwebapp.azurewebsites.net](https://shreyakwebapp.azurewebsites.net)

---

## ⚙️ Prerequisites
- [.NET 8 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/8.0)  
- [Visual Studio Code](https://code.visualstudio.com/)  
- [Git](https://git-scm.com/)  
- [Azure Account / Sandbox](https://aka.ms/az900/sandbox)  
- GitHub repository (this repo)

---

---

## 🖥️ Run Locally
```bash
# Clone repo
git clone https://github.com/shreyakmukherjee/aem_azure_project_portfolio.git
cd aem_azure_project_portfolio

# Restore dependencies
dotnet restore

# Run locally
dotnet run
```

➡ Open http://localhost:5001 in your browser.

🚀 Deploy to Azure (CI/CD with GitHub Actions)

This project uses a GitHub Actions workflow to automatically deploy on every push to main.

📌 Workflow file: .github/workflows/azure-webapp.yml

```bash
name: Build and deploy ASP.Net Core app to Azure Web App - shreyakwebapp

on:
  push:
    branches: [ main ]
  workflow_dispatch:

jobs:
  build:
    runs-on: windows-latest
    steps:
      - uses: actions/checkout@v4
      - name: Set up .NET Core
        uses: actions/setup-dotnet@v4
        with:
          dotnet-version: '8.x'
      - name: Build
        run: dotnet build --configuration Release
      - name: Publish
        run: dotnet publish -c Release -o "${{env.DOTNET_ROOT}}/myapp"
      - uses: actions/upload-artifact@v4
        with:
          name: .net-app
          path: ${{env.DOTNET_ROOT}}/myapp

  deploy:
    runs-on: windows-latest
    needs: build
    steps:
      - uses: actions/download-artifact@v4
        with:
          name: .net-app
      - name: Deploy to Azure
        uses: azure/webapps-deploy@v3
        with:
          app-name: 'shreyakwebapp'
          slot-name: 'Production'
          package: .
          publish-profile: ${{ secrets.AZUREAPPSERVICE_PUBLISHPROFILE }}
```
📦 .gitignore (for .NET projects)

Add this file to avoid committing build artifacts:
```bash
bin/
obj/
.vs/
*.user
*.suo
*.dll
*.exe
*.log
```

🔗 References

Azure App Service Overview

Deploy a .NET App to Azure

GitHub Actions for Azure

✨ With this setup, every push to main triggers a build & deployment pipeline → updates are live at:
👉 https://shreyakwebapp.azurewebsites.net


---


---

👉 If you copy this into your repo as `README.md`, your project page on GitHub will look professional and deployment-ready.  

Would you like me to also generate the `.gitignore` file and workflow file directly for your repo (so you just need to push them), or do you prefer adding them manually?
