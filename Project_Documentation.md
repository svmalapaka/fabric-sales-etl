# 🚀 Sales ETL Pipeline  
### Built with Microsoft Fabric • Dataflow Gen2 • Power Query • Lakehouse

A complete end‑to‑end ETL workflow demonstrating ingestion, transformation, Delta Lake storage, and reporting using Microsoft Fabric.

## Project Summary

This project demonstrates a complete end‑to‑end ETL workflow using Microsoft Fabric Dataflow Gen2 and Power Query.  
You ingest raw CSV sales data, apply structured transformations, generate aggregated insights, and store the final curated table in a Fabric Lakehouse using Delta format.  
The documentation walks through each step of the pipeline — from ingestion to reporting — providing a clear, reproducible template for modern data engineering projects in Fabric.


## Table of Contents
1. Introduction  
2. Project Overview  
3. Folder Structure  
4. Source Data Description  
5. Power Query Transformation Steps  
6. M-Code Reference  
7. Lakehouse File Structure  
8. Lakehouse Table Output  
9. Dataflow Gen2 Pipeline  
10. Power BI Integration  
11. Power BI Dashboard Preview  
12. Future Enhancements  
13. Lessons Learned  
14. Final Architecture Summary  
15. References & Resources  
16. Conclusion

### Overview
This project demonstrates how to ingest, transform, and load sales data using **Microsoft Fabric Dataflow Gen2** and **Power Query**. The pipeline loads a CSV file, applies data type transformations, aggregates sales by product, and stores the final table in a Fabric Lakehouse.

## 1. Data Source
- **File:** `sample_sales.csv`
- **Location:** Lakehouse → Files → `Portfolio_lakehouse_project1`
- **Ingestion Method:** Dataflow Gen2 → *Transform data (Power Query)*
### Lakehouse Source File
![Lakehouse Files - sample_sales.csv](images/lakehouse_files.png)
*Figure 1 – Lakehouse Files view showing sample_sales.csv used as the source.*


## 2. Initial Power Query Setup
### Power Query – Initial Setup
![Power Query Initial Transformations](images/powerquery_initial.png)
*Figure 2 – Power Query Editor showing Source and Navigation steps before applying Promoted Headers and Changed Column Types.*

Power Query automatically applied:
- Promoted Headers
- Changed Column Types

**M‑code:**
Table.TransformColumnTypes(#"Promoted headers", {
    {"Product", type text},
    {"Category", type text},
    {"Sales", Int64.Type},
    {"Date", type date}
})

## 3. Group By Transformation
### Power Query – Group By Step
![Group By Transformation](images/groupby_step.png)
*Figure 3 – Power Query Editor showing the Group By transformation and aggregated totals.*

To aggregate total sales per product:
- **Group By column:** Product
- **New column name:** TotalSales
- **Operation:** Sum
- **Column:** Sales

**M‑code:**
Table.Group(#"Changed column type", {"Product"}, {
    {"TotalSales", each List.Sum([Sales]), type nullable number}
})


## 4. Output Summary Table
### Output Summary Table (Screenshot)
![Output Summary](images/output_summary.png)
*Figure 4 – Final aggregated sales table stored in the Lakehouse, showing Product, Category, Sales, and Date.*

| Product  | TotalSales |
|----------|------------|
| Laptops  | 1220       |
| Mouse    | 25         |
| Keyboard | 45         |
| Monitor  | 300        |

## 5. Load to Lakehouse
The transformed and aggregated data is loaded into the Fabric Lakehouse as a managed table.

**Lakehouse Path:**

Portfolio_lakehouse_project1 / tables / dbo / SalesData_Grouped
### Lakehouse Managed Table (Screenshot)
![Lakehouse Managed Table](images/lakehouse_table_load.png)
*Figure 5 – Managed table SalesData_Grouped (example: publicholidays) created in the Lakehouse after Dataflow Gen2 load.*

