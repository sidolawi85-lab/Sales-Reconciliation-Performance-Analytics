# 🚀 Sales Operations Reconciliation & Performance Analytics

## 🖼️ Project Cover  
<!-- Replace with your project cover image -->
![Project Cover](INSERT_PROJECT_COVER_IMAGE_LINK_HERE)

---

## 📌 Project Overview  
This project delivers an **end-to-end Sales Operations analytics solution** built to answer a hard operational question:

> **Can the business trust what sales teams report against what the system actually records?**

At face value, this looks like a reporting task. In reality, it is an **operational control problem disguised as an analytics problem**.

The project combines:
- **data cleaning**
- **record reconciliation**
- **sales performance analysis**
- **data integrity auditing**
- **control design recommendations**

to turn fragmented field-reported sales and system records into **decision-grade operational intelligence**.

This was not simply a dashboard exercise. It was a structured attempt to diagnose where the commercial data pipeline was breaking, quantify the size of the breakdown, and show what management would need to fix before scaling reporting, automation, or advanced analytics.

---

## 🎯 Business Problem  
The starting point was a major mismatch between what the field reported and what the system captured.

Sales teams reported **27,764 transactions**, while the system contained only **9,509 valid records**. That means the business was not dealing with a minor discrepancy or a small timing lag. It was dealing with a material breakdown in transaction traceability. :contentReference[oaicite:2]{index=2}

This creates several strategic risks:

- **Revenue visibility risk**  
  If reported transactions cannot be traced back to the system, management cannot tell whether performance is real, delayed, duplicated, or simply missing.

- **Accountability risk**  
  When agent attribution and channel data are incomplete, performance management becomes unreliable and incentive decisions become distorted.

- **Audit and control risk**  
  Missing or invalid serials weaken traceability, making it difficult to verify the authenticity and completeness of transactions.

- **Decision-making risk**  
  If the reporting layer is unstable, downstream dashboards may look polished while still being structurally misleading.

In simple terms:

> The business was trying to manage sales performance on top of a data foundation that could not yet be fully trusted.

---

## 📊 Dataset Summary  
The analysis was built around two core data streams:

### 1. Field-Reported Sales  
These are transactions reported by country sales operations teams and field structures.

- **Reported Sales (Cleaned):** 27,764 rows  
- **Coverage:** Kenya, Tanzania, Nigeria, Ghana

### 2. System Records  
These represent the system-side reference records used to verify whether reported sales can actually be found in the operational data environment.

- **System Records:** 9,509 valid rows

### Reconciliation Snapshot  
- **Matched Serials:** 3,781  
- **Unmatched Reported Serials:** 23,983  
- **Reporting Match Rate:** 13.6%  
- **Total Discrepancies:** ~24K  
- **Reported Units:** ~28K  
- **System Units:** ~10K :contentReference[oaicite:3]{index=3} :contentReference[oaicite:4]{index=4}

### Why these numbers matter  
A 13.6% match rate means that only a small fraction of reported sales can be directly tied back to the system. That does **not** support the interpretation of a healthy, fully governed reporting process. It points to a structural disconnect between field capture and system recording.

This disconnect may include:
- missing uploads
- data-entry failures
- serial formatting issues
- inconsistent country-level schemas
- delays in capture
- incomplete reference fields
- reconciliation processes happening too late or not at all

---

## 🧱 Data Model (RDBM)  
<!-- Replace with your data model image -->
![Data Model](INSERT_RDBM_IMAGE_LINK_HERE)

### Data Model Logic  
The model is built around serial-level traceability.

At the core of the design is the assumption that a sale should be identifiable through a key transaction reference, in this case the **serial number**. That serial becomes the bridge between:

- **reported sales records**
- **system-side records**
- **reconciliation status**
- **data quality flags**
- **performance reporting**

### Core entities in the model  
The project structure can be understood as four logical layers:

#### 1. Raw Reported Sales Tables  
Country-specific source tables for:
- Kenya
- Tanzania
- Nigeria
- Ghana

These feeds vary in structure, field naming, completeness, and formatting.

#### 2. Clean Reported Data  
A standardized, formula-driven consolidation layer that harmonizes:
- serial number
- country
- survey region / location
- customer
- agent
- date
- channel
- product type

