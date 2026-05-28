# 📊 IT Operations Dashboard — Power BI Project

## 🌟 The Story Behind the Project

Every digital platform generates operational data — tickets, incidents, response times, and service requests. But raw data alone does not improve operations. The real value lies in turning that data into clear, actionable insights that help teams make faster and better decisions.

This project started with a real-world IT support ticket dataset containing 8,000+ records. The challenge was not just to visualize numbers, but to build a diagnostic tool that mirrors what operations and monitoring teams actually need — a live view of service performance, incident distribution, workload patterns, and customer satisfaction trends.

## 🚀 What I Built

A 3-page interactive IT Operations Dashboard in Power BI that provides end-to-end visibility into service desk performance. This is not a generic chart collection — it is a structured reporting tool designed to support data-driven decisions for Operations, Monitoring, and Service Management teams.

**Dashboard pages:**
- **Page 1 — Executive Overview:** High-level KPIs, ticket volume trends, status breakdown, and priority distribution
- **Page 2 — Incident Analysis:** Deep dive into ticket types, monthly trends, and a priority-type matrix
- **Page 3 — Service Performance:** Channel performance, resolution rates by ticket type, and satisfaction analysis

## 🛠️ Technical Deep Dive

### Power Query — Data Cleaning & Transformation

All data preparation was done directly inside Power BI using Power Query M, keeping the pipeline transparent and reproducible:

- Removed PII columns (Customer Name, Email, Age, Gender) irrelevant to operational analysis
- Removed free-text columns (Ticket Description, Resolution) not suitable for BI aggregation
- Renamed `Date of Purchase` to `Ticket Date` for semantic clarity
- Changed data types to ensure correct aggregation (dates, decimals)
- Built a calculated `Resolution Hours` column from timestamp differences
- Applied conditional logic to handle null and negative resolution values
- Created a dedicated **Date Table** using `CALENDAR()` with Month, Month Number, Quarter, and Year columns for time intelligence

### Data Modeling

- Established a **star schema** with the Date Table connected to the fact table via `Ticket Date`
- Created a dedicated **Measures Table** to keep all DAX logic organized and separated from raw data

### DAX Measures

All KPIs were built as explicit DAX measures for reusability and filter context awareness:

```DAX
Total Tickets = COUNTROWS('customer_support_tickets')

Resolved Tickets = 
CALCULATE(
    COUNTROWS('customer_support_tickets'),
    'customer_support_tickets'[Ticket Status] = "Closed"
)

Resolution Rate % = 
DIVIDE([Resolved Tickets], [Total Tickets], 0) * 100

Critical Tickets = 
CALCULATE(
    COUNTROWS('customer_support_tickets'),
    'customer_support_tickets'[Ticket Priority] = "Critical"
)

Open Tickets = 
CALCULATE(
    COUNTROWS('customer_support_tickets'),
    'customer_support_tickets'[Ticket Status] = "Open"
)

Avg Satisfaction Score = 
AVERAGE('customer_support_tickets'[Customer Satisfaction Rating])
```

### Dashboard Design & UI/UX

- Clean card-based layout with consistent borders and rounded corners
- Color-coded priority bars (Critical = Red, High = Orange, Medium = Blue, Low = Green) for instant visual scanning
- Interactive slicers for Ticket Priority and Ticket Type with cross-page filtering
- Donut chart for ticket status breakdown with percentage labels
- Line chart for monthly ticket volume trends using the Date Table
- Matrix visual for ticket type vs priority cross-analysis

## 📈 Key Insights & Results

- **Volume:** 8,000+ support tickets analyzed across all channels and priority levels
- **Resolution Rate:** Only 32.7% of tickets are closed, indicating a significant backlog requiring operational attention
- **Priority Distribution:** Critical tickets (2,129) represent over 26% of total volume — a key risk area for SLA compliance
- **Channel Performance:** Email, Phone, Social Media, and Chat each handle approximately equal volume (~2.1K tickets), suggesting no single channel bottleneck
- **Satisfaction Score:** Average customer satisfaction of 2.99 out of 5 highlights room for service quality improvement
- **Open Tickets:** 3,000 open tickets represent unresolved demand that operations teams should prioritize

## 🎯 Business Value

This dashboard directly supports the needs of Operations and Monitoring teams by:
- Providing real-time visibility into incident volume and status
- Identifying high-priority ticket clusters that require immediate attention
- Tracking service quality through satisfaction scores across channels
- Enabling data-driven decisions through interactive filtering and drill-down

## 🧰 Tools & Technologies

| Tool | Purpose |
|------|---------|
| Power BI Desktop | Dashboard development |
| Power Query (M) | Data cleaning and transformation |
| DAX | KPI measures and calculated columns |
| Star Schema Modeling | Data model design |

## 📁 Dataset

**Source:** [IT Support Ticket Dataset — Kaggle](https://www.kaggle.com/datasets/suraj520/customer-support-ticket-dataset)

**Size:** 8,000+ records · 17 columns (9 used after cleaning)

**Key columns used:** Ticket Status, Ticket Priority, Ticket Type, Ticket Channel, Customer Satisfaction Rating, First Response Time, Time to Resolution, Ticket Date

---

[![GitHub](https://img.shields.io/badge/GitHub-zahraahmadi12-181717?logo=github)](https://github.com/zahraahmadi12)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Zahra%20Ahmadi-0A66C2?logo=linkedin)](https://linkedin.com/in/zahra-ahmadi-0579aa328)
