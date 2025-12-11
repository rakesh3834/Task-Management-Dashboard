Task Management Dashboard

A web-based Task Assignment, Tracking, and Reporting System built using Firebase Realtime Database and EmailJS.
This dashboard enables managers to assign tasks, track daily/weekly/monthly performance, filter tasks, export backups, and send automated email reports.

1. Overview

The Task Management Dashboard is an internal productivity tool designed to:

Assign tasks to employees with multi-task input support

Manage daily tasks and overdue carry-forward tasks

Generate daily, weekly, monthly performance summaries

Apply advanced custom filters

Send task assignment notifications via EmailJS

Generate and email employee-wise performance reports

Export full data in JSON or CSV for backup

Edit, update, or delete tasks directly in the UI

The system is powered by:

Component	Technology
Frontend	HTML, CSS, JavaScript
Database	Firebase Realtime Database
Email Sending	EmailJS
Persistence	Firebase Cloud + LocalStorage (for UI tabs)
2. Features
A. Task Assignment

Assign tasks to any employee by ID

Auto-fill employee profile if already used

Multi-task input fields (add/remove dynamically)

Optional email notification using EmailJS

Stores tasks in Firebase with status = Pending

B. Task Management

View today’s tasks (pending + overdue)

Mark tasks as Done or Not Done

Edit tasks via modal

Delete tasks permanently

Overdue tasks highlighted in yellow

C. Custom Filters

Filter tasks by:

Single date

Date range

Employee ID

Status (Pending / Done)

Generates:

Task summary

Efficiency percentage

Table by employees

Task breakdown (details view)

D. Daily / Weekly / Monthly Summaries

Each summary view includes:

Efficiency calculation

Task counts (assigned, completed, pending)

Employee-wise breakdown

Detailed task list

Shareable summary via Web Share API or clipboard

E. Email Reporting

Supports four types:

Daily Summary

Weekly Summary

Pending Tasks

Custom Date Range Report

Features:

Auto-generate full email-ready content

Email preview panel

Copy-to-clipboard for managers

Direct send using EmailJS with fallback to mailto

F. Backup & Export

Export all task data as JSON backup

Export formatted CSV for Excel

Shows live data status (counts, storage info)

3. Technology Stack
Frontend

Vanilla HTML

Custom CSS (UI optimized for dashboard usage)

Vanilla JavaScript (Framework-free)

Backend

Firebase Realtime Database

Firebase Hosting (optional)

Email Delivery

EmailJS Browser SDK

Pre-configured Template ID, Service ID, Public Key

4. Project Structure
/project-root
│── index.html        # Complete Task Dashboard UI + JS logic
│── README.md         # Project documentation
│── assets/           # (Optional) Images, icons, CSS files
│── backups/          # (Optional) JSON/CSV exports


All logic is embedded into the single HTML file for simplicity and portability.

5. Setup Instructions
Step 1 — Clone the Repository
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>

Step 2 — Configure Firebase

Create a Firebase project → Realtime Database → Copy your config:

const firebaseConfig = {
  apiKey: "...",
  authDomain: "...",
  databaseURL: "...",
  projectId: "...",
  storageBucket: "...",
  messagingSenderId: "...",
  appId: "..."
};
firebase.initializeApp(firebaseConfig);


The app uses:

Realtime Database

Public read/write under authenticated environment

Step 3 — Configure EmailJS

Create account: https://emailjs.com

Then update:

const EMAILJS_PUBLIC_KEY = 'XXXX';
const EMAIL_SERVICE_ID   = 'service_xxxx';
const EMAIL_TEMPLATE_ID  = 'template_xxxx';


Template Variables required:

from_email
to_email
subject
message
from_name

Step 4 — Run the Dashboard

You can open the HTML file locally:

double click → index.html


Or deploy to Firebase Hosting:

firebase init
firebase deploy

6. How Data Flows
1. Assign Tasks

→ Saved into Firebase under /tasks/{autoKey}
→ UI auto-refreshes due to realtime listener

2. Manage Tasks

→ Lists tasks with status "Pending"
→ Marking task "Done" updates Firebase + adds completedDate

3. Reporting

→ Reads tasks from Firebase
→ Filters by date range & employee
→ Calculates efficiency, statistics
→ Generates ready-to-send email content

4. Backup

→ Exports tasks array to JSON or CSV

7. Key Functional Modules
A. Employee Profile Auto-Fill

Builds a profile map dynamically from all tasks.

B. Overdue Task Detection

Compares task.date < today’s date.

C. Dynamic Task Inputs

Add/remove unlimited tasks in assignment section.

D. Modal-Based Editing

Allows inline update of:

Employee ID

Name

Task description

Date

E. EmailJS Fallback

If EmailJS fails:
→ System opens mailto fallback automatically.

8. Screens & Components
Tabs:

Assign Tasks

Manage Tasks

Custom Filter

Daily Summary

Weekly Summary

Monthly Summary

Email Reports

Backup & Export

Each tab is controlled using JS and saved in LocalStorage for persistence.

9. Efficiency Formula
efficiency = (completed tasks / total tasks) × 100


Displayed in:

Progress bars

Summary tables

Email reports

10. Export Formats
JSON Backup
task-backup-YYYY-MM-DD.json

CSV Export

Columns:

Employee ID

Employee Name

Task Description

Date

Status

11. Future Enhancements (optional roadmap)

Role-based authentication (Admin, Employee)

Push notifications

Task attachment uploads

Analytics dashboards with charts

Mobile app version

Auto-reminders for overdue tasks

12. Author

Rakesh Ranjan
Task Automation & Productivity Tool Developer
Collegedunia.com
