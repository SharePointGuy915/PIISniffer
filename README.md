# SharePoint PII Exposure Scanner

A browser-based Microsoft 365 security assessment tool that helps identify potentially exposed Personally Identually Identifiable Information (PII) stored in SharePoint Online. The application uses the Microsoft Graph Search API to locate files containing sensitive terms and generates a findings register for review and remediation.

> ⚠️ **Disclaimer:** This tool is intended for discovery and assessment purposes only. It is not a Data Loss Prevention (DLP) solution, compliance certification tool, or replacement for Microsoft Purview. All findings require human review.

---

## Features

### 🔐 Microsoft 365 Authentication

- Microsoft Entra ID (Azure AD) authentication
- Secure sign-in via MSAL (Microsoft Authentication Library)
- Permission-trimmed search results
- Delegated Microsoft Graph API access

### 🔍 PII Discovery Scanning

Search SharePoint content for customizable keywords and phrases, including:

- Social Security Numbers (SSN)
- Driver's Licenses
- Passports
- Dates of Birth (DOB)
- Medical Records
- SF-50
- DD214
- DD2875
- Home Addresses
- Credit Card Information
- Financial Records
- Organizationally-defined sensitive terms

### 📂 SharePoint Content Discovery

- Searches only files the signed-in user has permission to access
- Uses Microsoft Graph Search API
- Exact phrase searching
- Configurable scan limits
- Supports large result sets

### 📊 Findings Dashboard

Displays:

| Field | Description |
|---------|-------------|
| Command / Site | SharePoint site title |
| Search Term | Matched keyword or phrase |
| URL Location | Direct link to the file |
| Site Owners | Ownership metadata when available |
| Review Status | Status for remediation tracking |

### 📤 Reporting

Export findings to:

- Excel (.xlsx)
- CSV (.csv)

### 👥 Site Ownership Discovery

Attempts to identify site owners using Microsoft Graph permissions to assist with remediation workflows.

---

## Technology Stack

| Component | Technology |
|------------|------------|
| Frontend | HTML5 |
| Styling | CSS3 |
| Authentication | MSAL Browser |
| API | Microsoft Graph |
| Export Engine | SheetJS (xlsx) |
| Runtime | Vanilla JavaScript |

### External Libraries

#### Microsoft Authentication Library (MSAL)

```html
https://alcdn.msauth.net/browser/3.26.1/js/msal-browser.min.js
```

#### SheetJS

```html
https://cdn.jsdelivr.net/npm/xlsx@0.18.5/dist/xlsx.full.min.js
```

---

## Prerequisites

### Microsoft 365 Requirements

- Microsoft 365 Tenant
- SharePoint Online
- Microsoft Entra ID
- Permission to register applications

### Required Microsoft Graph Permissions

| Permission | Purpose |
|------------|------------|
| Sites.Read.All | Read SharePoint site metadata |
| Files.Read.All | Read file metadata |

> Administrator consent may be required.

---

## Setup

### 1. Register an Entra ID Application

Open:

```text
Microsoft Entra Admin Center
→ Applications
→ App Registrations
→ New Registration
```

Configure:

- Name: SharePoint PII Exposure Scanner
- Supported Account Types: Organizational Accounts
- Platform: Single Page Application (SPA)

---

### 2. Configure Redirect URI

Add the URL where the application will reside.

Example:

```text
https://yourdomain.com/sharepoint_pii_exposure_scanner.html
```

---

### 3. Configure API Permissions

Add the following delegated Microsoft Graph permissions:

```text
Sites.Read.All
Files.Read.All
```

Grant admin consent if required.

---

### 4. Deploy Application

Host the HTML file from an approved HTTPS location, such as:

- SharePoint Online
- Azure Storage Static Websites
- Azure App Service
- Internal IIS Web Server

> Do not run the application using `file://`.

---

### 5. Launch the Application

Provide:

- Tenant ID or domain
- Client ID

Click **Sign In**.

---

## Usage

### Connect to Microsoft 365

1. Enter Tenant ID or Domain.
2. Enter Application Client ID.
3. Click **Sign In**.

---

### Configure a Scan

1. Enter one search term per line.
2. Specify the maximum results to return.
3. Click **Start Scan**.

Example search terms:

```text
SSN
Passport
Driver's License
Medical Records
DD214
Home Address
Credit Card
```

---

### Review Findings

Each result includes:

- SharePoint Site
- Matched Search Term
- File Location
- Site Ownership Information
- Review Status

---

### Export Findings

#### Excel

Generates:

```text
SharePoint_PII_Findings_YYYY-MM-DD.xlsx
```

#### CSV

Generates:

```text
SharePoint_PII_Findings.csv
```

---

## How It Works

The application uses the Microsoft Graph Search endpoint:

```javascript
POST /search/query
```

Searching for:

```javascript
{
  "entityTypes": ["driveItem"]
}
```

Each keyword is submitted as an exact phrase search:

```text
"Social Security Number"
```

Results are permission-trimmed and limited to content the signed-in user can already access.

---

## Security Model

### ✅ What the Tool Does

- Searches SharePoint content the user already has access to
- Retrieves metadata only
- Records file locations
- Attempts ownership discovery
- Exports findings metadata

### ❌ What the Tool Does NOT Do

- Bypass SharePoint permissions
- Access unauthorized files
- Export file contents
- Export matched text snippets
- Modify SharePoint documents
- Replace DLP or Compliance solutions

---

## Known Limitations

### Site Ownership

Microsoft Graph does not always expose complete SharePoint ownership information.

In some tenants:

- Owners may not be returned
- Groups may not be resolvable
- Service principals may appear instead of individuals

Always validate ownership through:

- SharePoint Admin Center
- Site Permissions
- Site Collection Administrators

### Search Accuracy

This application relies on Microsoft Search indexing.

Potential limitations:

- False positives
- False negatives
- Newly uploaded files may not yet be indexed
- Search behavior depends on tenant search configuration

---

## Recommended Use Cases

- Privacy Assessments
- Security Audits
- Data Governance Initiatives
- Records Management Reviews
- Compliance Readiness Exercises
- SharePoint Cleanup Projects
- PII Exposure Discovery

---

## Example Workflow

```text
1. Authenticate to Microsoft 365
2. Configure search terms
3. Scan SharePoint content
4. Review potential matches
5. Validate findings
6. Identify content owners
7. Assign remediation actions
8. Export findings register
```

---

## Future Enhancements

Potential enhancements include:

- Multi-threaded scanning
- Severity scoring
- SharePoint site filtering
- Purview sensitivity label integration
- Remediation workflow tracking
- Automated owner notifications
- Risk dashboard analytics
- PDF export support

---

## Screenshots

Add screenshots here after deployment:

```text
/docs/images/login-screen.png
/docs/images/scan-results.png
/docs/images/export-report.png
```

---

## Contributing

Contributions are welcome.

Suggested areas:

- Additional search capabilities
- Improved owner resolution
- Enhanced reporting
- Performance optimization
- Accessibility improvements

---

## License

Internal Organizational Use Only

Review your organization's security, privacy, records management, and acceptable use policies before deployment.

---

## Author
SharePointGuy915
Developed for Microsoft 365 SharePoint security assessment and PII discovery initiatives.

---

## Version

**Version:** 1.0  
**Platform:** Microsoft 365 / SharePoint Online  
**Authentication:** Microsoft Entra ID (MSAL)  
**API:** Microsoft Graph Search API
