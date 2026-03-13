```markdown
# AI Supply Chain Analytics

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Arpit%20Dalal-blue?style=flat&logo=linkedin)](https://www.linkedin.com/in/arpitdalal9/)
[![GitHub](https://img.shields.io/badge/GitHub-Repository-black?style=flat&logo=github)](https://github.com/arpitdalal7/ai-supplychain-analytics)
[![Python](https://img.shields.io/badge/Python-3.8+-blue?style=flat&logo=python)](https://www.python.org/)

An end-to-end **AI-powered supply chain analytics system** that automates data collection, performs intelligent analysis, and generates actionable insights to optimize supply chain operations, improve delivery performance, and reduce operational costs.

---

## 📋 Overview

This project demonstrates a modern approach to supply chain management by leveraging AI and automation tools to solve real-world operational challenges. The system automatically:

- **Collects** order data from email attachments  
- **Stores** data in a cloud PostgreSQL database  
- **Cleans** and transforms data using AI-generated Python code  
- **Analyzes** supply chain performance through 15+ KPIs  
- **Generates** business insights and recommendations  

### Business Problem

Supply chain operations often face challenges like:

- Late deliveries impacting customer satisfaction  
- Incomplete order fulfillment causing revenue loss  
- Lack of real-time visibility into performance metrics  
- Manual data processing leading to delays and errors  

### Solution

This automated analytics pipeline provides:

- **Real-time monitoring** of supply chain KPIs (OTIF, Fill Rates, Cycle Time)  
- **Predictive insights** for demand planning and inventory optimization  
- **Automated reporting** reducing manual effort by 10-15x  
- **Data-driven recommendations** for operational improvements  

---

## ✨ Features

### Core Capabilities

- **🤖 Workflow Automation**
  - Automated email monitoring and CSV extraction using n8n  
  - Zero-touch data ingestion from vendors to database  
  - Scheduled data pipeline execution  

- **📊 Supply Chain KPIs**
  - On-Time Delivery % (OT%)  
  - In-Full Delivery % (IF%)  
  - On-Time-In-Full % (OTIF%) – primary success metric  
  - Line Fill Rate & Volume Fill Rate  
  - Order Cycle Time & Delivery Delay Analysis  
  - Backorder Tracking & Lead Time Variability  

- **🧹 AI-Powered Data Processing**
  - Natural language prompts generate Python cleaning code  
  - Automatic data type conversion and validation  
  - Multi-table merging and feature engineering  
  - Currency conversion (USD ↔ INR) for cross-country operations  

- **📈 Business Intelligence**
  - Customer performance analysis (OTIF gaps, revenue loss)  
  - Product category fulfillment trends  
  - Metro vs Non-Metro service level comparison  
  - Demand variability and supply chain bottleneck identification  

- **🎯 Interactive Dashboards**
  - Real-time KPI monitoring  
  - Custom visualizations using AI-generated charts  
  - Drill-down capabilities for root cause analysis  

---

## 🛠️ Tech Stack

### Automation & Workflow
- **n8n** – No-code workflow automation platform  
- **Gmail API** – Email monitoring and attachment extraction  

### Database & Backend
- **PostgreSQL** – Relational database for structured data storage  
- **Supabase** – Managed PostgreSQL hosting with real-time APIs  
- **SQL** – Data querying and transformation  

### Analytics & AI
- **Quadratic** – AI-powered spreadsheet with Python/SQL support  
- **Python** – Data processing and analysis  
  - `pandas` – Data manipulation  
  - `numpy` – Numerical computing  
  - `matplotlib` / `plotly` – Visualization  
  - `requests` – API integration for exchange rates  

### Data Modeling
- **Star Schema** – Dimensional modeling (Fact & Dimension tables)  
- **ETL Pipeline** – Extract, Transform, Load architecture  

---

## 📦 Installation

### Prerequisites

- Python 3.8 or higher  
- PostgreSQL database (or Supabase account)  
- n8n instance (cloud or self-hosted)  
- Quadratic account (free tier available)  

### Step 1: Clone the Repository

```bash
git clone https://github.com/arpitdalal7/ai-supplychain-analytics.git
cd ai-supplychain-analytics
```

### Step 2: Set Up Python Environment

```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### Step 3: Configure Database

