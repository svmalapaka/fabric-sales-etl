# 🚀 Sales ETL Pipeline Using Microsoft Fabric

<p align="left">

  <!-- Core Fabric Badges -->
  <img src="https://img.shields.io/badge/Microsoft%20Fabric-0078D4?style=flat-square&logo=microsoft&logoColor=white" />
  <img src="https://img.shields.io/badge/Dataflow%20Gen2-FF6F00?style=flat-square&logo=powerbi&logoColor=white" />
  <img src="https://img.shields.io/badge/Power%20Query-217346?style=flat-square&logo=microsoft-excel&logoColor=white" />
  <img src="https://img.shields.io/badge/Lakehouse-FFB900?style=flat-square&logo=databricks&logoColor=white" />
  <img src="https://img.shields.io/badge/Delta%20Tables-FF6F00?style=flat-square&logo=apache-spark&logoColor=white" />

  <!-- Tools & Output -->
  <img src="https://img.shields.io/badge/Power%20BI-F2C811?style=flat-square&logo=powerbi&logoColor=black" />
  <img src="https://img.shields.io/badge/ETL%20Pipeline-4CAF50?style=flat-square" />

  <!-- Status -->
  <img src="https://img.shields.io/badge/Status-Complete-brightgreen?style=flat-square" />

</p>

<p align="left">

  <!-- GitHub Repo Stats -->
  <img src="https://img.shields.io/github/stars/SastryXYZ/fabric-sales-etl?style=flat-square" />
  <img src="https://img.shields.io/github/forks/SastryXYZ/fabric-sales-etl?style=flat-square" />
  <img src="https://img.shields.io/github/license/SastryXYZ/fabric-sales-etl?style=flat-square" />

</p>

<!-- Banner -->
<p align="center">
  <img src="banner.png" width="100%" alt="Fabric ETL Banner">
</p>

## Overview
This project demonstrates how to ingest, transform, and load sales data using Microsoft Fabric Dataflow Gen2 and Power Query. The pipeline loads a CSV file, applies data type transformations, aggregates sales by product, and stores the final table in a Fabric Lakehouse.

## Diagrams

### Architecture
![Architecture](architecture.svg)

### Pipeline
![Pipeline](pipeline.svg)

### Report Preview
![Report](report.svg)

## Technologies Used
- Microsoft Fabric
- Dataflow Gen2
- Power Query
- Lakehouse (Delta Tables)
- Power Query M-code

## Transformation Steps

### 1. Load CSV into Power Query
Source file: `sample_sales.csv`  
Location: Lakehouse → Files

### 2. Promote Headers & Set Column Types
```m
Table.TransformColumnTypes(#"Promoted headers", {
    {"Product", type text},
    {"Category", type text},
    {"Sales", Int64.Type},
    {"Date", type date}
})


Table.Group(#"Changed column type", {"Product"}, {
    {"TotalSales", each List.Sum([Sales]), type nullable number}
})

### 4\. Resulting Summary Table

| Product | TotalSales |
| --- | --- |
| Laptops | 1220 |
| Mouse | 25  |
| Keyboard | 45  |
| Monitor | 300 |

## Author
**Sastry Malapaka**  
Old Bridge, New Jersey  
Microsoft Fabric Learner • Data Engineering Enthusiast