This layer also creates validation and audit flags.

#### 3. Clean System Data  
A standardized system-side reference table with aligned serial structure and matching logic.

#### 4. Analytical Summary Layer  
A reporting layer used to drive:
- reconciliation metrics
- performance metrics
- data integrity summaries
- country comparisons
- dashboard visuals

### Why this model matters  
Without a proper relational logic, reconciliation becomes superficial. The model ensures that the analysis is not just counting rows, but actually testing **record presence, record integrity, and operational consistency**.

---

## 🧠 Methodology  

### 1️⃣ Data Cleaning & Consistency  

The first challenge was not analysis. It was **making the data analytically usable**.

The source files came with the kinds of issues typical in real operations:
- inconsistent naming
- blank fields
- mixed schemas across countries
- unreliable agent/channel completion
- serial formatting problems
- fields that required normalization before comparison

### Cleaning objectives  
The cleaning layer was designed to do four things:

#### A. Standardize structure  
Fields from different country files were aligned into a common schema so that all records could be analyzed together.

#### B. Normalize values  
Text fields were standardized using formula-based cleaning logic such as trimming spaces, replacing blanks, and forcing consistent field population rules.

#### C. Preserve auditability  
Instead of freehand manual edits, the cleaning approach was designed to preserve logic in a transparent, repeatable way so that downstream auditing could trace how data was prepared.

#### D. Generate control flags  
The cleaning layer did not merely prepare the data. It also created audit columns that could diagnose problems, such as:
- missing field count
- duplicate serial checks
- cross-customer duplicate logic
- reconciliation readiness flags
- system match status
- serial validity status

### What was cleaned  
The dataset was standardized around these core fields:

- Serial number
- Country
- Survey region / Location
- Customer
- Agent
- Date
- Channel
- Product Type

### Data quality logic applied  
The cleaning process included:
- blank handling
- “Unknown” standardization for missing text fields
- serial validation
- duplicate detection
- reconciliation flagging
- cross-source lookup logic

### Deliverable  
A **cleaned analytical dataset** that was ready for:
- reconciliation analysis
- performance analysis
- integrity auditing
- dashboarding

This matters because poor reconciliation analysis usually begins with poor cleaning discipline. If the cleaning layer is weak, every chart built on top of it becomes suspect.

---

### 2️⃣ Reconciliation Analysis  

Once the data was cleaned, the next task was to compare what the field reported against what the system actually contained.

### Reconciliation question  
For each reported sale:

> **Can this serial be found in the system?**

That question was used to classify records into:
- **Matched**
- **Missing in System**

The system-side data was also analyzed in reverse to detect:
- **Extra in System**

### Why bidirectional reconciliation matters  
A one-way comparison only tells part of the story.

- If a reported serial is missing from the system, that suggests a reporting-to-system gap.
- If a system serial exists without a corresponding reported record, that suggests under-reporting, timing delays, or separate process capture.

A robust reconciliation process must test both.

### Key finding  
Only **3,781 out of 27,764 reported transactions** matched the system, translating to a **13.6% match rate**. :contentReference[oaicite:5]{index=5}

### What this means  
This result is too large to be dismissed as normal timing variance.

A discrepancy rate at this scale suggests structural issues such as:
- weak serial capture discipline
- poor synchronization between reporting and system entry
- fragmented operating processes across markets
- inconsistent country-level workflows
- delayed reconciliation cycles
- missing data governance standards

### Why this is operationally significant  
Reconciliation is not just an accounting exercise. In field operations, it is a control mechanism. It tells management whether the business can trust that what was sold, reported, and recorded all refer to the same underlying event.

In this project, the reconciliation analysis showed that this control was not functioning at the required level.

---

## 📊 Reconciliation Dashboard  
<!-- Replace with your reconciliation dashboard -->
![Reconciliation Dashboard](INSERT_RECON_DASHBOARD_IMAGE_LINK_HERE)

### Dashboard interpretation  
The reconciliation dashboard summarizes the scale and shape of the reporting breakdown:

- **Reported Units:** ~28K  
- **System Units:** ~10K  
- **Total Discrepancies:** ~24K  
- **Reporting Match Rate:** 13.6% :contentReference[oaicite:6]{index=6}

