# Uber Ride Analytics – Power BI Dashboard

## 1. Project Overview

This project is an **Uber Ride Analytics Dashboard built in Microsoft Power BI**. The objective is to transform raw Uber booking data into an interactive business intelligence solution that helps understand:

- Overall booking performance
- Completed, cancelled, incomplete, and unsuccessful bookings
- Revenue and booking value
- Vehicle-type performance
- Ride distance and operational performance
- Customer and driver cancellations
- Customer and driver ratings
- Payment-method usage
- Trends over time
- Operational problems affecting the ride experience

The project follows a complete Power BI workflow:

**Raw CSV Data → Power Query Cleaning → Data Modeling → DAX Measures → Interactive Dashboard → Business Insights**

---

## 2. Project Objectives

The main objectives of the dashboard are:

1. Prepare the raw Uber dataset for reliable analysis.
2. Clean and transform the data using **Power Query Editor**.
3. Build calculations and KPIs using **DAX measures**.
4. Analyze booking status and operational performance.
5. Compare vehicle types using revenue, distance, and performance metrics.
6. Analyze customer and driver cancellation behavior.
7. Evaluate customer and driver satisfaction through ratings.
8. Create an interactive dashboard where users can filter the analysis by date.
9. Convert a large transactional dataset into an easy-to-understand business report.

---

# 3. Dataset Description

The source dataset is an Uber booking dataset containing **150,000 booking records** and **21 columns**.

### Dataset size

- **Rows:** 150,000
- **Columns:** 21
- **Analysis period:** January 1, 2024 to December 30, 2024
- **Unique dates represented:** 365

### Main categories

The dataset contains information about:

- Booking details
- Customers
- Vehicle types
- Pickup and drop locations
- Booking status
- Cancellation information
- Booking value
- Ride distance
- Driver ratings
- Customer ratings
- Payment methods

---

# 4. Important Dataset Columns

| Column | Description |
|---|---|
| Date | Date on which the booking was made |
| Time | Time of the booking |
| Booking ID | Unique identifier for a booking |
| Booking Status | Status of the booking |
| Customer ID | Identifier for the customer |
| Vehicle Type | Type of Uber vehicle used/booked |
| Pickup Location | Ride pickup location |
| Drop Location | Ride destination |
| Avg VTAT | Average Vehicle Time of Arrival |
| Avg CTAT | Average Customer/Trip-related arrival time metric in the source data |
| Cancelled Rides by Customer | Indicates/counts customer cancellation records |
| Reason for cancelling by Customer | Reason provided for customer cancellation |
| Cancelled Rides by Driver | Indicates/counts driver cancellation records |
| Driver Cancellation Reason | Reason provided for driver cancellation |
| Incomplete Rides | Indicates/counts incomplete ride records |
| Incomplete Rides Reason | Reason for incomplete ride |
| Booking Value | Monetary value associated with a booking |
| Ride Distance | Distance travelled for the ride |
| Driver Ratings | Rating given to the driver |
| Customer Rating | Rating associated with the customer/ride |
| Payment Method | Payment method used for the booking |

---

# 5. Initial Dataset Understanding

The raw dataset contains five major booking-status categories:

| Booking Status | Records |
|---|---:|
| Completed | 93,000 |
| Cancelled by Driver | 27,000 |
| No Driver Found | 10,500 |
| Cancelled by Customer | 10,500 |
| Incomplete | 9,000 |
| **Total** | **150,000** |

This immediately shows that **Completed** bookings form the largest group, while driver cancellations are also a significant operational category.

The vehicle types represented in the dataset are:

- Auto
- Go Mini
- Go Sedan
- Bike
- Premier Sedan
- eBike
- Uber XL

The dataset also contains multiple payment methods, including:

- UPI
- Cash
- Uber Wallet
- Credit Card
- Debit Card

---

# 6. Step 1 – Importing the Dataset

The original data was available as a CSV file.

The first stage of the Power BI project was to import the CSV into Power BI.

### Process

1. Open Power BI Desktop.
2. Select **Get Data**.
3. Choose **Text/CSV**.
4. Select the Uber dataset.
5. Open the data in **Power Query Editor** instead of immediately loading it into the report.
6. Review the columns, data types, missing values, and categorical values.

