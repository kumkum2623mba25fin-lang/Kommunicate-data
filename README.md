# Automated Credit Risk Assessment & Application Workflow

An end-to-end automated pipeline built with **n8n** and **Orange Data Mining** that trains a predictive risk model, ingests financial application data from **Google Sheets**, evaluates applicants through multi-tiered conditional logic, and sends automated decision notifications via **Gmail**.

---

## 🚀 System Architecture & Workflow

The entire automation engine is driven by an asynchronous node-based workflow in n8n. It processes batch applications sequentially, passing them through structured evaluation matrices (`IF` filters) to arrive at three primary states: **Auto-Approve**, **Manual Review**, or **Auto-Reject**.

### Workflow Visual Map
<img src="./workflow.jpeg" alt="n8n Automated Decisioning Workflow" width="100%"/>

### Workflow Breakdown
1. **Trigger**: Manually executed or webhook-driven initiation (`When clicking 'Execute workflow'`).
2. **Data Ingestion**: Pulls raw applicant profiles from a secure Google Sheet ledger.
3. **Conditional Logic Filters (`If`, `If1`, `If2`, `If3`)**: 
   * Segregates applications based on risk factors such as credit health, baseline income tiering, and debt leverage ratios.
   * Out of 40 baseline items initialized, applications are successfully bucketed into specific validation branches.
4. **Data Synchronization & Notification**: Writes final pipeline updates back to the respective sheets while triggering personalized transactional emails.

---

## 🤖 FinBot Conversational Interface

To complement backend automated decisioning, frontline customer inquiries are handled by **FinBot**—an AI-powered Applied Finance Assistant integrated directly via the **Kommunicate** conversational widget.

### Live Chat Widget Interface
<img src="./WhatsApp Image 2026-06-11 at 8.33.12 PM.jpeg" alt="FinBot Kommunicate Integration Interface" width="100%"/>

### Core Functional Capabilities
* **Financial Ratios**: Instantly calculates and interprets corporate or retail accounting metrics for users.
* **Investment Planning**: Explains asset allocations and foundational financial planning strategies.
* **Loan Guidance**: Helps applicants navigate initial borrowing minimums, matching the exact backend thresholds enforced by the n8n pipeline.

---

## 🧠 Predictive Modeling Pipeline (Orange)

Before applications enter the live automation routing, risk evaluation thresholds are validated using a predictive machine learning pipeline designed in **Orange Data Mining**. This layer tests classification stability to ensure decision logic boundaries are mathematically sound.

### Data Science Canvas
<img src="./WhatsApp Image 2026-06-11 at 13.56.30.jpeg" alt="Orange Data Mining Predictive Workflow" width="100%"/>

### Model Components
* **File Node**: Ingests historical credit application training profiles.
* **Select Columns**: Sets the target classification variable (e.g., `System_Initial_Decision`) and isolates key predictive features like credit score and DTI ratios.
* **Logistic Regression**: Trains a generalized linear classification model to calculate risk probabilities.
* **Test and Score**: Evaluates model accuracy, AUC-ROC statistics, and confusion matrices prior to production logic deployment.

---

## 📊 Dataset Structure (Google Sheets)

The underlying decision logic evaluates financial metrics across multiple columns to flag anomalies, compliance warnings, or immediate rejections.

### Input Data Profile
<img src="./Screenshot (19).png" alt="Google Sheets Application Database" width="100%"/>

| Column Name | Description | Key Target Thresholds Evaluated |
| :--- | :--- | :--- |
| `Annual_Income` | Total gross yearly earnings | Evaluated for low-income tier audits |
| `Credit_Score` | Creditworthiness score (300 - 850) | Triggers `FAIL_CRITICAL_CREDIT` if under floor limits |
| `Debt_To_Income_Ratio` | Monthly debt obligations vs income ratio | Triggers ceiling violations if excessively high |
| `Watchlist_Match` | Compliance / AML background database matching | High percentages force automated rejection |
