# OLA Ride Analysis - Data Analytics Project

<div align="center">






**A comprehensive data analytics project analyzing 100,000+ ride-hailing bookings to uncover operational insights and drive business decisions**

[View Documentation](#-documentation) -  [Explore Dashboard](#-dashboard-overview) -  [SQL Queries](#-sql-analysis) -  [DAX Measures](#-power-bi--dax)

</div>

***

## 📊 Project Overview

This project presents an **end-to-end data analytics solution** for Ola, one of India's leading ride-hailing platforms. Through advanced SQL querying and interactive Power BI dashboards, the analysis reveals critical insights into booking patterns, customer behavior, revenue trends, and operational efficiency.

### 🎯 Objectives

- Analyze booking success rates and identify cancellation patterns
- Evaluate vehicle type performance and revenue contribution
- Understand customer segmentation and loyalty patterns
- Identify peak demand periods and high-traffic locations
- Provide actionable recommendations for business growth

### 🔑 Key Highlights

- **100,000+ booking records** analyzed over one month
- **5 interactive Power BI dashboard pages** with 25+ visualizations
- **10 SQL views** answering critical business questions
- **15+ DAX measures** for advanced analytics
- **62% booking success rate** with detailed breakdown analysis

***

## 🛠️ Tech Stack

| Technology | Purpose |
|------------|---------|
| **MySQL** | Database management and SQL querying |
| **Power BI Desktop** | Interactive dashboard development |
| **DAX** | Advanced calculations and measures |
| **Excel** | Initial data processing |
| **Git & GitHub** | Version control and collaboration |

***

## 📁 Project Structure

```
OLA-Ride-Analysis/
│
├── 📄 README.md                          # Project overview (this file)
├── 📊 Dashboard/
│   └── OLA-Dashboard.pbix                # Power BI dashboard file
│
├── 📝 Documentation/
│   ├── OLA-SQL-Queries.docx              # Complete SQL query documentation
│   ├── OLA-DAX-Queries.docx              # All DAX measures and calculations
│   └── OLA-Project-Documentation.docx     # Comprehensive project report
│
├── 🗃️ Data/
│   └── ola_bookings.csv                  # Dataset (100K records)
│
├── 🖼️ Images/
│   ├── dashboard-overview.png
│   ├── revenue-analysis.png
│   └── customer-segmentation.png
│
└── 📜 SQL/
    └── ola_queries.sql                   # All SQL queries and views
```

***

## 📊 Dashboard Overview

The Power BI dashboard consists of **5 comprehensive pages**, each targeting specific business dimensions:

### 1️⃣ Overview Page
**KPIs Tracked:**
- ✅ Completed Bookings: **67,000**
- ❌ Lost Bookings: **33,000**
- 💰 Total Revenue: **₹31.17M**
- 🚗 Total Distance: **1.09M km**
- 📏 Average Distance: **16.20 km**

**Visualizations:**
- Booking status breakdown (pie chart)
- Daily booking trends (line chart)
- Revenue by vehicle type (bar chart)
- Top pickup/drop locations
- Average ratings (gauge charts)

### 2️⃣ Vehicle Analysis
- Customer count by vehicle type
- Revenue contribution percentage
- Completed bookings by vehicle
- Booking trends over time

**Key Insight:** Bike category leads in volume (28.27%), while Prime SUV generates highest revenue (₹7.9M)

### 3️⃣ Revenue Analysis
- Revenue by customer (top 7)
- Revenue by payment method
- Monthly and quarterly trends
- Vehicle-wise revenue breakdown

**Key Insight:** UPI dominates with ₹14M revenue, followed by Cash at ₹11.9M

### 4️⃣ Rider Analysis
- Customer segmentation (New, Occasional, Frequent, Loyal)
- Cancellation reasons breakdown
- Payment method distribution
- Detailed customer information table

**Key Insight:** Customer segmentation reveals loyalty patterns for targeted marketing

### 5️⃣ Location Analysis
- Monthly distance trends
- Busy time slots (8 time periods)
- Top 7 high-demand areas
- Weekday vs weekend patterns

**Key Insight:** Multiple peak periods identified for optimal driver deployment

***

## 🔍 SQL Analysis

### Database Setup
```sql
CREATE DATABASE Ola;
USE Ola;
```

### Key Business Questions Answered

| # | Question | View Created |
|---|----------|--------------|
| 1 | What are all successful bookings? | `Successful_Bookings` |
| 2 | Average ride distance per vehicle type? | `ride_distance_for_each_vehicle` |
| 3 | Total customer cancellations? | `cancelled_rides_by_customers` |
| 4 | Top 5 most frequent customers? | `Top_5_Customers` |
| 5 | Driver cancellations (personal/car issues)? | `Rides_cancelled_by_Drivers_P_C_Issues` |
| 6 | Max/Min driver ratings (Prime Sedan)? | `Max_Min_Driver_Rating` |
| 7 | All UPI payment rides? | `UPI_Payment` |
| 8 | Average customer rating per vehicle? | `AVG_Cust_Rating` |
| 9 | Total successful ride revenue? | `total_successful_ride_value` |
| 10 | Incomplete rides with reasons? | `Incomplete_Rides_Reason` |

### Sample Query
```sql
-- Retrieve all successful bookings
CREATE VIEW Successful_Bookings AS
SELECT * FROM bookings
WHERE Booking_Status = 'Success';
```

📄 **[View Complete SQL Documentation](Documentation/OLA-SQL-Queries.docx)**

***

## 📐 Power BI & DAX

### Key DAX Measures

**KPIs:**
```dax
Completed Bookings = 
CALCULATE(
    COUNT('bookings'[Booking ID]),
    'bookings'[Booking Status] = "Success"
)

Total Distance = SUM('bookings'[Ride Distance (km)])

Avg Distance = AVERAGE('bookings'[Ride Distance (km)])
```

**Customer Segmentation:**
```dax
Ride Frequency = 
VAR _rides = 
    CALCULATE(
        COUNT(bookings[Booking ID]),
        ALLEXCEPT(bookings, bookings[Customer ID])
    )
RETURN
    SWITCH(
        TRUE(),
        _rides = 1, "New Customer",
        _rides <= 3, "Occasional",
        _rides <= 6, "Frequent",
        "Loyal"
    )
```

**Time Slot Analysis:**
```dax
Time Slot = 
VAR _hour = HOUR('bookings'[Time])
RETURN
    SWITCH(
        TRUE(),
        _hour >= 9 && _hour < 12, "09 AM - 12 PM",
        _hour >= 12 && _hour < 15, "12 PM - 03 PM",
        -- Additional time slots...
        "Unknown"
    )
```

📄 **[View Complete DAX Documentation](Documentation/OLA-DAX-Queries.docx)**

***

## 📈 Key Findings

### 🎯 Operational Performance
- **67.31%** booking success rate (room for improvement)
- **19.59%** driver cancellations impact revenue
- **7.68%** customer cancellations need attention

### 🚗 Vehicle Insights
- **Bike** category: Highest volume (28.27% bookings)
- **Prime SUV**: Highest revenue (₹7.9M)
- Balanced distribution across other vehicle types

### 👥 Customer Behavior
- **UPI** is preferred payment method (₹14M revenue)
- Top customers generate **₹4-5K** individual revenue
- **4.40 average rating** indicates good service quality

### 📍 Location & Time Patterns
- **Kharadi & Ravet** lead in booking counts
- Multiple peak periods throughout the day
- Consistent distance distribution across vehicle types

***

## 💡 Business Recommendations

### 1. Reduce Cancellation Rates (27.27% combined)
- ✅ Implement driver incentives for ride acceptance
- ✅ Improve driver-customer matching algorithms
- ✅ Address top cancellation reasons

### 2. Optimize Vehicle Deployment
- ✅ Balance fleet composition for revenue maximization
- ✅ Deploy Prime SUVs during peak demand
- ✅ Offer promotions on underutilized vehicles

### 3. Enhance Digital Payments
- ✅ Incentivize credit/debit card usage
- ✅ Promote wallet adoption through loyalty programs
- ✅ Ensure seamless payment experience

### 4. Customer Retention Strategies
- ✅ Loyalty programs for frequent customers
- ✅ Re-engagement campaigns for occasional riders
- ✅ First-ride incentives for new customers

***

## 📚 Documentation

Comprehensive documentation is provided in three separate documents:

1. **[OLA-SQL-Queries.docx](Documentation/OLA-SQL-Queries.docx)** - All 10 SQL queries with explanations
2. **[OLA-DAX-Queries.docx](Documentation/OLA-DAX-Queries.docx)** - Complete DAX measures and calculations
3. **[OLA-Project-Documentation.docx](Documentation/OLA-Project-Documentation.docx)** - 6-7 page comprehensive project report

***

## 🚀 Getting Started

### Prerequisites
- MySQL Server (8.0 or higher)
- Power BI Desktop (latest version)
- Basic understanding of SQL and DAX

### Installation & Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/ola-ride-analysis.git
   cd ola-ride-analysis
   ```

2. **Import dataset into MySQL**
   ```sql
   CREATE DATABASE Ola;
   USE Ola;
   -- Import ola_bookings.csv into 'bookings' table
   ```

3. **Run SQL queries**
   ```bash
   mysql -u root -p Ola < SQL/ola_queries.sql
   ```

4. **Open Power BI Dashboard**
   - Open `Dashboard/OLA-Dashboard.pbix` in Power BI Desktop
   - Update data source connection to your MySQL server
   - Refresh data

***

## 📊 Dataset Information

| Attribute | Details |
|-----------|---------|
| **Total Records** | 100,000 bookings |
| **Time Period** | 1 month (July 2024) |
| **Location** | Bengaluru, India (50+ areas) |
| **Booking Success Rate** | ~62% |
| **Vehicle Types** | Auto, Bike, eBike, Mini, Prime Plus, Prime Sedan, Prime SUV |
| **Payment Methods** | UPI, Cash, Credit Card, Debit Card, Wallet |

### Data Columns (19 total)
- Date, Time, Booking_ID, Booking_Status
- Customer_ID, Vehicle_Type
- Pickup_Location, Drop_Location
- V_TAT, C_TAT
- Cancellation indicators and reasons
- Booking_Value, Payment_Method
- Ride_Distance, Driver_Ratings, Customer_Rating

***

## 🎓 Skills Demonstrated

- ✅ **SQL**: Complex queries, aggregations, views, joins
- ✅ **DAX**: Calculated measures, time intelligence, customer segmentation
- ✅ **Power BI**: Dashboard design, data modeling, visualizations
- ✅ **Business Analytics**: KPI tracking, trend analysis, insights generation
- ✅ **Data Storytelling**: Clear communication of findings
- ✅ **Problem Solving**: Actionable recommendations based on data

***

## 🤝 Contributing

Contributions are welcome! Feel free to:
- Report bugs or issues
- Suggest new features or analyses
- Improve documentation
- Submit pull requests

***

## 📧 Contact

**Your Name**  
💼 LinkedIn: [linkedin.com/in/arpitdalal9](https://linkedin.com/in/arpitdalal9)  
🐙 GitHub: [@arpitdalal7](https://github.com/arpitdalal7)

***

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

***

## 🙏 Acknowledgments

- Dataset created using ChatGPT for educational purposes
- Inspired by real-world ride-hailing industry analytics
- Tutorial reference: [The Developer YouTube Channel](https://www.youtube.com/@The-Developer-BI)

***

<div align="center">

**⭐ If you found this project helpful, please consider giving it a star!**



</div>
