# 🏥 AI-Powered Australian Healthcare Data Enrichment

An end-to-end **healthcare data engineering and AI enrichment project** that collects Australian medical practice information, cleans and validates the data, and uses **AI-assisted prompt engineering** to transform unstructured healthcare service information into structured, analysis-ready data.

---

## 📌 Project Overview

Healthcare information available on clinic websites is often presented in an inconsistent and unstructured format.

This project demonstrates how to build a practical data pipeline that:

**Web Source → Data Collection → Data Cleaning → Data Validation → AI Enrichment → Structured Dataset**

The project focuses on Australian GP and medical practices and converts publicly available clinic information into a structured dataset containing standardized healthcare services and telehealth availability.

### 🎯 Objective

To create a reliable, structured dataset of Australian medical practices by combining:

- Web scraping
- Data cleaning and validation
- Python-based data processing
- AI-assisted data enrichment
- Prompt engineering
- Data quality checks
- Structured CSV/Excel outputs

---

## 🚀 Key Features

- 🌐 Automated extraction of medical practice information
- 🐍 Python-based data collection and processing
- 🔎 Selenium and BeautifulSoup for web scraping
- 🧹 Data cleaning and duplicate removal
- 🤖 AI-assisted healthcare service categorization
- ✨ Prompt engineering with iterative refinement
- 📊 Structured, analysis-ready dataset
- 🔍 Source traceability using source URLs
- ✅ Data quality validation
- 📄 Prompt engineering documentation

---

## 🏗️ Project Architecture

```text
                 ┌──────────────────────────┐
                 │ Family Doctor Australia  │
                 │     Clinic Directory     │
                 └─────────────┬────────────┘
                               │
                               ▼
                 ┌──────────────────────────┐
                 │ Selenium Web Scraping    │
                 │ + BeautifulSoup         │
                 │ + JSON-LD Extraction    │
                 └─────────────┬────────────┘
                               │
                               ▼
                 ┌──────────────────────────┐
                 │     Raw Clinic Data      │
                 │ Practice / Phone /       │
                 │ Address / Hours /        │
                 │ Services / Source URL    │
                 └─────────────┬────────────┘
                               │
                               ▼
                 ┌──────────────────────────┐
                 │ Data Cleaning &          │
                 │ Quality Validation       │
                 │                          │
                 │ • Missing values        │
                 │ • Duplicate records     │
                 │ • Address cleanup       │
                 │ • URL validation        │
                 └─────────────┬────────────┘
                               │
                               ▼
                 ┌──────────────────────────┐
                 │     AI Enrichment        │
                 │                          │
                 │ • Service categories    │
                 │ • Telehealth status      │
                 │ • Prompt engineering     │
                 └─────────────┬────────────┘
                               │
                               ▼
                 ┌──────────────────────────┐
                 │     Final Dataset        │
                 │                          │
                 │ Structured &             │
                 │ Analysis-Ready Data      │
                 └──────────────────────────┘
```

---

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| **Python** | Data collection, processing and transformation |
| **Selenium** | Dynamic webpage extraction |
| **BeautifulSoup** | HTML parsing |
| **JSON-LD** | Extracting structured webpage information |
| **Pandas** | Data cleaning and transformation |
| **AI / LLM** | Healthcare service enrichment |
| **Prompt Engineering** | Controlled and evidence-based AI extraction |
| **Jupyter Notebook** | Development and experimentation |
| **CSV / Excel** | Final structured data output |
| **GitHub** | Version control and project documentation |

---

## 📂 Dataset

The final dataset contains structured information for **86 unique medical practice records**.

### Final Dataset Fields

| Field | Description |
|---|---|
| `practice_name` | Name of the medical practice |
| `phone` | Official contact number extracted from the source |
| `full_address` | Practice address |
| `opening_hours` | Available opening hours |
| `services_raw` | Original service information collected from the source |
| `service_categories` | AI-enriched standardized service categories |
| `telehealth` | Telehealth availability based on explicit source evidence |
| `source_url` | Original source page for traceability |

### Example Service Categories

The AI enrichment process standardizes explicitly mentioned services into categories such as:

- General Practice
- Health Assessments
- Immunisations
- Chronic Disease Management
- Mental Health Care Plans
- Skin Checks
- Women's Health
- Men's Health
- Children's Health
- Travel Medicine
- Telehealth Consultations

> The enrichment process is evidence-based and does not intentionally introduce unsupported healthcare services.

---

## 🤖 AI & Prompt Engineering

A major component of this project is the use of **AI for controlled data enrichment**.

The initial approach produced overly generalized outputs because many medical practices contained similar service descriptions.

### Problem

A naive AI prompt could cause the model to:

- Assume services commonly offered by GP clinics
- Copy information from another clinic
- Infer telehealth availability
- Fill missing information using general knowledge
- Produce inconsistent outputs

### Solution

The prompt was refined to enforce strict source-based extraction.

The final approach instructs the AI to:

1. Process one clinic at a time.
2. Use only the information supplied for that clinic.
3. Never use outside knowledge or assumptions.
4. Generate service categories only from `services_raw`.
5. Mark unsupported information as `Unknown`.
6. Treat telehealth as available only when explicitly supported by the source.
7. Maintain evidence for generated classifications.
8. Perform a final quality check before producing the result.

This improved the reliability and traceability of the enrichment process.

---

## 🔄 Prompt Engineering Evolution

### Prompt V1

The first prompt focused on:

- Service categorization
- Telehealth
- Missing information
- Evidence-based extraction