### Why Power Query was used

Power Query acts as the data-preparation layer between the raw source and the Power BI data model.

Instead of manually changing the original CSV, transformations are performed in Power Query. This makes the preparation process:

- Repeatable
- Easier to maintain
- Traceable
- More suitable for future refreshes
- Safer than manually editing source data

---

# 7. Step 2 – Data Cleaning Using Power Query Editor

Before creating the dashboard, the dataset was cleaned and prepared using **Power Query Editor**.

This is an important part of the project because dashboard accuracy depends heavily on data quality.

## 7.1 Column and Data-Type Validation

The first step is to verify that every field has an appropriate data type.

Typical data-type assignments for this dataset include:

- `Date` → Date
- `Time` → Time
- `Booking ID` → Text
- `Booking Status` → Text
- `Customer ID` → Text
- `Vehicle Type` → Text
- `Pickup Location` → Text
- `Drop Location` → Text
- `Avg VTAT` → Decimal Number
- `Avg CTAT` → Decimal Number
- `Booking Value` → Decimal Number
- `Ride Distance` → Decimal Number
- `Driver Ratings` → Decimal Number
- `Customer Rating` → Decimal Number
- Cancellation/incomplete indicators → Numeric fields
- Payment Method → Text

Correct data types are especially important because Power BI treats text, dates, integers, and decimal values differently during calculations and visualizations.

---

## 7.2 Cleaning Text Fields

Text columns can contain inconsistent formatting such as:

- Extra spaces
- Unwanted quotation marks
- Inconsistent text formatting
- Blank values

The Power Query cleaning process can standardize text fields using transformations such as:

- Trim
- Clean
- Replace Values
- Change Data Type

This is particularly useful for fields such as:

- Booking ID
- Customer ID
- Vehicle Type
- Booking Status
- Pickup Location
- Drop Location
- Payment Method
- Cancellation reasons

Clean categorical values ensure that Power BI does not incorrectly treat visually similar values as different categories.

---

## 7.3 Handling Missing Values

The dataset contains missing values in several operational fields.

For example, cancellation-reason columns are naturally blank for bookings that were not cancelled. Similarly, booking value, ride distance, payment method, and ratings are not populated for every booking status.

Therefore, missing values need to be interpreted according to business meaning rather than automatically treating every blank as an error.

For example:

- A completed ride can have booking value and ride distance.
- A cancelled booking may not have a completed ride distance.
- A non-cancelled booking does not need a cancellation reason.
- A booking without a driver does not necessarily have driver-rating information.

This distinction is important because **blank does not always mean bad data**.

---

## 7.4 Validating Numerical Columns

Numerical fields were reviewed before dashboard creation.

Important numeric columns include:

- Booking Value
- Ride Distance
- Avg VTAT
- Avg CTAT
- Driver Ratings
- Customer Rating
- Cancellation indicators
- Incomplete ride indicators

The purpose of this validation is to ensure that numerical fields can be correctly aggregated using:

- Sum
- Average
- Count
- Minimum
- Maximum
- DAX measures

---

## 7.5 Date Preparation

The `Date` field is critical because the dashboard contains date filtering and time-based analysis.

The data covers 2024, allowing the dashboard to analyze booking activity across the year.

The dashboard uses a **Date slicer**, allowing users to select a particular date or date range and dynamically update the visuals.

---

## 7.6 Why Cleaning Was Completed Before Dashboard Creation

The correct Power BI workflow is:

**Raw Data → Cleaning → Modeling → Measures → Visualization**

If the raw data is directly used for visualization, problems such as incorrect data types, inconsistent categories, missing-value issues, and incorrect calculations can affect the dashboard.

Cleaning first creates a reliable foundation for the later modeling and reporting stages.

---

# 8. Step 3 – Loading the Cleaned Data

After the Power Query transformations were completed, the prepared data was loaded into the Power BI data model.

At this stage, the data becomes available for:

- DAX calculations
- Measures
- Filtering
- Aggregation
- Visualizations
- Dashboard interactions

The central analytical table in the report is the **Uber** dataset.

---

# 9. Step 4 – Data Modeling

After cleaning the data, the next stage was **Data Modeling**.