### What the country visuals reveal  
The dashboard also shows discrepancy patterns by country and variance breakdowns between:
- **Missing in System**
- **Extra in System**

This is important because the problem is not evenly distributed. Some countries show more severe reconciliation weakness than others, which suggests the issue is not purely technical. It is likely also process-dependent.

### Strategic reading of the dashboard  
The reconciliation dashboard should be interpreted as a **control map**, not just a reporting summary.

It tells leadership:
- where reporting leakage is concentrated
- where field processes are weakest
- where audit risk is highest
- where daily exception management should begin

---

### 3️⃣ Sales Performance Analysis  

After testing whether sales could be trusted structurally, the project then examined how reported sales were distributed across:
- countries
- agents
- channels

### Why performance analysis was still necessary  
Even when a dataset has integrity issues, performance analysis is still useful because it reveals whether business decisions are being made on distorted visibility.

The goal here was not just to rank performance, but to ask:

> **How much of the performance story is actually trustworthy?**

### Country-level performance  
Nigeria emerged as the largest reported volume contributor at **12,514 units**, representing **45.1%** of total reported units. Tanzania followed as another high-volume market, with Kenya and Ghana operating at smaller reported volumes. :contentReference[oaicite:7]{index=7}

### Agent concentration analysis  
The dashboard shows a **Top 5 Agent Contribution of 51.05%**, and also flags a **high concentration risk**. :contentReference[oaicite:8]{index=8}

This is a critical result, but it needs interpretation.

At first glance, high contribution by a small number of agents may suggest overdependence on a few performers. However, the analysis is distorted by missing attribution and “UNKNOWN” records. That means the concentration result must be read with caution.

### Channel performance  
Channel mix is heavily dominated by:
- **B2C**
- followed by **UNKNOWN**
- with **B2B** contributing only a small share :contentReference[oaicite:9]{index=9}

This raises a major commercial visibility issue.

If “UNKNOWN” is materially present as a channel category, then route-to-market analysis becomes less reliable. Management may think they are seeing channel performance, but they are actually seeing an incomplete classification structure.

### The distortion problem  
The single most important limitation in the performance layer is that **11,334 rows — over 40% of the dataset — are missing agent attribution**. :contentReference[oaicite:10]{index=10}

That means:
- agent rankings are incomplete
- coaching/accountability insights are weakened
- territory performance becomes harder to validate
- incentive analysis becomes exposed to misclassification

So while the performance dashboard is valuable, it also demonstrates why **control quality must come before performance interpretation**.

---

## 📊 Sales Performance Dashboard  
<!-- Replace with your sales dashboard -->
![Sales Dashboard](INSERT_PROJECT_COVER_IMAGE_LINK_HERE)

<!-- Replace with your sales dashboard -->
![Sales Dashboard](INSERT_SALES_DASHBOARD_IMAGE_LINK_HERE)

### Dashboard interpretation  
The sales performance dashboard provides a view into:
- total units sold
- top agent contribution
- units sold by channel
- ranked agent performance
- units sold by country
- concentration risk signals :contentReference[oaicite:11]{index=11}

### Key reads from the dashboard  
#### Total units sold  
The dashboard summarizes total reported sales at roughly **28K units**. This is the volume layer that leadership would ordinarily use to assess market activity.

#### Country performance  
Nigeria is the dominant volume driver. That matters commercially, because it tells leadership where the largest sales engine currently sits.

#### Agent table  
The ranked agent table highlights a hard truth: some of the largest “performers” are actually driven by missing attribution categories such as **UNKNOWN**, especially in Tanzania. That means the dashboard is not just showing performance. It is also visualizing data quality failure.

#### Channel split  
With B2C dominating and UNKNOWN still materially present, the business cannot claim full route-to-market visibility.

### Final interpretation  
The performance dashboard is useful, but its deeper value is diagnostic:

> it shows not only who is selling, but also where the business lacks the structural data needed to evaluate performance fairly.

---

### 4️⃣ Data Integrity & Risk Identification  

This section moves beyond reconciliation and performance to ask a broader question:

> **What specific data quality risks are preventing this sales operation from being controlled properly?**

The integrity review identified the following issues:

