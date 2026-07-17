# Azure Admin App

A cross-platform Flutter desktop application for managing both **Azure Active Directory** and **On-Premise Active Directory** users and groups through PowerShell automation.

![App Background](assets/images/bg1.jpeg)

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [App Structure](#app-structure)
- [Screenshots](#screenshots)
- [Dependencies](#dependencies)
- [PowerShell Scripts](#powershell-scripts)
- [Getting Started](#getting-started)

---

## Overview

The **Azure Admin App** is built for IT administrators who need to manage Azure AD and On-Premise Active Directory resources quickly and efficiently. It provides a GUI wrapper around PowerShell scripts — no more running scripts manually in the terminal.

| Property | Details |
|---|---|
| Platform | Windows (Desktop) |
| Framework | Flutter 3.x |
| Language | Dart |
| Target Users | IT Administrators |
| Script Integration | PowerShell |

---

## Features

### Tab 1 — Azure Admin

Five operational cards, each color-coded for quick identification:

| # | Card | Color | Description |
|---|------|-------|-------------|
| 1 | **Create New User** | Blue | Bulk-create Azure AD users from a CSV file |
| 2 | **Group Assignment** | Green | Assign users to Azure groups using two CSV files |
| 3 | **Add Contacts via CSV** | Orange | Bulk-import external contacts into the directory |
| 4 | **Create Distribution Groups** | Purple | Create distribution lists from a CSV file |
| 5 | **Assign Users to DLs** | Teal | Bulk-assign users to existing distribution lists |

All operations display their PowerShell output in a scrollable output panel at the top of the screen.

---

### Tab 2 — On-Premise Admin

A form-based interface for creating a single user in an On-Premise Active Directory:

| Field | Notes |
|---|---|
| Username | AD account name |
| Password | Masked input |
| Email | User's email address |
| Authorized Service | Service/role assignment |
| SSH Public Key | Optional SSH key for the account |

---

## App Structure

```
lib/
├── main.dart                       # App entry point, MainScreen with bottom tab navigation
├── home_page.dart                  # Azure Admin tab — PowerShellApp widget (all 5 operations)
└── on_premise_user_creation.dart   # On-Premise Admin tab — user creation form
```

### Component Hierarchy

```
MyApp (MaterialApp)
└── MainScreen (BottomNavigationBar — 2 tabs)
    ├── Tab 0: Azure Admin
    │   └── PowerShellApp
    │       ├── Output Panel (TextArea)
    │       └── GridView (2 columns)
    │           ├── Create New User Card
    │           ├── Group Assignment Card
    │           ├── Add Contacts Card
    │           ├── Create Distribution Groups Card
    │           └── Assign Users to DLs Card
    └── Tab 1: On-Premise Admin
        └── OnPremiseUserCreationApp
            ├── Username Field
            ├── Password Field
            ├── Email Field
            ├── Authorized Service Field
            └── SSH Public Key Field
```

---

## Screenshots

> **Azure Admin Tab** — Five color-coded operation cards with a central output panel

```
┌─────────────────────────────────────────────────────────────┐
│  Output Panel (PowerShell results appear here)              │
├────────────────────────┬────────────────────────────────────┤
│  🔵 Create New User   │  🟢 Group Assignment               │
│  [ Select CSV ]        │  [ Select Users CSV ]              │
│  [ Run Script ]        │  [ Select Groups CSV ]             │
│                        │  [ Run Script ]                    │
├────────────────────────┼────────────────────────────────────┤
│  🟠 Add Contacts       │  🟣 Create Distribution Groups     │
│  [ Select CSV ]        │  [ Select CSV ]                    │
│  [ Run Script ]        │  [ Run Script ]                    │
├────────────────────────┼────────────────────────────────────┤
│  🔵 Assign Users to DLs                                     │
│  [ Select CSV ]  [ Run Script ]                             │
└─────────────────────────────────────────────────────────────┘
```

> **On-Premise Admin Tab** — Single user creation form

```
┌─────────────────────────────────────┐
│         On-Premise User Setup       │
│                                     │
│  Username:    [________________]    │
│  Password:    [●●●●●●●●●●●●●●●●]   │
│  Email:       [________________]    │
│  Auth Service:[________________]    │
│  SSH Key:     [________________]    │
│                                     │
│         [ Create User ]             │
│                                     │
│  Output:                            │
│  [______________________________]   │
└─────────────────────────────────────┘
```

---

## Dependencies

```yaml
file_picker: ^8.1.3        # CSV file selection dialogs
path_provider: ^2.1.5      # Temp directory for script extraction
process_run: ^1.1.0        # PowerShell script execution
csv: ^6.0.0                # CSV parsing
http: ^1.2.2               # HTTP requests
shared_preferences: ^2.3.2 # Local persistence
flutter_appauth: ^8.0.0+1  # OAuth2 / OpenID Connect
msal_flutter: ^2.0.1       # Microsoft Authentication Library
msal_auth: ^2.1.1          # MSAL auth wrapper
aad_oauth: ^1.0.1          # Azure AD OAuth
```

---

## PowerShell Scripts

All scripts are bundled in `assets/` and extracted to the system temp directory at runtime before execution.

| Script | Purpose |
|---|---|
| `importuser.ps1` | Bulk create Azure AD users from CSV |
| `script.ps1` | Assign users to Azure groups |
| `add_contacts.ps1` | Import external contacts |
| `create_dl.ps1` | Create distribution lists |
| `assign_to_dl.ps1` | Assign users to distribution lists |
| `onpremise_importuser.ps1` | Create on-premise AD user |
| `create_user.ps1` | Alternate user creation script |
| `delete_user.ps1` | Delete a user account |
| `disable_user.ps1` | Disable a user account |
| `wipe_user_data.ps1` | Wipe user data |

---

## Getting Started

### Prerequisites

- Flutter SDK `>=3.4.3`
- Windows OS (PowerShell required)
- Azure AD tenant (for Azure operations)
- On-Premise Active Directory access (for on-premise operations)

### Install & Run

```bash
# Clone the repository
git clone <repo-url>
cd azureadminapp

# Install dependencies
flutter pub get

# Run on Windows desktop
flutter run -d windows
```

### CSV Format

For **Create New User**, your CSV should include columns such as:

```
DisplayName,UserPrincipalName,Password,Department,...
John Doe,jdoe@company.com,P@ssw0rd!,Engineering,...
```

Refer to the individual PowerShell scripts in `assets/` for the exact column format expected by each operation.

---

## License

Private — not published to pub.dev.
