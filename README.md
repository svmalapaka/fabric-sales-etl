# Sales ETL Pipeline Using Microsoft Fabric

![Microsoft Fabric](https://img.shields.io/badge/Microsoft-Fabric-blue?style=flat-square)
![Power Query](https://img.shields.io/badge/Power%20Query-M--Code-green?style=flat-square)
![Dataflow Gen2](https://img.shields.io/badge/Dataflow-Gen2-orange?style=flat-square)
![Lakehouse](https://img.shields.io/badge/Lakehouse-Delta%20Tables-yellow?style=flat-square)
![Status](https://img.shields.io/badge/Project-Complete-brightgreen?style=flat-square)

## Overview
This project demonstrates how to ingest, transform, and load sales data using Microsoft Fabric Dataflow Gen2 and Power Query. The pipeline loads a CSV file, applies data type transformations, aggregates sales by product, and stores the final table in a Fabric Lakehouse.

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