### Issue Identified

The initial results showed that AI could generalize information across clinics when similar healthcare services appeared repeatedly.

### Prompt V2

The prompt was refined to explicitly state:

> Use ONLY the current clinic record.

Additional controls were introduced:

- No assumptions
- No external knowledge
- No copying between clinics
- Explicit evidence requirements
- `Unknown` when information is not supported
- Independent processing of every clinic

This refinement made the AI enrichment process more controlled and suitable for structured data processing.

Detailed prompt versions and the refinement process are available in:

**`AI_Healthcare_Data_Enrichment_Prompt_Documentation.docx`**

---

## 🧹 Data Quality & Validation

Data quality was treated as an important part of the pipeline rather than an afterthought.

The project included checks for:

- Missing practice names
- Missing phone numbers
- Missing addresses
- Missing opening hours
- Missing service information
- Duplicate practice records
- Duplicate URLs
- Incorrect address extraction
- Invalid or incomplete scraped records

Duplicate records were reviewed and removed to produce a cleaner final dataset.

The final dataset contains **86 unique clinic records**.

---

## ⚙️ Web Scraping Approach

The source website used for the project was the **Family Doctor Australia clinic directory**.

The scraping process used:

```text
Clinic Directory
      ↓
Clinic URLs
      ↓
Selenium
      ↓
Page Source
      ↓
BeautifulSoup
      ↓
JSON-LD / FAQ Information
      ↓
Structured Clinic Record
```

### Why Selenium?

Direct HTTP requests were not consistently reliable for the source website. The project therefore used Selenium to load webpages and extract the required information from dynamically served content.

### Extracted Information

The scraper collected:

- Practice name
- Phone number
- Full address
- Opening hours
- Services
- Source URL

---

## 🧠 Problem-Solving Highlights

### 1. HTTP Connection Issues

Direct requests to the website resulted in connection/reset issues.

**Solution:**  
Switched to Selenium-based browser extraction.

---

### 2. Inconsistent Page Structures

Different clinic pages did not always expose information in exactly the same HTML structure.

**Solution:**  
Used multiple extraction approaches, including structured JSON-LD and FAQ content.

---

### 3. Address Extraction Problems

Some addresses initially returned incorrect suburb/state information.

**Solution:**  
Implemented address cleaning and extraction logic using:

- State identification
- Postcode detection
- Comma-separated address components
- Removal of trailing country information

---

### 4. Duplicate Clinic Records

Some practices appeared through multiple URLs.

**Solution:**  
Compared practice names, addresses and URLs and removed duplicate records while retaining the most appropriate source URL.

---

### 5. AI Generalization

AI initially had a tendency to generalize common GP services.

**Solution:**  
Refined the prompt with strict evidence-based rules and independent clinic processing.

---

## 📁 Repository Structure

```text
AI-Healthcare-Data-Enrichment/
│
├── README.md
│
├── HealthCare_Project_Clean_Final.ipynb
│
├── AI_Healthcare_Data_Enrichment_Prompt_Documentation.docx
│
├── Healthcare_Practice_Enrichment_Final_Dataset.csv
│
└── data/
    └── Final healthcare dataset
```

---

## ▶️ How to Run the Project

### 1. Clone the repository

```bash
git clone https://github.com/Rutuja2082/AI-Healthcare-Data-Enrichment.git
```

### 2. Open the project

Open the notebook:

```text
HealthCare_Project_Clean_Final.ipynb
```

using Jupyter Notebook, JupyterLab, or VS Code.

### 3. Install required libraries

```bash
pip install pandas selenium beautifulsoup4
```

Additional browser/driver configuration may be required depending on the local Selenium setup.

### 4. Run the notebook

Execute the notebook cells sequentially to reproduce the data collection and processing workflow.

---

## 📄 Project Documentation

The repository includes detailed prompt engineering documentation covering:

- Project objective
- Dataset fields
- Prompt V1
- Problems identified
- Prompt V2
- Prompt refinement
- Data quality strategy
- AI enrichment approach
- Final workflow
- Key learnings

See:

**`AI_Healthcare_Data_Enrichment_Prompt_Documentation.docx`**

---

## 📈 Project Outcome

The project successfully demonstrates an end-to-end workflow for transforming semi-structured healthcare website information into a structured dataset.

### Final outcome

- **86 unique medical practice records**
- Structured clinic information
- Standardized healthcare service categories
- Evidence-based telehealth classification
- Duplicate and data-quality checks
- Source URL traceability
- Documented AI prompt engineering process

---

## 🎓 Key Learnings

Through this project, I gained practical experience in:

- Web scraping and data extraction
- Handling dynamic websites
- Data cleaning and validation
- Duplicate detection
- Structured data transformation
- AI-assisted data enrichment
- Prompt engineering
- Evidence-based AI extraction
- Data quality management
- Building reproducible data workflows
- Documenting an end-to-end data engineering project

---

## 👩‍💻 About Me

**Rutuja Ghodake**

Aspiring **Data Engineer** with hands-on experience in:

- SQL / T-SQL
- Python
- PySpark
- Databricks
- Azure
- ETL / ELT
- Data Cleaning & Data Quality
- Power BI
- AI-assisted data processing

I am interested in opportunities involving **Data Engineering, Data Quality, Data Analytics, SQL Development and AI/Data workflows**.

---

## ⭐ If You Find This Project Interesting

Feel free to explore the repository and review the notebook, dataset, and prompt engineering documentation.

**Thank you for visiting!**