1. **Create Supabase Project**
   - Sign up at [supabase.com](https://supabase.com)  
   - Create new project and note connection string  

2. **Run Database Schema**
   ```bash
   psql -h <your-supabase-host> -U postgres -d postgres -f database/schema.sql
   ```

3. **Update Configuration**
   - Copy `.env.example` to `.env`  
   - Add your database credentials:

     ```env
     DB_HOST=your-supabase-host
     DB_PORT=5432
     DB_NAME=postgres
     DB_USER=postgres
     DB_PASSWORD=your-password
     ```

### Step 4: Set Up n8n Workflow

1. **Install n8n** (choose one method):

   ```bash
   # Option 1: npm
   npm install n8n -g

   # Option 2: Docker
   docker run -it --rm --name n8n -p 5678:5678 n8nio/n8n
   ```

2. **Import Workflow**
   - Open n8n at `http://localhost:5678`  
   - Go to Workflows → Import from File  
   - Select `workflows/email_to_database.json`  

3. **Configure Credentials**
   - Add Gmail credentials for email monitoring  
   - Add PostgreSQL credentials pointing to Supabase  

### Step 5: Set Up Quadratic

1. Create account at [quadratichq.com](https://quadratichq.com)  
2. Connect to your Supabase database  
3. Import `quadratic/supply_chain_analysis.grid` workbook  

---

## 🚀 Usage

### Running the Data Pipeline

#### 1. Start n8n Workflow

```bash
# Start n8n
n8n start

# The workflow will automatically:
# - Monitor Gmail inbox for vendor emails
# - Extract CSV attachments
# - Load data into PostgreSQL tables
```

#### 2. Load Sample Data (Optional)

```bash
# Load sample order data
python scripts/load_sample_data.py

# This will populate:
# - fact_orders_aggregate
# - fact_order_line
# - dim_customers
# - dim_products
```

#### 3. Run Data Cleaning & Analysis

Open Quadratic and execute AI prompts:

**Create Date Table:**

```text
Create a date table that has dates from 03-01-2025 to 05-31-2025
```

**Create Exchange Rate Table:**

```text
Create exchange_rate table for March 1 to May 17, 2025 
using Open Exchange Rates API
```

**Generate fact_summary Table:**

```text
Create Python code that:
1. Loads data from fact_order_line, dim_products, dim_customers, exchange_rate
2. Cleans data (convert IDs to integers, remove nulls, standardize dates)
3. Merges tables on product_id, customer_id, order_placement_date
4. Calculates total_amount_inr (handles USD/INR conversion)
5. Creates calculated columns: backorder_qty, order_cycle_time_days, 
   delivery_delay_days, in_full_percent, on_time_flag
```

#### 4. Calculate Supply Chain KPIs

```text
Create the following KPIs:
1. Total Order Lines
2. Line Fill Rate
3. Volume Fill Rate
4. Total Orders
5. On Time Delivery %
6. In Full Delivery %
7. On Time In Full %
8. Order Cycle Time
9. Backorder Rate
10. Lead Time Variability
```

#### 5. Generate Business Insights

```text
Show top 5 customers based on order value and their OTIF%, IF%, OT%.
Include customer_name, customer_id, and city
```

```text
Filter the most recent 4 weeks. Aggregate by category: 
total backorder_qty, average in_full_percent, and average delivery_delay_days.
Return the five categories with highest backorder_qty
```

---

## 📊 Project Structure

```text
ai-supplychain-analytics/
│
├── data/
│   ├── sample_order_aggregate.csv
│   └── sample_order_line.csv
│
├── database/
│   ├── schema.sql
│   └── seed_data.sql
│
├── workflows/
│   └── email_to_database.json
│
├── quadratic/
│   └── supply_chain_analysis.grid
│
├── scripts/
│   ├── load_sample_data.py
│   └── validate_kpis.py
│
├── docs/
│   ├── PROJECT_DOCUMENTATION.pdf
│   └── screenshots/
│       ├── n8n_workflow.png
│       ├── data_cleaning_prompt.png
│       └── kpi_dashboard.png
│
├── requirements.txt
├── .env.example
├── .gitignore
└── README.md
```

### 🔗 Direct Folder Links

- **Data:** [`/data`](https://github.com/arpitdalal7/ai-supplychain-analytics/tree/main/data)  
- **Database:** [`/database`](https://github.com/arpitdalal7/ai-supplychain-analytics/tree/main/database)  
- **Workflows:** [`/workflows`](https://github.com/arpitdalal7/ai-supplychain-analytics/tree/main/workflows)  
- **Quadratic:** [`/quadratic`](https://github.com/arpitdalal7/ai-supplychain-analytics/tree/main/quadratic)  
- **Scripts:** [`/scripts`](https://github.com/arpitdalal7/ai-supplychain-analytics/tree/main/scripts)  
- **Docs:** [`/docs`](https://github.com/arpitdalal7/ai-supplychain-analytics/tree/main/docs)  

---

## 📈 Key Performance Indicators (KPIs)

### Delivery Performance

| KPI | Formula | Industry Benchmark |
|-----|---------|-------------------|
| **On-Time Delivery %** | (On-time orders / Total orders) × 100 | 90%+ |
| **In-Full Delivery %** | (Complete orders / Total orders) × 100 | 95%+ |
| **OTIF %** | (On-time AND In-full / Total orders) × 100 | 85%+ |

### Operational Efficiency

| KPI | Description | Target |
|-----|-------------|--------|
| **Line Fill Rate** | % of order lines delivered completely | 95%+ |
| **Volume Fill Rate** | % of ordered quantity delivered | 98%+ |
| **Order Cycle Time** | Avg days from order to delivery | < 5 days |

### Risk & Variability

| KPI | Measurement | Interpretation |
|-----|------------|----------------|
| **Lead Time Variability** | Std dev of cycle times | Lower = more reliable |
| **Demand Variability** | Weekly quantity fluctuation | Informs safety stock |
| **Backorder Rate** | % of lines with backorders | < 5% acceptable |

---

## 🎓 Learning Outcomes

This project demonstrates proficiency in:

- **Workflow Automation** – Building no-code data pipelines with n8n  
- **Database Design** – Implementing star schema for analytics  
- **ETL Development** – Extracting, transforming, loading supply chain data  
- **AI Integration** – Leveraging AI for code generation and analysis  
- **Business Analytics** – Calculating and interpreting supply chain KPIs  
- **Data Visualization** – Creating actionable dashboards  
- **Problem Solving** – Translating business problems into technical solutions  

---

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

### Reporting Issues

- Use GitHub Issues to report bugs or suggest features  
- Provide detailed description, steps to reproduce, and expected behavior  

### Making Contributions

1. **Fork the repository**

   ```bash
   # Click "Fork" button on GitHub
   ```

2. **Create a feature branch**

   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **Make your changes**
   - Follow existing code style  
   - Add comments for complex logic  
   - Update documentation if needed  

4. **Commit your changes**

   ```bash
   git add .
   git commit -m "Add: Brief description of changes"
   ```

5. **Push to your fork**

   ```bash
   git push origin feature/your-feature-name
   ```

6. **Create Pull Request**
   - Go to original repository on GitHub  
   - Click "New Pull Request"  
   - Select your fork and branch  
   - Describe your changes clearly  

### Development Guidelines

- Write clear, self-documenting code  
- Include docstrings for Python functions  
- Test your changes before submitting  
- Update README if adding new features  
- Ensure backward compatibility  

---

## 📝 License

This project is licensed under the **MIT License** – see the [LICENSE](LICENSE) file for details.

```text
MIT License

Copyright (c) 2026 Arpit Dalal

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## 👨‍💻 Developed by

**Arpit Dalal**

- 💼 **LinkedIn:** [linkedin.com/in/arpitdalal9](https://www.linkedin.com/in/arpitdalal9/)  
- 🐙 **GitHub:** [github.com/arpitdalal7](https://github.com/arpitdalal7)  
- 📂 **Project Repository:** [ai-supplychain-analytics](https://github.com/arpitdalal7/ai-supplychain-analytics)  

---

<div align="center">

**Built with 🧠 AI • ⚡ Automation • 📊 Data**  

*Transforming supply chain operations through intelligent analytics*

</div>
```