| Risk | Count | Severity | Business Impact |
|------|------|---------|----------------|
| Missing reported in system | 23,983 | 🔴 High | No traceability to source system |
| Missing agent attribution | 11,334 | 🔴 High | No accountability |
| Missing customer names | 23,300 | 🟠 Medium | No customer traceability |
| Missing channel data | 2,726 | 🟠 Medium | Weak route-to-market insight |
| Invalid serial formats | 5 | 🟠 Medium | Breaks reconciliation |
| Duplicate serials | 0 | 🟢 Low | No double-count risk | :contentReference[oaicite:12]{index=12}

### Deep interpretation of each risk  

#### 1. Missing reported in system — 23,983  
This is the largest and most serious issue in the dataset.

It means the majority of reported sales cannot be traced to the system. That weakens confidence in:
- operational reporting
- auditability
- downstream performance analytics
- control enforcement

#### 2. Missing agent attribution — 11,334  
Without agent data, there is no clean accountability structure for a large part of the dataset.

This damages:
- agent performance rankings
- productivity analysis
- coaching and territory management
- incentive credibility

#### 3. Missing customer names — 23,300  
Customer-level incompleteness means reported transactions often cannot be easily linked to an identifiable end record. That limits customer traceability and weakens downstream audit investigations.

#### 4. Missing channel data — 2,726  
This reduces visibility into where sales are actually coming from and undermines commercial channel analysis.

#### 5. Invalid serial formats — 5  
Although the count is small, the risk is important. Serial integrity is foundational to reconciliation. Even a small number of malformed serials can break lookup logic and introduce matching errors.

#### 6. Duplicate serials — 0  
This is the one encouraging sign in the integrity layer. It suggests that outright duplicate double-count risk is not the primary issue. The bigger issue is **missingness and misalignment**, not over-duplication.

### Reality check  
The project’s most important integrity conclusion is this:

> This is not simply a dirty dataset. It is a dataset reflecting weak operational controls.

---

## 🌍 Country-Level Insights  

The country view helps translate data issues into operational realities.

### 🇳🇬 Nigeria  
Nigeria is the largest reported sales contributor, accounting for roughly **45.1%** of total reported volume. This makes it the core revenue engine in the analysis. :contentReference[oaicite:13]{index=13}

**What this means strategically:**  
Because Nigeria drives the largest share of reported sales, improvements here would have the biggest absolute impact on reporting quality and operational visibility.

### 🇰🇪 Kenya  
Kenya shows a case where **system records exceed reported activity**, suggesting:
- over-capture in the system
- under-reporting from the field
- or process timing differences between reporting and system entry :contentReference[oaicite:14]{index=14}

**What this means strategically:**  
Kenya may require investigation into reporting discipline, submission timing, and data handoff controls.

### 🇹🇿 Tanzania  
Tanzania presents a serious attribution problem. Agent visibility is weak enough that performance interpretation becomes unreliable. In practice, this creates a major blind spot for productivity management. :contentReference[oaicite:15]{index=15}

**What this means strategically:**  
Tanzania needs mandatory attribution controls before any serious agent-level performance management can be trusted.

### 🇬🇭 Ghana  
Ghana appears more concentrated in agent attribution, which may distort productivity interpretation if management assumes the distribution is broader than it really is. :contentReference[oaicite:16]{index=16}

**What this means strategically:**  
Ghana requires closer review of whether concentration reflects true productivity or reporting structure bias.

---

## ⚠️ Core Problem Diagnosis  

The central diagnosis of this project is straightforward:

> ❌ The issue is **not** dashboarding  
> ❌ The issue is **not** Power BI  
> ❌ The issue is **not** the lack of sophisticated analytics  
>
> ✅ The issue is a **control design failure at the data entry, data capture, and reconciliation layers**. :contentReference[oaicite:17]{index=17}

This matters because many organizations respond to poor reporting by asking for:
- better dashboards
- automation
- AI insights
- more reporting frequency

But none of those solve the root problem if:
- key fields are missing
- serials are not captured correctly
- reporting and system layers are not aligned
- exception handling is weak or absent

The project therefore reframes the challenge from an analytics issue into an operational governance issue.

---

## 🏗️ Solution Design (Operational Controls)  

The analysis led to five control recommendations.

### 1. Serial Validation at Entry  
Every reported sale should require a valid serial number at the point of entry.

**Design principle:**  
Reject bad data before it enters the process.