Data modeling is the process of organizing data so that Power BI can calculate metrics correctly and efficiently.

The project uses the cleaned Uber table as the main analytical source.

### Why data modeling is important

Without proper modeling, a dashboard may:

- Produce incorrect totals
- Aggregate data incorrectly
- Become difficult to maintain
- Make calculations harder
- Create inconsistent KPIs

A good model allows the same dataset to support different business views such as revenue, vehicle performance, cancellations, and ratings.

---

# 10. Step 5 – Creating DAX Measures

After data preparation and modeling, custom measures were created using **DAX (Data Analysis Expressions)**.

Measures are dynamic calculations. Unlike manually calculated columns, measures respond to filters and slicers applied to the report.

This is particularly important in this project because selecting a date range should automatically change the dashboard KPIs.

## Measures identified in the Power BI report

The dashboard uses measures including:

- Count of Booking ID
- Count of Booking Status
- Success Booking Value
- sum of Ride distance
- Avg.Distance travelled
- Total Distance Travelled
- Cancellation Rate %

---

## 10.1 Count of Booking ID

This measure is used to determine the number of bookings.

Conceptually:

```DAX
Count of Booking ID =
COUNT('Uber'[Booking ID])
```

### Business meaning

It answers:

> How many bookings are included in the current filter context?

Because it is a measure, selecting a different date range can change the result automatically.

---

# 11. Success Booking Value

The **Success Booking Value** measure is used to focus on booking value associated with successful/completed rides rather than treating every booking as completed revenue.

Conceptually, this type of measure can be created using a filtered calculation:

```DAX
Success Booking Value =
CALCULATE(
    SUM('Uber'[Booking Value]),
    'Uber'[Booking Status] = "Completed"
)
```

### Why this measure is important

The dataset contains cancelled, incomplete, and unsuccessful booking records. Simply summing all booking values can therefore give a misleading picture of successful ride revenue.

A success-focused measure provides a more meaningful business KPI.

---

# 12. Average Distance Travelled

The dashboard contains an **Avg.Distance travelled** measure.

Conceptually:

```DAX
Avg.Distance travelled =
AVERAGE('Uber'[Ride Distance])
```

### Business meaning

This KPI answers:

> On average, how far are rides travelling?

It can help compare the operating characteristics of different vehicle types.

---

# 13. Total Distance Travelled

The dashboard also contains a **Total Distance Travelled** measure.

Conceptually:

```DAX
Total Distance Travelled =
SUM('Uber'[Ride Distance])
```

### Business meaning

This measures the total recorded ride distance within the current filter context.

It can be useful for understanding:

- Overall utilization
- Vehicle-type contribution
- Distance trends
- Operational scale

---

# 14. Cancellation Rate %

The dashboard includes a **Cancellation Rate %** measure.

A cancellation-rate KPI is generally designed to compare cancelled bookings with total bookings within the current filter context.

A common conceptual implementation is:

```DAX
Cancellation Rate % =
DIVIDE(
    [Cancelled Bookings],
    [Total Bookings],
    0
)
```

The exact business definition of the rate should be kept consistent throughout the report.

This metric is important because cancellation rate is not just a count; it measures the **proportion of bookings affected by cancellations**.

---

# 15. Why Measures Were Created Instead of Only Using Columns

A major advantage of DAX measures is that they are **filter-aware**.

For example:

If the user selects:

> January 2024

the measure calculates January's value.

If the user changes the slicer to:

> January – June 2024

the same measure automatically recalculates for that period.

This makes measures ideal for interactive Power BI dashboards.

---

# 16. Dashboard Structure

The Power BI report contains six main pages:

1. **Home Page**
2. **Overall**
3. **Vehicle Type**
4. **Revenue**
5. **Cancellation**
6. **Rating**

Each page answers a different business question.

---

# 17. Home Page

The Home Page acts as the landing/navigation page of the report.

Its purpose is to provide a clean entry point into the dashboard.

It contains:

- Dashboard branding
- Navigation elements
- Visual design elements
- Access to the analytical sections

The Home Page is not intended to display every KPI. Instead, it creates a structured starting point for the report.

---

# 18. Overall Dashboard

