# 🏥 Healthcare Analytics Project (Microsoft Fabric + Power BI)



## 📌 Project Overview

This project demonstrates a structured healthcare analytics workflow using Microsoft Fabric and Power BI.

The objective was to:

- Organize raw healthcare data using a Medallion-style structure
- Build a clean dimensional model (Fact + Dimensions)
- Implement basic pipeline orchestration with logging
- Apply Row-Level Security (RLS)
- Create a focused 2-page analytical dashboard

This is primarily a **data analytics project**, using Fabric tools to maintain proper structure and governance.

---

## 🏗 Data Architecture (Medallion Structure)

This project follows a simplified Medallion pattern:

### 🥉 Bronze Layer (Raw Data)

- Raw dataset uploaded into Lakehouse Files.
- Data copied into structured Bronze table using a pipeline.
- Purpose: Preserve raw data as-is for traceability.

---

### 🥈 Silver Layer (Clean & Structured Data)

Using **Dataflow Gen2**:

- Cleaned column names and data types
- Derived fields (YearMonth, Length of Stay)
- Created dimension tables:
  - `dim_date`
  - `dim_department`
  - `dim_doctor`
  - `dim_hospital`
  - `dim_payment`
- Created fact table:
  - `fact_admissions`

Purpose:
Prepare data for analytical modeling.

---

### 🥇 Gold Layer (Analytical Model)

- Star schema created inside Fabric.
- 1-to-many relationships between dimensions and fact table.
- Connected semantic model to Power BI Desktop via Lakehouse SQL Endpoint (Import Mode).

Purpose:
Enable efficient slicing and filtering for analysis.

---

## 🔄 Pipeline Orchestration

Three pipelines were created:

1. `PL_Ingestion_Bronze`
   - Copies raw file into Bronze table.

2. `PL_Transformation_Silver`
   - Runs Dataflow Gen2 to generate fact and dimension tables.

3. `PL_Master_Orchestration`
   - Invokes ingestion and transformation pipelines.
   - Includes basic failure logging using variables.

---

## ⚠ Failure Logging

Failure handling was added to simulate basic monitoring:

- On-failure activities
- Logging variables capturing ingestion and transformation failures

This demonstrates controlled execution rather than manual refresh.

---

## 🔐 Row-Level Security (RLS)

Static RLS implemented in Power BI.

Example:
- Province-based access restriction
- A role created to restrict data visibility by Province

Note:
This is a static demonstration of RLS, not dynamic user-based filtering.

---

## 📊 Reporting Structure (Power BI)

The final report contains 2 pages:

---

### 📈 Page 1 – Hospital Executive Summary

KPIs:
- Total Revenue
- Total Admissions
- Average Length of Stay
- Surgery Rate %

Visuals:
- Revenue trend (Year-Month)
- Admissions trend
- Revenue by Department
- Revenue by Province

Purpose:
Provide high-level performance overview.

---

### 📊 Page 2 – Operational Drivers & Resource Utilization

Visuals:
- Revenue by Treatment Type
- Procedure Mix (Surgery vs Non-Surgery)
- Avg Length of Stay by Department
- Top 5 Admissions by Diagnosis
- Revenue by Room Type

Purpose:
Explore operational and resource-related drivers.

---

## 🧠 Key Observations

- Average Length of Stay ≈ 5 days
- Surgery accounts for ~50% of admissions
- ICU and Semi-Private rooms generate higher revenue
- Revenue distribution across departments is relatively balanced
- Certain diagnoses consistently drive high admission volumes

---

## ⚙ Design Decisions & Constraints

- Fabric trial workspace had limited Git integration.
- Power BI Desktop was used for report portability.
- Static RLS chosen for demonstration purposes.
- Data and PBIX file backed up locally due to trial limitations.

---


## 📁 Repository Structure

```
Healthcare-Fabric-Analytics/
│
├── architecture/
├── data/
├── powerbi/
├── screenshots/
└── README.md
```

---

## 📸 Screenshots Included

- Pipeline execution
- Dataflow Gen2 design
- Star schema model
- Lakehouse tables
- Failure handling setup
- Executive dashboard
- Operational dashboard

---

## 🎯 What This Project Demonstrates

- Structured data preparation for analytics
- Dimensional modeling
- Use of Fabric tools for workflow management
- Basic monitoring and logging
- Role-based access control
- Focused, business-oriented reporting

---

## 👤 Author

**Shabin Pk**

🔗 LinkedIn: https://www.linkedin.com/in/shabinpengad  

---

## 🛠 Tools Used

- Microsoft Fabric  
  - Lakehouse  
  - Dataflow Gen2  
  - Fabric Pipelines  
  - Semantic Model  

- Power BI Desktop  

---
