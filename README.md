# 🚀 Sales Operations Reconciliation & Performance Analytics 
## 🖼️ Project Cover  
<!-- Replace with your project cover image -->
![Project Cover](INSERT_PROJECT_COVER_IMAGE_LINK_HERE)

## 📌 Project Overview  
This project delivers an **end-to-end Sales Operations analytics solution**, transforming fragmented field-reported sales and system records into **actionable operational intelligence**.

The objective was simple but critical:  
👉 **Can we trust our sales data? And if not, where is it breaking?**

Using **data cleaning, reconciliation analysis, and performance analytics**, this project exposes structural gaps in reporting and designs **control mechanisms to fix them at scale**.

---

## 🎯 Business Problem  
Sales teams reported **27,764 transactions**, while the system only contained **9,509 valid records**.

👉 That’s not a small mismatch — that’s a **systemic failure in data linkage and operational control**.

---

## 📊 Dataset Summary  
- **Reported Sales (Cleaned):** 27,764 rows  
- **System Records:** 9,509 rows  
- **Coverage:** Kenya, Tanzania, Nigeria, Ghana  
- **Matched Serials:** 3,781  
- **Unmatched Reported Serials:** 23,983

## 🧱 Data Model (RDBM)  
<!-- Replace with your data model image -->
![Data Model](INSERT_RDBM_IMAGE_LINK_HERE)
 
---

## 🧠 Methodology  

### 1️⃣ Data Cleaning & Consistency  
- Removed duplicate serial risks  
- Standardized formats (serials, names, structure)  
- Handled missing values (agent, channel, customer fields)  
- Validated serial integrity (format + completeness)

📦 **Deliverable:** Clean dataset ready for reconciliation  

---

### 2️⃣ Reconciliation Analysis  
- Compared **reported vs system records by country**  
- Identified:
  - Missing-in-system records  
  - Extra-in-system records  
- Quantified reconciliation gaps  

📊 **Key Finding:**  
> Only **3,781 / 27,764 (~13.6%)** reported sales match the system  

📉 **Implication:**  
This is **not timing noise** — it’s a **structural breakdown in data capture or system integration**

---

## 📊 Reconciliation Dashboard  
<!-- Replace with your reconciliation dashboard -->
![Reconciliation Dashboard](INSERT_RECON_DASHBOARD_IMAGE_LINK_HERE)

---

### 3️⃣ Sales Performance Analysis  
- Ranked performance by:
  - Country  
  - Agent  
  - Channel  

📊 **Key Insights:**  
- 🇳🇬 Nigeria = **12,514 units (45.1%) → dominant market**  
- Top agents contribute only **~8.5% → low concentration risk**  
- Channel visibility is weak (UNKNOWN dominates)

📉 **Critical Distortion:**  
> **11,334 rows (~40%) missing agent attribution**

👉 Performance analysis is **structurally unreliable**

---

## 📊 Sales Performance Dashboard  
<!-- Replace with your sales dashboard -->
![Sales Dashboard](INSERT_SALES_DASHBOARD_IMAGE_LINK_HERE)

---

### 4️⃣ Data Integrity & Risk Identification  

| Risk | Count | Severity | Business Impact |
|------|------|---------|----------------|
| Missing reported in system | 23,983 | 🔴 High | No traceability to source system |
| Missing agent attribution | 11,334 | 🔴 High | No accountability |
| Missing customer names | 23,300 | 🟠 Medium | No customer traceability |
| Missing channel data | 2,726 | 🟠 Medium | Weak route-to-market insight |
| Invalid serial formats | 5 | 🟠 Medium | Breaks reconciliation |
| Duplicate serials | 0 | 🟢 Low | No double-count risk |

📌 **Reality Check:**  
This is not just dirty data — it’s **missing operational controls**

---

## 🌍 Country-Level Insights  

- 🇳🇬 **Nigeria:**  
  - Highest volume driver  
  - Healthy agent distribution  
  - Core revenue engine  

- 🇰🇪 **Kenya:**  
  - System > Reported → **over-capture or under-reporting**  

- 🇹🇿 **Tanzania:**  
  - Agent data unusable → **performance blind spot**  

- 🇬🇭 **Ghana:**  
  - Over-concentrated attribution → **distorted productivity view**  

---

## ⚠️ Core Problem Diagnosis  

> ❌ The issue is NOT analytics  
> ❌ The issue is NOT tooling  
>  
> ✅ The issue is **control design failure at data entry and reconciliation layers**

---

## 🏗️ Solution Design (Operational Controls)  

### 1. Serial Validation at Entry  
- Mandatory serial input  
- Reject invalid/blank values  

💰 Value: Prevents bad data before it enters the system  

---

### 2. Daily Automated Reconciliation  
- Country-level serial matching  
- Exception reporting:
  - Missing in system  
  - Extra in system  
  - Invalid serials  

💰 Value: Moves from **monthly firefighting → daily control loop**

---

### 3. Master Data Standardization  
- Unified data dictionary  
- Same schema across all countries  

💰 Value: Eliminates structural mismatches  

---

### 4. Mandatory Agent & Channel Attribution  
- No sale without agent + channel  
- Supervisor override required  

💰 Value: Restores accountability  

---

### 5. Exception Resolution Workflow  
- Assigned ownership  
- SLA timelines  
- Weekly governance reviews  

💰 Value: Prevents backlog accumulation  

---


## 📈 Key Metrics  

- **Match Rate:** 13.6%  
- **Discrepancy Volume:** ~24K units  
- **Top Market Contribution:** Nigeria (45.1%)  
- **Agent Attribution Gap:** 40%+  

---

## 🧠 Strategic Insight  

> **You cannot scale analytics on top of broken data pipelines.**

Before dashboards →  
Before AI →  
Before automation →  

👉 Fix **data capture + reconciliation controls first**

---

## 🛠️ Tech Stack  

- **Excel** → Data cleaning & preparation  
- **Power BI** → Visualization & dashboards  
- **Data Modeling** → Relationship design for reconciliation  
- **Analytical Methods:**  
  - Reconciliation logic  
  - Variance analysis  
  - Data quality auditing  

---

## 📂 Repository Structure  