The **Overall** page provides a high-level summary of Uber booking performance.

### Main components

The page contains:

- Total booking KPI
- Date slicer
- Booking-status distribution
- Booking trend over time

### Booking KPI

The booking KPI provides a quick view of the number of bookings in the selected filter context.

This is useful for management because it gives an immediate understanding of operational volume.

---

## 18.1 Booking Status Distribution

The dashboard uses a pie chart to show the distribution of booking statuses.

The major categories are:

- Completed
- Cancelled by Driver
- Cancelled by Customer
- Incomplete
- No Driver Found

### Why this visual matters

The pie chart provides a quick answer to:

> What percentage of bookings are successful versus unsuccessful?

A high completed share indicates strong conversion from booking to completed ride.

Cancellation and unsuccessful categories highlight operational areas requiring attention.

---

## 18.2 Booking Trend Over Time

The Overall page also includes a line chart using booking count and date.

This visual helps identify:

- High-demand periods
- Low-demand periods
- Changes in booking volume
- Trends across the year

### Business use

A time-series view can support decisions related to:

- Driver availability
- Fleet planning
- Demand forecasting
- Staffing
- Promotions
- Operational capacity

---

## 18.3 Date Slicer

The date slicer is an important interactive feature.

Users can select a date or date range.

When the selection changes, the relevant dashboard calculations and visuals respond to the selected filter context.

This converts the report from a static dashboard into an interactive analytical tool.

---

# 19. Vehicle Type Dashboard

The **Vehicle Type** page focuses on performance across different Uber vehicle categories.

The dashboard compares:

- Booking Value
- Successful Booking Value
- Average Distance
- Total Distance
- Vehicle types

Vehicle types include:

- Auto
- Go Mini
- Go Sedan
- Bike
- Premier Sedan
- eBike
- Uber XL

---

## 19.1 Booking Value by Vehicle Type

Multiple KPI cards are used to compare booking value for individual vehicle types.

This helps answer:

> Which vehicle types contribute the most booking value?

For example, a business analyst can compare Auto against Go Mini, Go Sedan, Premier Sedan, Bike, eBike, and Uber XL.

---

## 19.2 Successful Booking Value by Vehicle Type

The dashboard also uses the **Success Booking Value** measure for selected vehicle types.

This is more meaningful than looking only at total booking value because it focuses on completed/successful bookings.

### Business question

> Which vehicle types generate the strongest value from successful rides?

This can support:

- Fleet planning
- Vehicle availability decisions
- Pricing strategy
- Service optimization

---

## 19.3 Average Distance by Vehicle Type

The **Avg.Distance travelled** measure is used to compare average ride distance for each vehicle type.

This helps understand how each category is being utilized.

For example:

- Short-distance categories may be more suitable for urban trips.
- Longer-distance categories may be more relevant for premium or larger vehicle services.

---

## 19.4 Total Distance by Vehicle Type

The **Total Distance Travelled** measure shows the total recorded distance associated with each vehicle type.

This allows the analyst to distinguish between:

- Vehicles that handle many/long rides
- Vehicles that contribute relatively less distance
- High-utilization categories

Combining total distance with successful booking value gives a stronger operational picture than looking at either metric alone.

---

# 20. Revenue Dashboard

The **Revenue** page focuses on the financial and transactional side of the dataset.

It contains:

- Date slicer
- Customer-level/month-level booking-value table
- Payment-method analysis
- Ride-distance analysis over time

---

## 20.1 Revenue/Booking Value Table

The table displays fields such as:

- Customer ID
- Month
- Booking Value

This provides a more detailed view than KPI cards.

The table can help users investigate individual customer/month combinations and understand how booking value is distributed.

---

## 20.2 Booking Value by Payment Method

A column chart compares booking value across payment methods.

Payment methods represented include:

- UPI
- Cash
- Uber Wallet
- Credit Card
- Debit Card

### Business questions

This visual helps answer:

> Which payment methods contribute the most booking value?

This can be useful for:

- Digital-payment strategy
- Payment partnerships
- Customer convenience analysis
- Transaction monitoring

---

## 20.3 Ride Distance Over Time

The Revenue page also contains a column chart using ride distance and date/month information.

This helps understand how ride activity changes over time.

