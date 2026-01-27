# Azure Deployment Guide

This guide explains how to deploy the Fabric Fest website to Azure Static Web Apps using GitHub Actions.

## Prerequisites

1. An Azure account with an active subscription
2. GitHub repository with admin access
3. Azure Static Web Apps resource created in Azure Portal

## Setup Instructions

### 1. Create Azure Static Web App

1. Go to [Azure Portal](https://portal.azure.com)
2. Click "Create a resource"
3. Search for "Static Web App" and select it
4. Click "Create"
5. Fill in the required information:
   - **Subscription**: Choose your subscription
   - **Resource Group**: Create new or use existing
   - **Name**: Choose a unique name (e.g., `fabric-fest-prod`)
   - **Plan type**: Choose Free or Standard
   - **Region**: Choose the closest region to your users
   - **Deployment details**:
     - Source: **GitHub**
     - Organization: Your GitHub username/org
     - Repository: `fabric-fest`
     - Branch: `main`
6. Click "Review + create" then "Create"

### 2. Get the Deployment Token

After the Static Web App is created:

1. Navigate to your Static Web App resource in Azure Portal
2. Go to "Overview" section
3. Click "Manage deployment token"
4. Copy the deployment token

### 3. Add Secret to GitHub

1. Go to your GitHub repository
2. Navigate to **Settings** → **Secrets and variables** → **Actions**
3. Click "New repository secret"
4. Add the secret:
   - **Name**: `AZURE_STATIC_WEB_APPS_API_TOKEN`
   - **Value**: Paste the deployment token from Azure
5. Click "Add secret"

### 4. Configure GitHub Environment (Optional)

For additional protection, you can set up a GitHub Environment:

1. Go to your GitHub repository
2. Navigate to **Settings** → **Environments**
3. Click "New environment"
4. Name it: `Production`
5. (Optional) Add protection rules:
   - Required reviewers
   - Wait timer
   - Deployment branches

## How It Works

The GitHub Actions workflow (`.github/workflows/azure-static-web-apps-deploy.yml`) will:

1. **Trigger on**:
   - Push to `main` branch → Deploy to production
   - Pull requests → Create staging environment
   - PR closed → Clean up staging environment

2. **Deployment Process**:
   - Check out the repository code
   - Deploy to Azure Static Web Apps
   - Set the Production environment URL

3. **Features**:
   - ✅ Automatic deployments on merge to main
   - ✅ PR preview environments
   - ✅ Environment URL tracking
   - ✅ No build step needed (static files)

## Testing the Deployment

1. Merge the PR with the workflow file to the `main` branch
2. Go to **Actions** tab in GitHub
3. You should see the "Azure Static Web Apps CI/CD" workflow running
4. Once complete, visit the Azure Portal to get your site URL
5. The URL will be available in:
   - Azure Portal → Static Web App → Overview → URL
   - GitHub → Environments → Production

## Troubleshooting

### Workflow fails with "Invalid token"
- Verify the `AZURE_STATIC_WEB_APPS_API_TOKEN` secret is correctly set
- Regenerate the token in Azure Portal if needed

### Deployment succeeds but site doesn't update
- Check if the workflow is running on the correct branch
- Verify the `app_location` in the workflow file is set to "/"

### Need to update the deployment configuration
- Edit `.github/workflows/azure-static-web-apps-deploy.yml`
- Commit and push to trigger a new deployment

## Additional Resources

- [Azure Static Web Apps Documentation](https://docs.microsoft.com/azure/static-web-apps/)
- [GitHub Actions Documentation](https://docs.github.com/actions)
- [Static Web Apps CLI](https://github.com/Azure/static-web-apps-cli)
