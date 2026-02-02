# Smart Library Integration Architecture
### Enterprise Architecture Design using TOGAF ADM

![Status](https://img.shields.io/badge/Status-Completed-success)
![Framework](https://img.shields.io/badge/Framework-TOGAF%20ADM-blue)

## Executive Summary
This project outlines the Enterprise Architecture (EA) design for transforming the library services at **UIN Syarif Hidayatullah Jakarta**.

The core objective was to solve the data silo problem between the **Academic Information System (AIS)** and the **Library Management System (LMS)**. By designing a real-time integration architecture, this solution enables a **Self-Service Kiosk** ecosystem where students can validate their membership instantly using their Student ID (KTM), eliminating manual paperwork.

---

## The Challenge (The "Before" State)
Based on business process analysis, the library faced significant operational bottlenecks:
* **Data Silos:** The library system did not have direct access to the university's active student database.
* **Manual Redundancy:** Students had to fill out physical forms to register as library members, even though they were already enrolled in the university.
* **Inefficiency:** The manual validation process took **5-10 minutes per student**, causing long queues during peak periods.

---

## The Solution (Architecture Vision)
I utilized the **TOGAF ADM (Architecture Development Method)** to design a holistic solution.

### 1. The Core Concept
* **Single Identity:** Use the Student ID Card (KTM) as the single source of truth.
* **Real-Time Validation:** Replace local data storage with real-time API calls to the Academic System.
* **Secure Network:** All data traffic flows through a secure Intranet (VLAN) to protect student privacy.

### 2. High-Level Architecture Diagram
The architecture bridges the frontend (Kiosk) and backend (Academic Database) using an API Gateway.

<img width="369" height="572" alt="image" src="https://github.com/user-attachments/assets/2c7411fe-9604-4252-a699-986ff368ccfd" />


---

## Technical Specifications

### A. Integration Logic (API Design)
As the System Analyst, I defined the **API Contract** to ensure the Kiosk and Academic System communicate standard JSON data.

**Endpoint:** `GET /api/v1/students/validate/{nim}`

**Response Structure (JSON):**
```json
{
  "response_code": 200,
  "timestamp": "2025-12-20T14:30:00Z",
  "data": {
    "student_id": "11230930000068",
    "full_name": "Maura Adha Salsabillah",
    "faculty": "Science and Technology",
    "status": "ACTIVE",
    "library_eligibility": true
  },
  "message": "Validation successful. Access granted."
}
```

### B. Data Flow Architecture
1.  **Input:** User scans Barcode/RFID on the Kiosk.
2.  **Request:** Kiosk sends encrypted request to API Gateway via Intranet.
3.  **Processing:** API Gateway queries the Academic Database (AIS).
4.  **Decision:**
    * If `status == ACTIVE`: Kiosk unlocks gate/menu.
    * If `status == INACTIVE`: Kiosk shows "Access Denied" message.

---

## Business Process Improvement
We modeled the efficiency gains using **BPMN** (Business Process Model and Notation).

| Metric | Traditional Process | Smart Library Process (Proposed) | Improvement |
| :--- | :--- | :--- | :--- |
| **Verification Method** | Manual (Human Check) | Automated (System API) | **Automated** |
| **Validation Time** | 5 - 10 Minutes | < 5 Seconds | **99% Faster** |
| **Data Accuracy** | Risk of Human Error | 100% Accurate (Single Source) | **High Integrity** |
| **Paper Usage** | High (Registration Forms) | Zero (Paperless) | **Eco-Friendly** |

---

## Tools & Standards Used
* **Framework:** TOGAF ADM (Preliminary to Technology Phase).
* **Modeling Tools:** Draw.io / Python (for architecture diagrams).
* **Documentation:** UML (Use Case, Class Diagram, Sequence Diagram).
* **Protocol:** RESTful API (JSON) over HTTPS.
* **Hardware Spec:** Touchscreen Kiosk with 2D Barcode Scanner.

---

## Documentation Reference
This repository contains the digital artifacts of the analysis:
* 📂 `/diagrams` - High-resolution UML and TOGAF diagrams.
* 📂 `/docs` - The comprehensive PDF report of the architecture design.
* [Open in Draw.io](https://app.diagrams.net/?#Uhttps://github.com/USERNAME/NAMA-REPO/raw/main/NAMA-FILE.drawio) - The visualization of use case diagram and kiosk's lend and return BPMN

---
