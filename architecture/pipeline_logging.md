# 🔄 Pipeline Orchestration & Failure Logging

This document explains how pipeline execution and failure handling were implemented in the Healthcare Analytics project.

---

## 📌 Pipeline Structure

Three pipelines were created:

### 1️⃣ PL_Ingestion_Bronze
Purpose:
- Copies raw healthcare dataset from Lakehouse Files
- Loads it into Bronze table inside Lakehouse

---

### 2️⃣ PL_Transformation_Silver
Purpose:
- Executes Dataflow Gen2
- Generates cleaned Silver layer
- Produces:
  - `fact_admissions`
  - All dimension tables (`dim_*`)

---

### 3️⃣ PL_Master_Orchestration
Purpose:
- Acts as the main controller pipeline
- Invokes:
  - `PL_Ingestion_Bronze`
  - `PL_Transformation_Silver`
- Ensures controlled execution flow

Execution Order:

PL_Master_Orchestration  
→ PL_Ingestion_Bronze  
→ PL_Transformation_Silver  

---

## ⚠ Failure Handling Implementation

Basic failure logging was implemented to simulate monitoring behavior.

### 🔹 Approach Used

- Added **On Failure** paths from:
  - Ingestion pipeline
  - Transformation pipeline
- Connected to `Set Variable` activities
- Variables capture failure messages

Example:
- If ingestion fails → `Log_Ingestion_Failure`
- If transformation fails → `Log_Transformation_Failure`

This ensures:

- Failures are not silent
- Execution status is traceable
- Controlled orchestration flow

---

## 🧠 Why This Was Implemented

Although this is an analytics-focused project, pipeline logging demonstrates:

- Structured execution control
- Basic observability
- Reduced reliance on manual refresh
- Awareness of production-style workflow patterns

---

## 📌 Note

This is a simplified logging implementation for demonstration purposes.

It does not include:
- External monitoring services
- Alerting systems
- Log storage in separate logging tables

The objective was to simulate controlled execution behavior within Fabric.

---
