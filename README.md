# Fabric Fest

🎪 **Fabric Fest** - A V-Valley event dedicated to Microsoft Fabric

## Overview

Fabric Fest is a single-page web application showcasing information about a V-Valley technology event focused on Microsoft Fabric. The site provides event details, a full-day schedule, and registration information.

## Features

- **Event Information**: Details about the Fabric Fest event including location and what attendees can expect
- **Event Schedule**: Complete schedule from 9:00 AM to 5:00 PM with sessions, workshops, and networking breaks
- **Registration Section**: Call-to-action for event registration
- **Responsive Design**: Optimized for desktop, tablet, and mobile devices
- **Modern UI**: Professional design using Microsoft Fabric brand colors
- **Secure**: Implements Content Security Policy and other security headers

## Technologies

- HTML5
- CSS3
- Vanilla JavaScript
- Azure Static Web Apps configuration

## Files

- `index.html` - Main landing page with all content
- `styles.css` - Styling and responsive design
- `app.js` - Interactive features and notification system
- `staticwebapp.config.json` - Azure Static Web Apps configuration

## Local Development

To run locally, use any HTTP server. For example with Python:

```bash
python3 -m http.server 8080
```

Then open `http://localhost:8080` in your browser.

## Deployment to Azure Static Web Apps

This application is configured for deployment to Azure Static Web Apps. The `staticwebapp.config.json` file contains all necessary configuration including:

- Route handling
- Security headers
- MIME types
- Navigation fallback

### Deploy via Azure Portal

1. Create a new Static Web App in Azure Portal
2. Connect to your GitHub repository
3. Set the app location to `/` (root)
4. No build configuration needed (static HTML/CSS/JS)
5. Azure will automatically deploy on push to the main branch

### Deploy via Azure CLI

```bash
az staticwebapp create \
    --name fabric-fest \
    --resource-group <your-resource-group> \
    --source https://github.com/<your-username>/fabric-fest \
    --location "Central US" \
    --branch main \
    --app-location "/" \
    --login-with-github
```

## Security

The application implements several security best practices:

- Content Security Policy (CSP) headers
- X-Frame-Options to prevent clickjacking
- X-Content-Type-Options to prevent MIME type sniffing
- X-XSS-Protection for cross-site scripting protection
- No inline scripts (external JavaScript only)

## License

© 2026 V-Valley | Fabric Fest. All rights reserved.