Combining booking value and ride distance can help analyze the relationship between:

- Operational activity
- Distance travelled
- Booking value

---

# 21. Cancellation Dashboard

The **Cancellation** page focuses on why bookings fail or get cancelled.

This is one of the most important operational-analysis sections because cancellation directly affects customer experience, driver utilization, and potential revenue.

---

## 21.1 Customer Cancellation Analysis

A pie chart uses:

- Reason for cancelling by Customer
- Cancelled Rides by Customer

Customer cancellation reasons include categories such as:

- Wrong Address
- Change of plans
- Driver not moving towards pickup location
- Driver asked to cancel
- AC not working

### Business interpretation

This analysis helps identify customer pain points.

For example, if many customers cancel because the driver is not moving toward the pickup location, the business may need to investigate:

- Driver assignment
- Driver acceptance behavior
- GPS/navigation problems
- Pickup communication
- Driver availability

---

# 22. Driver Cancellation Analysis

A second pie chart analyzes driver cancellations using the driver cancellation reason.

The dataset includes reasons such as:

- Customer related issue
- Customer coughing/sick
- Personal & Car related issues
- More than permitted people in the vehicle

### Business interpretation

Driver cancellations can indicate operational problems related to:

- Driver behavior
- Customer behavior
- Vehicle condition
- Safety
- Trip suitability
- Driver policies

Understanding these reasons is more useful than looking only at the cancellation count.

---

# 23. Cancellation KPI Cards

The Cancellation page also includes KPI cards for cancellation-related metrics.

These cards provide quick answers to questions such as:

- How many bookings were cancelled?
- Which cancellation category is being analyzed?
- What is the cancellation rate?
- Which driver cancellation reason is contributing to the selected result?

The **Cancellation Rate %** measure is particularly useful because it converts raw cancellation counts into a normalized performance metric.

---

# 24. Rating Dashboard

The **Rating** page evaluates customer and driver satisfaction.

It contains KPI cards comparing:

- Customer Rating by vehicle type
- Driver Rating by vehicle type

This allows the business to understand whether service quality differs across vehicle categories.

---

## 24.1 Customer Rating by Vehicle Type

The dashboard compares average customer ratings across:

- Go Mini
- Go Sedan
- Uber XL
- Premier Sedan
- Auto
- Bike
- eBike

### Business question

> Which vehicle types receive the best customer ratings?

This can help identify service categories that deliver stronger customer satisfaction.

---

## 24.2 Driver Rating by Vehicle Type

The dashboard also compares driver ratings across vehicle types.

This can help answer:

> How are drivers performing across different vehicle categories?

Driver ratings can be used as one indicator of service quality and operational performance.

---

# 25. Interactive Dashboard Features

One of the main strengths of this Power BI project is interactivity.

The dashboard includes date slicers and filter-aware measures.

### Example

Suppose the user selects:

**January 1 – March 31, 2024**

The report can recalculate:

- Booking count
- Booking status distribution
- Successful booking value
- Vehicle performance
- Revenue analysis
- Cancellation metrics
- Rating metrics

This allows the user to perform **ad-hoc analysis without modifying the underlying dataset**.

---

# 26. Dashboard Design Approach

The report is designed as a multi-page analytical dashboard rather than putting every chart onto a single page.

This improves usability because each page has a clear analytical purpose.

### Page hierarchy

**Home**
→ Navigation

**Overall**
→ General business performance

**Vehicle Type**
→ Fleet/category performance

**Revenue**
→ Financial/payment analysis

**Cancellation**
→ Operational problems

**Rating**
→ Customer and driver satisfaction

This structure follows a business-analysis storytelling approach.

---

# 27. End-to-End Project Workflow

The complete workflow of the project can be summarized as:

```text
Raw Uber CSV
      ↓
Data Import into Power BI
      ↓
Power Query Editor
      ↓
Data Cleaning & Transformation
      ↓
Data Type Validation
      ↓
Handling Missing/Blank Values
      ↓
Categorical/Text Standardization
      ↓
Load Clean Data
      ↓
Data Modeling
      ↓
Create DAX Measures
      ↓
Build KPIs
      ↓
Create Visualizations
      ↓
Add Slicers & Interactions
      ↓
Dashboard Design
      ↓
Business Analysis & Insights
```

