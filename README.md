# 🎓 Campus AI — Intelligent Academic Management System
> Redefining how educational institutions communicate, automate, and operate — powered by Microsoft Power Platform and Azure AI.

---

## 📌 Overview

**Campus AI** is a cloud-native, AI-powered academic management platform built on the **Microsoft Power Platform** ecosystem. It unifies fragmented academic communication into a single intelligent system — enabling students to query information conversationally and administrators to manage schedules through natural language.

No more missed updates. No more WhatsApp chaos. No more administrative bottlenecks.

---

## 🚨 The Problem

Academic communication in most institutions is scattered across:

- 📋 Notice boards
- 💬 WhatsApp groups
- 📧 Email chains
- 🌐 Disconnected portals

This fragmentation causes students to **miss critical updates** — room changes, session cancellations, placement drives, trainer reassignments — and leaves administrators buried in repetitive manual work.

---

## 💡 The Solution

Campus AI acts as a **centralized intelligence layer** for academic operations:

| For Students | For Admins |
|---|---|
| Ask any academic question conversationally | Update schedules using plain English |
| Get real-time timetable & placement info | Emergency updates override schedules automatically |
| Never miss a room change or cancellation | Zero manual follow-up required |

---

## ⚙️ Technology Stack

| Technology | Role |
|---|---|
| **Microsoft Power Apps** | Frontend application interface |
| **Microsoft Copilot Studio** | AI Agents (Student & Admin) |
| **Microsoft Power Automate** | Workflow & process automation |
| **Microsoft Dataverse** | Cloud relational database |
| **Microsoft Power BI** | Analytics & reporting dashboard |
| **Azure AI Services** | Natural Language Processing |
| **SharePoint Online** | Document & resource storage |
| **Microsoft 365** | Authentication & platform integration |

---

## 🏗️ System Architecture

Campus AI is structured across a **three-tier cloud architecture**:

```
┌─────────────────────────────────────────────┐
│            PRESENTATION LAYER               │
│   Power Apps │ Admin Agent │ Student Agent  │
│              Analytics Dashboard            │
└────────────────────┬────────────────────────┘
                     │
┌────────────────────▼────────────────────────┐
│               LOGIC LAYER                   │
│  Power Automate Flows │ Override Logic      │
│  Schedule Retrieval │ Data Cleanup          │
└────────────────────┬────────────────────────┘
                     │
┌────────────────────▼────────────────────────┐
│                DATA LAYER                   │
│  Weekly Schedule │ Emergency Updates        │
│  Placement Data │ Academic Information      │
└─────────────────────────────────────────────┘
```

---

## ✨ Key Features

### 🧑‍🎓 Student Agent
- Conversational timetable lookups
- Faculty and trainer information
- Placement drive schedules
- Emergency & override schedule updates
- Natural language query handling

### 🛠️ Admin Agent
- Natural language schedule modifications
- Emergency update broadcasting
- Automated timetable management
- Workflow-driven data automation

### 🔧 System Capabilities
- ⚡ Real-time schedule communication
- 🔄 Intelligent emergency override logic
- 🤖 AI-powered conversational interface
- 📊 Analytics and reporting dashboard
- 🔐 Secure, cloud-based architecture

---

## 🔁 How It Works

### Admin Workflow
```
Admin enters update in natural language
        ↓
AI Agent extracts parameters via NLP
        ↓
Power Automate validates & processes data
        ↓
Emergency update stored in Dataverse
        ↓
Students receive updated information instantly
```

### Student Workflow
```
Student asks a query conversationally
        ↓
Student Agent processes the request
        ↓
System checks for emergency overrides first
        ↓
Latest & most accurate data is returned
        ↓
Student gets the right answer, instantly
```

---

## 🗄️ Database Design

### Weekly Schedule Table
Stores the permanent academic timetable:

| Field | Description |
|---|---|
| Batch Name | Student group identifier |
| Technology / Subject | Course or topic |
| Trainer Name | Assigned faculty/trainer |
| Room / Venue | Physical or virtual location |
| Day of Week | Scheduled day |
| Session Timings | Start and end time |

### Emergency Updates Table
Stores temporary schedule overrides:

| Field | Description |
|---|---|
| Update ID | Unique identifier |
| Batch Name | Affected student group |
| Technology | Affected subject/course |
| Action Type | Type of change (cancel, reschedule, etc.) |
| New Venue | Updated location |
| Start Date | Override effective from |
| End Date | Override expires on |

---

## ⚡ Power Automate Flows

| Flow Name | Purpose |
|---|---|
| `Add Emergency Update` | Insert new schedule changes |
| `Retrieve Student Schedule` | Fetch timetable data |
| `Apply Override Logic` | Merge emergency updates with base schedule |
| `Delete Expired Updates` | Auto-cleanup old records |
| `Placement Drive Query` | Return placement-related information |

---

## 📈 Advantages

- ✅ **Single source of truth** for all academic communication
- ✅ **Real-time delivery** — no delays, no manual broadcasts
- ✅ **Reduced admin workload** — automation handles the repetitive tasks
- ✅ **Student-first UX** — conversational, intuitive, always available
- ✅ **Enterprise-grade security** via Microsoft 365
- ✅ **Scalable architecture** built for growth

---

## 🚀 Roadmap

- [ ] 🎙️ Voice-based interaction support
- [ ] 📱 Mobile application deployment
- [ ] 🌐 Multi-language chatbot support
- [ ] 🔒 Biometric attendance integration
- [ ] 📚 LMS (Learning Management System) integration
- [ ] 🧠 AI predictive analytics for academic trends
- [ ] 🔔 Push notifications via Microsoft Teams & Email

---

## 🧰 Built With

![Power Apps]
![Power Automate]
![Copilot Studio]
![Dataverse]
![Power BI]
![Azure]
![SharePoint]
<img width="292" height="559" alt="WhatsApp Image 2026-05-10 at 4 09 50 PM" src="https://github.com/user-attachments/assets/f5aca841-d24e-4514-88e2-d909d572fc48" />
<img width="294" height="542" alt="WhatsApp Image 2026-05-10 at 4 09 50 PM (1)" src="https://github.com/user-attachments/assets/8dd55150-bd36-44fd-b63f-40be7cf15026" />
<img width="299" height="493" alt="WhatsApp Image 2026-05-10 at 4 09 51 PM" src="https://github.com/user-attachments/assets/8f0b05b3-d42b-4ee7-9d5a-8e91192d3b6b" />
<img width="294" height="506" alt="WhatsApp Image 2026-05-10 at 4 09 51 PM (1)" src="https://github.com/user-attachments/assets/f8333a27-c94c-4d51-98f4-34020b3364f0" />


---

## 📄 License

This project is developed for academic and institutional use. Refer to the [LICENSE](./LICENSE) file for details.

---

<div align="center">
  <strong>Campus AI</strong> — Smarter Campuses. Seamless Communication. Zero Friction.
</div>