**Why it matters:**  
Reconciliation cannot function if the core transaction key is missing or malformed.

**Control recommendation:**  
- mandatory serial field
- format validation
- no blank or placeholder acceptance
- exception route for supervisor review

**Business value:**  
Prevents invalid data from flowing downstream into dashboards and audit processes. :contentReference[oaicite:18]{index=18}

---

### 2. Daily Automated Reconciliation  
Reconciliation should not wait until month-end or ad hoc review cycles.

**Design principle:**  
Turn reconciliation into a daily control loop.

**What it should do:**  
- match serials by country
- flag missing in system
- flag extra in system
- flag invalid serials
- generate exception lists for action owners

**Business value:**  
Moves the business from delayed firefighting to continuous operational control. :contentReference[oaicite:19]{index=19}

---

### 3. Master Data Standardization  
Country-level data structures must be harmonized.

**Design principle:**  
One business cannot operate with four different data languages for the same commercial event.

**What it should include:**  
- standardized field names
- controlled value lists
- unified country schema
- common data dictionary

**Business value:**  
Eliminates structural mismatches and improves comparability across markets. :contentReference[oaicite:20]{index=20}

---

### 4. Mandatory Agent & Channel Attribution  
Every sale should carry agent and channel data unless explicitly escalated.

**Design principle:**  
No attribution, no trusted performance analysis.

**What it should include:**  
- required agent field
- required channel field
- controlled exceptions only
- supervisor override with reason logging

**Business value:**  
Restores accountability, supports performance evaluation, and protects channel strategy analysis. :contentReference[oaicite:21]{index=21}

---

### 5. Exception Resolution Workflow  
Finding exceptions is not enough. The business must have a process to resolve them.

**Design principle:**  
A control without ownership is not a real control.

**What it should include:**  
- assigned owner by issue type
- SLA for resolution
- weekly governance review
- backlog tracking
- escalation path for unresolved items

**Business value:**  
Prevents discrepancy accumulation and makes reconciliation a managed operating rhythm. :contentReference[oaicite:22]{index=22}

---

## 📈 Key Metrics  

The core performance and control indicators from the project are:

- **Reported Units:** ~28K  
- **System Units:** ~10K  
- **Match Rate:** 13.6%  
- **Discrepancy Volume:** ~24K  
- **Top Market Contribution:** Nigeria (45.1%)  
- **Top 5 Agent Contribution:** 51.05%  
- **Agent Attribution Gap:** 40%+  
- **Missing-in-System Records:** 23,983  
- **Missing Channel Data:** 2,726  
- **Invalid Serial Formats:** 5 :contentReference[oaicite:23]{index=23} :contentReference[oaicite:24]{index=24}

### Why these metrics matter  
These are not just descriptive numbers. Together they show a business where:
- commercial activity is happening
- reporting exists
- dashboards can be built

but the **control layer underneath is weak enough to distort interpretation**.

---

## 🧠 Strategic Insight  

The most important strategic takeaway from the project is:

> **You cannot scale analytics on top of broken data pipelines.** :contentReference[oaicite:25]{index=25}

Before:
- dashboards
- automation
- AI copilots
- predictive models
- advanced sales optimization

the business must first fix:
- data capture discipline
- reference key integrity
- attribution completeness
- reconciliation cadence
- exception ownership

This is why the project is valuable beyond reporting.

It shows the transition from:
**“build a dashboard”**  
to  
**“design a control system the business can trust.”**

---

## 🛠️ Tech Stack  

- **Excel** → Data cleaning, formula-driven standardization, audit logic, reconciliation preparation  
- **Power BI** → Data model, visual analytics, country/agent/channel dashboards  
- **Data Modeling** → Serial-based matching logic and summary-table design  
- **Analytical Methods**  
  - reconciliation logic  
  - variance analysis  
  - data quality auditing  
  - concentration analysis  
  - control-gap diagnosis :contentReference[oaicite:26]{index=26}

### Why this stack was appropriate  
This stack reflects real-world operational analytics work:

- Excel handled the preparation and control logic
- Power BI handled the visualization and insight layer
- the analytical framework connected the two into a business diagnosis

This is exactly the kind of setup often used in fast-moving operations teams before heavier data engineering infrastructure is put in place.

---