This allows downstream analytics, reporting, and warehouse-style querying using SQL or notebooks.
## 6. Purpose

This project demonstrates:

- Building an ETL pipeline in Microsoft Fabric  
- Applying Power Query transformations  
- Aggregating data using Group By  
- Loading structured data into a Lakehouse table  

This project is useful for:

- Data engineering portfolios  
- Microsoft Fabric learning  
- Recruiter visibility  
- LinkedIn project showcase  

## 7. Next Steps

This project can be extended in several useful ways:

### 7.1 Add Power BI Reporting
Connect the Lakehouse table (`SalesData_Grouped`) to Power BI to build:
- Sales trend visuals  
- Product performance dashboards  
- Category-level comparisons  

### 7.2 Automate Data Refresh
Use Fabric Dataflow Gen2 scheduled refresh to automatically:
- Re‑ingest updated CSV files  
- Recompute aggregated totals  
- Keep Lakehouse tables current  

### 7.3 Add More Transformations
Enhance the pipeline with:
- Date normalization  
- Category standardization  
- Additional calculated columns  

### 7.4 Expand to Multiple Sources
Combine sales data with:
- Inventory files  
- Product metadata  
- External pricing feeds  

This turns the project into a more complete data engineering portfolio piece.

```markdown
## 8. Architecture Diagram

The following diagram illustrates the end‑to‑end flow of the Sales ETL pipeline using Microsoft Fabric Dataflow Gen2 and Lakehouse.

```mermaid
flowchart LR
    A[Lakehouse Files<br/>sample_sales.csv] --> B[Dataflow Gen2<br/>Power Query]
    B --> C[Transformations<br/>Promoted Headers<br/>Changed Types<br/>Group By]
    C --> D[Output Table<br/>SalesData_Grouped]
    D --> E[Lakehouse Tables<br/>dbo.SalesData_Grouped]
    E --> F[Downstream Analytics<br/>Power BI / SQL / Notebooks]

*Figure 8 – Architecture diagram showing the flow from Lakehouse file ingestion to Dataflow transformations and final managed table output.*


## 9. Folder Structure

The following structure shows how project files are organized for the Sales ETL Pipeline in Microsoft Fabric:

fabric-sales-etl/
│
├── images/
│   ├── lakehouse_files.png
│   ├── powerquery_initial.png
│   ├── groupby_step.png
│   ├── output_summary.png
│   └── lakehouse_table_load.png
│
├── sample_sales.csv
├── Project_Documentation.md
└── README.md

*Figure 9 – Folder layout showing images, source CSV, and documentation files used in the Fabric Lakehouse ETL project.*

## 10. GitHub Badges

Enhance your project’s visibility and professionalism on GitHub by adding badges that highlight tools, technologies, and project status.

### Recommended Badges