---

# 28. Business Insights That Can Be Derived

The dashboard is designed to answer several practical business questions.

### Booking Performance

- How many bookings are being generated?
- What percentage of bookings are completed?
- How many bookings fail because no driver is found?
- Are cancellations increasing or decreasing?

### Vehicle Performance

- Which vehicle type generates the highest booking value?
- Which vehicle type has the highest successful booking value?
- Which vehicle type travels the most distance?
- What is the average distance for each vehicle type?

### Revenue

- Which payment method contributes the most booking value?
- How does booking value change over time?
- How does ride distance change over time?

### Cancellation

- Why do customers cancel rides?
- Why do drivers cancel rides?
- Which cancellation reason is most common?
- What is the cancellation rate?

### Customer Experience

- Which vehicle type has the highest customer rating?
- Which vehicle type has the highest driver rating?
- Are certain vehicle categories consistently associated with better ratings?

---

# 29. Key Analytical Takeaway

The major strength of this project is that it does not stop at simply displaying raw data.

The project transforms transactional data into **business-oriented KPIs and analytical views**.

The progression is:

**Data → Information → Metrics → Analysis → Business Insights**

For example:

Raw data tells us that a booking has a status.

The dashboard converts this into:

> Booking Status Distribution

Raw data contains booking values.

The dashboard converts this into:

> Successful Booking Value and Vehicle-Level Revenue Analysis

Raw data contains cancellation reasons.

The dashboard converts this into:

> Customer and Driver Cancellation Analysis

Raw data contains ratings.

The dashboard converts this into:

> Vehicle-Level Customer and Driver Satisfaction Analysis

This is the core purpose of a Business Intelligence dashboard.

---

# 30. Technologies Used

### Microsoft Power BI
Used for:

- Data modeling
- DAX
- Dashboard development
- Interactive reporting
- Data visualization

### Power Query
Used for:

- Data cleaning
- Data transformation
- Data-type preparation
- Handling data-quality issues
- Preparing the source for modeling

### DAX
Used for:

- Dynamic measures
- KPI calculations
- Filter-aware calculations
- Business metrics

### CSV
Used as the original data source.

---

# 31. Skills Demonstrated

This project demonstrates practical skills in:

- Data cleaning
- Power Query
- Data transformation
- Data modeling
- DAX
- KPI development
- Data visualization
- Interactive dashboard design
- Business analysis
- Trend analysis
- Revenue analysis
- Cancellation analysis
- Customer satisfaction analysis

---

# 32. Project Outcome

The final Power BI report converts a **150,000-record Uber booking dataset** into an interactive multi-page analytics solution.

The report provides separate analytical views for:

- Overall performance
- Vehicle type performance
- Revenue
- Cancellations
- Ratings

The combination of **Power Query + Data Modeling + DAX + Visualization** demonstrates an end-to-end Power BI workflow suitable for a portfolio or data-analytics project.

---

# 33. Recommended Project Presentation Explanation

When explaining this project in an interview, the project can be described as:

> "I developed an Uber Ride Analytics Dashboard using Power BI. I started with a raw CSV dataset containing 150,000 booking records. Before creating the dashboard, I used Power Query Editor to clean and prepare the data, including validating data types, standardizing fields, and handling missing values according to their business meaning. I then loaded the cleaned data into the Power BI data model and created DAX measures such as booking count, successful booking value, average distance, total distance travelled, and cancellation rate. Finally, I built a six-page interactive dashboard covering overall performance, vehicle types, revenue, cancellations, and ratings. I added date slicers so that the KPIs and visuals dynamically respond to the selected period. The dashboard helps analyze booking performance, vehicle utilization, revenue, cancellation reasons, and customer and driver satisfaction."

---

# 34. Conclusion

This Uber Power BI project demonstrates how raw transactional data can be transformed into a structured Business Intelligence solution.

The project follows a professional analytics workflow:

**Power Query → Data Modeling → DAX → Visualization → Business Insights**

The dashboard is not only a collection of charts. Each page is designed around a specific business question, making the final report useful for understanding operational performance, revenue, vehicle utilization, cancellations, and customer experience.

