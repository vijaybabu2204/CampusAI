# CampusAI Setup Guide

## Project Overview

**Campus AI** is an intelligent academic management system built on Microsoft Power Platform.
It uses AI-powered agents to automate campus communication, schedule updates, emergency notifications,
webinars, and placement drive information through conversational interfaces.

### Built With
- Microsoft Power Apps (Canvas App + PCF Component)
- Microsoft Copilot Studio (Student Agent + Admin Agent)
- Microsoft Power Automate (Backend flows)
- Microsoft Dataverse (Database)
- Microsoft Outlook (Notifications)
- Power Apps Component Framework (PCF) — Purple Hex UI

---

## Required Environment

| Requirement | Details |
|-------------|---------|
| Microsoft 365 License | With Power Apps access |
| Power Apps Plan | Per-app or Per-user license |
| Copilot Studio License | For AI agents |
| Dataverse Environment | Developer or Production |
| Node.js | v16 or higher |
| Power Platform CLI (PAC) | Latest version |
| .NET SDK | v6 or higher |
| VS Code | Latest version |

---

## How to Import Solution

### Step 1 — Prerequisites
Install required tools:
```powershell
# Install Power Platform CLI
winget install Microsoft.PowerPlatformCLI

# Verify installation
pac --version
node --version
```

### Step 2 — Fix PowerShell Execution Policy
```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

### Step 3 — Create PCF Project
```powershell
cd C:\
mkdir PCFProject
cd PCFProject
mkdir CampusAI
cd CampusAI

pac pcf init --namespace BotApp --name CampusAIApp --template field
npm install
code .
```

### Step 4 — Replace PCF Files in VS Code
Replace these two files with the Campus AI versions:
- `ControlManifest.Input.xml`
- `index.ts`

Save both files (`Ctrl+S`)

### Step 5 — Build and Push PCF
```powershell
# Build the component
npm run build

# Authenticate to your environment
pac auth create --url https://yourorg.crm.dynamics.com

# Verify connection
pac org who

