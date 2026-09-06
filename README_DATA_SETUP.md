# RAMAIAH ACADEMY FOUNDATION
## Executive Office Control Centre — Data Files & Manual Setup Guide

Welcome, **Sarojini**. This guide explains all data files connected to your Executive Office Control Centre, where they are stored, what each column means, and how to edit and update them daily in **Microsoft Excel** or **Google Sheets**.

---

### Directory Location of All Data Files

All your working CSV template files and master JSON backups are stored directly in your workspace under:
```
C:\Users\LENOVO\.gemini\antigravity\scratch\executive-office-control-centre\data\
```

You can open any of these `.csv` files in Microsoft Excel by double-clicking them, editing rows, and clicking **Save**.

---

### 1. The 10 Connected CSV Data Files

| # | CSV File Name | Connected Dashboard Module | Purpose |
|---|---|---|---|
| 1 | `actions.csv` | **Master Action Tracker** | Single source of truth for all tasks across VC (20%), CHRO (40%), and Strategy (40%). |
| 2 | `meetings.csv` | **Meeting Centre** | Class A (VC), Class B (CHRO/Strategy), and Class C meetings with pre-briefing & MoM tracking. |
| 3 | `decisions.csv` | **Decisions Register** | High-level decisions required, impact level, decision maker, deadlines, and recommendations. |
| 4 | `approvals.csv` | **Approvals & Sign-offs** | Purchase requisitions, CapEx, MoU agreements, faculty appointment letters, and SLA aging. |
| 5 | `waiting_for.csv` | **Waiting-For Register** | External dependencies with automatic calculation of **Days Waiting** and follow-up counter. |
| 6 | `projects.csv` | **Projects & Initiatives** | PMO tracking for 3D Design, Advanced VLSI, Embedded CoE, Software cohorts, and milestones. |
| 7 | `recruitment.csv` | **HR Recruitment Pipeline** | Open faculty and staff requisitions, candidate stages, and hiring aging (strictly no sensitive PII). |
| 8 | `stakeholders.csv` | **Stakeholder Directory** | Tier 1 & Tier 2 leadership, government liaisons (KSDC), ecosystem partners (Techno Centre, Valdel). |
| 9 | `events.csv` | **Events & Dates Calendar** | Board meetings, academic batch launches, partner visits, and institutional audits. |
| 10 | `risks.csv` | **Risk & Escalation Matrix** | RAG-coded operational risks (e.g. trainer vacancy, hardware customs delay) with mitigation plans. |
| — | `executive_data_master.json` | **Master Backup File** | Complete single-file snapshot containing all 10 datasets together. |

---

### 2. How to Update the Dashboard (3 Ways)

#### Option A: Direct In-App Editing (Easiest)
- Click **+ Quick Add** at the top right of the dashboard to create an action.
- Click **Toggle Status (`↺`)** directly in the table to cycle an item from `In Progress` → `Waiting` → `Completed` → `Overdue`.
- Changes are automatically saved to your browser's persistent storage.

#### Option B: Edit in Excel & Upload (Batch Updating)
1. Open any of the `.csv` files (e.g., `actions.csv`) in **Microsoft Excel**.
2. Add, update, or remove rows as needed.
3. Save the file (keep the `.csv` format).
4. Open the dashboard, navigate to **Tab 17 (Data Management)**, click **Upload & Sync CSV**, and select your file.
5. The dashboard will automatically detect which dataset it is, update the table, and recalculate all KPIs and workload charts.

#### Option C: One-Click Master JSON Backup / Restore
- In **Tab 17 (Data Management)**, click **Download JSON Backup** to save your current work.
- To restore everything onto any computer or browser, click **Import JSON** and select `executive_data_master.json`.

---

### 3. Detailed Data Schemas & Allowed Values