![Fabric](https://img.shields.io/badge/Microsoft%20Fabric-Dataflow%20Gen2-blue)
![Power Query](https://img.shields.io/badge/Power%20Query-ETL-green)
![Lakehouse](https://img.shields.io/badge/Fabric-Lakehouse-orange)
![Python](https://img.shields.io/badge/Notebook-SQL%20%7C%20Python-yellow)
![Status](https://img.shields.io/badge/Project-Complete-brightgreen)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

### How to Use
You can place these badges:
- At the top of your README  
- Under the project title  
- In the “Technologies Used” section  

Badges help recruiters and viewers quickly understand the stack and status of your project.

## 11. Power BI Dashboard Preview

After loading the transformed data into the Lakehouse table (`SalesData_Grouped`), you can build a Power BI report to visualize product‑level sales performance.

### Example Visuals
- **Bar Chart:** Total Sales by Product  
- **Line Chart:** Sales trends over time  
- **Category Breakdown:** Sales by category using a donut or treemap  
- **Table View:** Detailed sales records with filters  

### Connecting Power BI to the Lakehouse
1. Open **Power BI Desktop**.  
2. Select **Get Data → Microsoft Fabric (Lakehouse)**.  
3. Choose your workspace and Lakehouse.  
4. Load the `SalesData_Grouped` table.  
5. Build visuals using the fields:
   - `Product`
   - `TotalSales`
   - `Category`
   - `Date`

### Benefits
- Interactive exploration of sales trends  
- Easy sharing with stakeholders  
- Supports scheduled refresh when paired with Dataflow Gen2  
- Ideal for portfolio demonstrations and LinkedIn posts  

## 12. Future Enhancements

This Sales ETL Pipeline can be expanded into a more advanced data engineering solution by adding additional features and automation layers.

### 12.1 Incremental Data Loads
Implement incremental refresh logic so only new or updated rows are processed.  
This reduces compute cost and improves refresh performance.

### 12.2 Data Quality Checks
Add validation steps such as:
- Null value detection  
- Duplicate product checks  
- Out-of-range sales amounts  
- Date format consistency  

These checks can be implemented using Power Query or Fabric Data Pipelines.

### 12.3 Error Logging & Monitoring
Enhance reliability by adding:
- Error logs stored in a Lakehouse table  
- Refresh failure notifications  
- Monitoring dashboards using Power BI  

### 12.4 Integration with Warehouse
Load curated data into a Fabric Warehouse for:
- SQL analytics  
- Semantic models  
- Direct Lake mode reporting  

### 12.5 Multi‑File Ingestion
Extend the pipeline to ingest:
- Monthly sales files  
- Multiple product categories  
- External pricing feeds  

This turns the project into a scalable ingestion framework.

### 12.6 Add Machine Learning
Use Fabric notebooks to build:
- Sales forecasting models  
- Product performance predictions  
- Category trend analysis  

This adds an AI layer to your ETL pipeline.

*Figure 12 – Future enhancements that expand the Sales ETL Pipeline into a scalable, production‑ready data engineering solution.*

## 13. Lessons Learned

Building this Sales ETL Pipeline in Microsoft Fabric provided several practical insights into modern data engineering workflows.

### 13.1 Importance of Clean Source Data
Even small inconsistencies in CSV files (missing values, incorrect types, extra spaces) can break transformations.  
Implementing early validation steps prevents downstream failures.

### 13.2 Power Query Is More Capable Than Expected
Power Query’s M‑language supports:
- Complex grouping  
- Conditional logic  
- Column transformations  
- Multi‑file ingestion  
This makes it a strong candidate for lightweight ETL inside Fabric.

### 13.3 Lakehouse Tables Are Ideal for Analytics
Using Delta tables in the Lakehouse provides:
- ACID transactions  
- Fast reads for Power BI  
- Easy integration with notebooks and pipelines  

This simplifies the architecture compared to traditional data lakes.

### 13.4 Visual Documentation Helps Understanding
Mermaid diagrams and folder structure visuals make the project easier to explain to recruiters, teammates, and future contributors.

### 13.5 Automation Saves Time
Scheduled refreshes and Dataflow Gen2 pipelines reduce manual work and ensure data stays up‑to‑date without intervention.

### 13.6 Iteration Is Key
The pipeline improved through multiple iterations:
- First version: basic load  
- Second version: grouping logic  
- Third version: Lakehouse integration  
- Fourth version: Power BI preview  

Each iteration added clarity and reliability.

*Figure 13 – Summary of key lessons learned while building the Sales ETL Pipeline in Microsoft Fabric.*

## 14. Final Architecture Summary

This project demonstrates a complete, end‑to‑end ETL workflow built using Microsoft Fabric’s unified analytics platform. The architecture integrates ingestion, transformation, storage, and reporting into a single streamlined pipeline.

### 14.1 Data Ingestion
- Source files (CSV) are uploaded into the Lakehouse Files area.
- Fabric automatically organizes the data into a structured folder hierarchy.
- Power Query or Dataflow Gen2 can be used for scheduled ingestion.

### 14.2 Data Transformation
- Power Query performs:
  - Column cleanup  
  - Grouping and aggregation  
  - Type conversions  
  - Data quality checks  
- The transformed output is written into a Lakehouse Delta table (`SalesData_Grouped`).

### 14.3 Storage Layer (Lakehouse)
- Delta format ensures ACID transactions.
- Tables support fast reads for analytics.
- Data is accessible to notebooks, pipelines, and Power BI.

### 14.4 Analytics & Reporting
- Power BI connects directly to the Lakehouse.
- Visuals include:
  - Sales by product  
  - Category breakdown  
  - Time‑series trends  
- Reports can be shared, refreshed, and embedded.

### 14.5 Scalability & Extensibility
- Supports incremental refresh.
- Can integrate with Warehouse for SQL analytics.
- Can add ML models using Fabric notebooks.
- Can expand to multi‑file ingestion and enterprise‑grade pipelines.

*Figure 14 – High‑level architecture summarizing ingestion, transformation, storage, and reporting in the Sales ETL Pipeline.*

## 15. References & Resources

This project was built using Microsoft Fabric, Power Query, Lakehouse tables, and Power BI.  
The following resources were helpful during development and can support future enhancements.

### 15.1 Microsoft Fabric Documentation
- Microsoft Fabric Overview  
  https://learn.microsoft.com/fabric/

- Lakehouse Architecture  
  https://learn.microsoft.com/fabric/data-engineering/lakehouse-overview

- Dataflow Gen2  
  https://learn.microsoft.com/fabric/data-factory/dataflows-gen2-overview

### 15.2 Power Query & M Language
- Power Query M Reference  
  https://learn.microsoft.com/powerquery-m/

- Power Query Tutorials  
  https://learn.microsoft.com/power-bi/guided-learning/power-query/

### 15.3 Delta Lake & Storage
- Delta Lake in Fabric  
  https://learn.microsoft.com/fabric/data-engineering/delta-lake-overview

### 15.4 Power BI Reporting
- Power BI Desktop  
  https://learn.microsoft.com/power-bi/fundamentals/desktop-getting-started

- Direct Lake Mode  
  https://learn.microsoft.com/fabric/data-engineering/direct-lake-overview

### 15.5 Additional Learning Resources
- Microsoft Learn Data Engineering Path  
  https://learn.microsoft.com/training/paths/data-engineer-fabric/

- Fabric Community Blog  
  https://community.fabric.microsoft.com/

*Figure 15 – Reference links and learning resources supporting the development of the Sales ETL Pipeline.*

## 16. Conclusion

This project demonstrates how Microsoft Fabric unifies data ingestion, transformation, storage, and analytics into a single, streamlined workflow. By building a complete ETL pipeline—from raw CSV files to a curated Lakehouse table and Power BI dashboard—you gain hands‑on experience with modern data engineering patterns used in real‑world solutions.

The pipeline highlights several strengths of Fabric:
- A simplified Lakehouse architecture using Delta tables  
- Powerful transformation capabilities through Power Query  
- Seamless integration with Power BI for reporting  
- Scalable design that can grow into enterprise‑grade pipelines  

Through this project, you developed practical skills in Fabric’s data engineering ecosystem and created a reusable template for future analytics or machine learning workloads. The modular design ensures that new datasets, transformations, or reporting layers can be added with minimal effort.

This ETL pipeline serves as a strong portfolio piece and a foundation for more advanced projects, including incremental refresh, multi‑file ingestion, ML‑based forecasting, and Warehouse‑based SQL analytics.

*Figure 16 – Final summary of the completed Sales ETL Pipeline and its role within Microsoft Fabric.*

## Author
**Sastry Malapaka**  
Old Bridge, New Jersey  
Microsoft Fabric Learner • Data Engineering Enthusiast

---

### 🧩 Sales ETL Pipeline • Microsoft Fabric  
Built with Dataflow Gen2 • Power Query • Lakehouse  
**© 2026 Sastry Malapaka — Old Bridge, New Jersey**

---