# Push to Power Apps
pac pcf push --publisher-prefix ca
```

---

## Dataverse Setup

### Tables Required

#### 1. Weekly Schedule Table
| Column | Type | Description |
|--------|------|-------------|
| batch | Text | Batch name (e.g. Batch A) |
| technology | Text | Subject/Technology name |
| trainer | Text | Trainer full name |
| room | Text | Room/Lab number |
| day | Choice | Monday to Saturday |
| start_time | DateTime | Class start time |
| end_time | DateTime | Class end time |

#### 2. Emergency Updates Table
| Column | Type | Description |
|--------|------|-------------|
| batch | Text | Affected batch name |
| technology | Text | Affected subject |
| action | Choice | Move / Cancel / No Class |
| new_room | Text | New room (if moved) |
| start_date | Date | Update start date |
| end_date | Date | Update end date |
| created_by | Text | Admin who created |
| created_on | DateTime | Timestamp |

#### 3. Webinars Table
| Column | Type | Description |
|--------|------|-------------|
| title | Text | Webinar topic |
| presenter | Text | Presenter name |
| platform | Choice | Teams / Zoom / Meet |
| link | URL | Meeting link |
| date_time | DateTime | Scheduled date and time |
| batch | Text | Target batch |

---

## Power Automate Flows

### Flow 1 — Add Emergency Update
```
Trigger: HTTP Request (from Admin Agent)
Action 1: Parse JSON (extract command details)
Action 2: Create row in Emergency Updates table
Action 3: Send Outlook notification to batch
```

### Flow 2 — Get Student Schedule
```
Trigger: HTTP Request (from Student Agent)
Action 1: Get rows from Weekly Schedule table
Action 2: Get rows from Emergency Updates table
Action 3: Apply override logic
Action 4: Return merged schedule
```

### Flow 3 — Add Webinar / Virtual Meet
```
Trigger: HTTP Request (from Admin Agent)
Action 1: Parse JSON (webinar details)
Action 2: Create row in Webinars table
Action 3: Send Teams/Outlook invite to batch
```

---

## Copilot Studio Configuration

### Student Agent Topics
| Topic | Trigger Phrases |
|-------|----------------|
| Get Schedule | "my schedule", "today's classes", "timetable" |
| Emergency Updates | "any updates", "changes today", "cancelled" |
| Find Room | "where is my class", "room for flutter" |
| Trainer Info | "who is my trainer", "faculty for python" |
| Webinars | "any webinars", "virtual meet today" |

### Admin Agent Topics
| Topic | Trigger Phrases |
|-------|----------------|
| Move Room | "move class to", "change room" |
| Cancel Class | "cancel today's", "no session" |
| No Classes | "no classes for batch", "holiday" |
| Add Webinar | "add webinar", "schedule meet" |
| Share Link | "send webinar link", "share meeting" |

---

## Connection References

After importing solution, reconnect these:

| Connection | Type | Used By |
|------------|------|---------|
| Dataverse | Microsoft Dataverse | All flows |
| Office 365 Outlook | Outlook | Notification flows |
| Microsoft Teams | Teams connector | Webinar flows |

Steps to reconnect:
1. Go to **make.powerapps.com**
2. Open **Campus AI** solution
3. Click **Cloud flows**
4. Open each flow → click **Edit**
5. Fix any connections shown in red
6. Save and enable the flow

---

## Required Licenses

| License | Purpose |
|---------|---------|
| Microsoft 365 | Outlook, Teams integration |
| Power Apps per-user or per-app | Canvas App access |
| Power Automate | Cloud flows |
| Copilot Studio (100 sessions/month free) | AI agents |
| Dataverse | Database storage |

---

## Canvas App Setup

### Step 1 — Create Canvas App
1. Go to **make.powerapps.com**
2. Open **Campus AI** solution
3. Click **+ New** → **App** → **Canvas app**
4. Choose **Phone layout**

### Step 2 — Enable PCF Components
Inside the Canvas App editor:
1. Click **Settings** → **Updates**
2. Click **Preview** tab
3. Find **"Power Apps component framework for canvas apps"**
4. Toggle **ON** → Close

### Step 3 — Insert PCF Component
```
+ Insert
→ Get more components (bottom)
→ Code tab
→ CampusAIApp
→ Import
→ Insert → Code components → CampusAIApp
```

### Step 4 — Full Screen Setup
Select the component and set:
```
X      = 0
Y      = 0
Width  = App.Width
Height = App.Height
```

### Step 5 — Connect Properties
| Property | Formula |
|----------|---------|
| userRole | "student" or variable |
| userName | User().FullName |
| agentEndpoint | "your copilot studio URL" |
| adminFlowUrl | "your power automate URL" |
| outlookFlowUrl | "your outlook flow URL" |

---

## Steps to Run Chatbot / App

1. Import the Campus AI solution into Power Platform
2. Configure Dataverse tables (add sample data)
3. Reconnect Power Automate flows
4. Configure Copilot Studio agent connections
5. Push PCF component using `pac pcf push --publisher-prefix ca`
6. Open Canvas App → insert PCF component
7. Connect all properties
8. Click **Save** → **Publish**
9. Share the app with students and admins

---

## Common Errors and Fixes

| Error | Fix |
|-------|-----|
| `running scripts is disabled` | `Set-ExecutionPolicy RemoteSigned -Scope CurrentUser` |
| `pcfproj not found` | Run push from PCF root folder, not solutions subfolder |
| `No active environment` | Run `pac org select --environment "your-env"` |
| `publisher-prefix error` | Use `--publisher-prefix` not `--publisher -prefix` |
| Component not in Insert menu | Enable PCF in Settings → Updates → Preview |
| Flow connection error | Reconnect Dataverse and Outlook connections |

---

## Project Structure

```
CampusAI/
├── ControlManifest.Input.xml    # PCF properties definition
├── index.ts                     # Full app UI and logic
├── package.json                 # Build dependencies
├── tsconfig.json                # TypeScript config
├── generated/
│   └── ManifestTypes.d.ts       # Auto-generated types
└── solutions/
    ├── CampusAI.cdsproj
    └── bin/Debug/                # Built solution zip
```

---

## Support

For issues contact your Power Platform administrator or
raise a request at the campus IT helpdesk.

**Campus AI v2.0 — Built with Microsoft Power Platform**