#### A. `actions.csv` (Master Action Tracker)
- **`Action_ID`**: Unique ID (e.g. `ACT-101`, `ACT-102`).
- **`Task_Title`**: Clear, actionable task name.
- **`Support_Area`**: Must be one of: `VC`, `CHRO`, `Strategy`, `EA`. *(Drives the 20/40/40 workload split!)*
- **`Requested_By`**: Leader who requested it (e.g. `Mr. Velluri`, `CHRO`, `Strategy Head`).
- **`Owner`**: Person responsible (e.g. `Sarojini (EA)`, `HR Ops Head`, `Lab Admin`).
- **`Department`**: Relevant department (e.g. `Executive Office`, `Human Resources`, `Embedded Systems`).
- **`Priority`**: `Critical`, `High`, `Medium`, `Low`.
- **`Date_Created`**: Format `YYYY-MM-DD`.
- **`Due_Date`**: Format `YYYY-MM-DD`. *(If past today and not completed, automatically becomes Overdue)*.
- **`Status`**: `In Progress`, `Overdue`, `Waiting`, `Not Started`, `Completed`.
- **`Next_Action`**: Concrete next step (e.g. *Call at 2:00 PM for confirmation*).
- **`Dependency`**: What is blocking this (e.g. *Legal clearance*, *Finance model*).
- **`Escalation_Required`**: `Yes` or `No`.

#### B. `meetings.csv` (Executive Meetings)
- **`Meeting_ID`**: `MTG-01`, `MTG-02`, etc.
- **`Date`**: `YYYY-MM-DD`.
- **`Time`**: e.g. `09:00 AM - 09:15 AM`.
- **`Meeting_Title`**: Agenda title.
- **`Class_Type`**:
  - `A` = **Critical** (Mr. Velluri must attend; requires 1-page pre-brief).
  - `B` = **Important** (CHRO or Strategy Lead may chair; EA coordinates).
  - `C` = **Operational** (Informational summary notes).
- **`Function_Area`**: `VC`, `CHRO`, `Strategy`, or `EA`.
- **`Participants`**: Key attendees.
- **`Pre_Brief_Status`**: `Ready (1-Page)`, `Drafted`, or `N/A`.
- **`Deliverable_MoM`**: Output of meeting (e.g. *Signed Term Sheet*, *Action Log*).

#### C. `waiting_for.csv` (Follow-up Register)
- **`Waiting_ID`**: `WAIT-01`, `WAIT-02`.
- **`Stakeholder`**: Name and title.
- **`Organisation`**: External partner or internal department.
- **`Matter_Pending`**: Exact deliverable you are waiting for.
- **`Date_Requested`**: `YYYY-MM-DD`.
- **`Expected_Date`**: `YYYY-MM-DD`.
- **`Days_Waiting`**: Number of days elapsed. *(If $>5$ days, the dashboard triggers an alert for follow-up)*.
- **`Follow_Ups_Sent`**: Count of reminders sent.

#### D. `decisions.csv` (Decisions Register)
- **`Decision_ID`**: `DEC-201`, `DEC-202`.
- **`Decision_Required`**: The question to be decided.
- **`Function_Area`**: `VC`, `CHRO`, `Strategy`.
- **`Decision_Maker`**: e.g. `Mr. Velluri (VC)`, `CHRO`, `Head of Strategy`.
- **`Required_By`**: `YYYY-MM-DD`.
- **`Impact`**: `Critical`, `High`, `Medium`.
- **`Status`**: `Pending`, `Under Discussion`, `Approved`, `Rejected`.
- **`Recommendation`**: Your recommended position as EA.

#### E. `approvals.csv` (Approvals & Sign-offs)
- **`Item_Code`**: `APP-401`, `APP-402`.
- **`Approval_Item`**: Description (e.g. *CapEx: 12 High-Performance Workstations*).
- **`Function_Area`**: `VC`, `CHRO`, `Strategy`.
- **`Financial_Value`**: e.g. `₹8,50,000`, `₹14.2 LPA`, or `Non-Financial`.
- **`Approver`**: Name or designation.
- **`Status`**: `Under Review`, `Awaiting Signature`, `Approved`.
- **`SLA_Aging`**: SLA countdown (e.g. `24h Remaining`, `Due Today`).

---

### 4. What to Do on Day 1 (Immediate Next Steps)

1. **Open the 10 CSV files** in `scratch/executive-office-control-centre/data/`.
2. Inspect the pre-filled sample rows. They are customized with authentic Ramaiah Academy Foundation projects:
   - Dassault Systèmes Innovation Centre expansion
   - Advanced VLSI Finishing School
   - Embedded Systems IoT lab with Valdel
   - Techno Centre Engineering corporate MoUs
3. Modify any names, dates, or contact details to reflect your exact start date.
4. Launch the dashboard by opening `executive_control_centre.html` in Chrome or Edge.
5. In **Tab 17 (Data Management)**, test importing your edited `actions.csv` to watch the numbers update live!
