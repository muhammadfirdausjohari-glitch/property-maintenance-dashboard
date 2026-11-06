# Property Maintenance Database & Dashboard Pipeline

AppSheet & Looker Studio property maintenance database and dashboard pipeline.

---

## 📌 Problem Statement
Field water meter readings and residential maintenance logs were recorded manually on paper. This led to data entry errors, delayed reporting, and a lack of real-time visibility into maintenance completion metrics.

---

## 🏗️ Solution Architecture
1. **Data Collection (AppSheet):** Mobile interface built for field staff to record readings, attach photos, and auto-validate inputs.
2. **Data Pipeline (Google Sheets / Supabase):** Asynchronous cloud sync to maintain structured database records.
3. **Visualization (Looker Studio):** Interactive dashboard tracking maintenance completion rates, identifying unit bottlenecks, and surfacing usage trends.

---

## 📱 AppSheet Mobile User Interface

The mobile application provides custom field interfaces for logging maintenance complaints, recording water meter readings, and attaching technician reports.

| Navigation Menu | Active Complaints List |
| :---: | :---: |
| ![App Navigation](Navigation.png) | ![Active Complaints](Active_complain.png) |

| Water Meter Readings | Technician Reports & Attachments |
| :---: | :---: |
| ![Meter Readings](Meter_readings.png) | ![Technician Report](Tech_report.png) |

---

## ⚙️ Key AppSheet Functions & Logic

```appsheet
/* 1. Automated Reference Lookup for Linked Complaint ID */
LOOKUP([_THISROW].[Related_Complaint_ID], "Active Complaint list", "COMPLAINT_ID", "UNIT_NO")

/* 2. Dynamic Priority Formatting Rules */
IFS(
  [PRIORITY] = "High", "#FF0000",
  [PRIORITY] = "Medium", "#FFA500",
  [PRIORITY] = "Low", "#008000"
)

/* 3. Auto-Generated Timestamp on Completion */
IF(ISNOTBLANK([COMPLETION_DATE]), NOW(), "")
