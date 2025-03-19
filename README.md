## 🎯 Problem Statement

"Analyzing airline punctuality in India (Jan 2024 - Sep 2024) by examining flight delays and on-time performance across different airlines to identify patterns and recommend improvements."

#### 🔍 Understanding Key Performance Indicators (KPIs)

Since we don’t have individual flight details (like delay minutes per flight), we need to analyze aggregated statistics:

📊 Primary KPIs (Most Important Metrics)
1️. Total Departures per Airline → Which airline handles the most flights?

2️. Total Delays per Airline → Which airline faces the most delays?

3️. On-Time Performance (%) → Which airlines are the most punctual?

4️. Delay Rate (%) → What % of flights are delayed per airline?
    Delay Rate=(Number of Departures/Number of Flight Delays)×100

5️. Rank Airlines by Punctuality → Sort airlines based on % on-time performance.

### Step 1: Data Collection & Preprocessing (ETL)

    Get the latest flight delay data in India Open Government Data (OGD) Platform India.
 #### Part 1 Summary: Tasks Completed

Here's a breakdown of what did in Part 1:
🔹 1. Data Extraction (Loading the CSV)

    1.1. Read the CSV file into a Pandas DataFrame.
    1.2. Manually checked for inconsistencies in the data.

🔹 2. Data Cleaning & Transformation

    2.1. Identified and fixed data inconsistencies:
        2.1.1. Corrected the misspelled month (Auguest → Aug-24).
        2.1.2. Ensured the Month column was properly formatted as a date.

    2.2. Converted data types:
        2.2.1 Fixed % On-time Performance, which was initially stored as a string.
        2.2.2 Ensured all necessary columns were converted to numeric (int/float) for calculations.

    2.3. Validated and corrected performance calculations:
        2.3.1.  Recalculated On-Time Arrival Rate using the formula:
        2.3.2. On-Time Rate=100−(Flights DelayedFlights Departed×100)
        2.3.3. On-Time Rate=100−(Flights DepartedFlights Delayed×100)
        2.3.4. Compared with existing values and replaced incorrect ones.

    2.4. Rounded values for consistency (2 decimal places).

    2.5. Renamed columns for better readability:
       2.5.1 % On-time Performance → On-Time Arrival Rate (%)
       2.5.2 Calculated Performance → Delay Rate (%)

🔹 3. Data Loading (Saving the Processed Data)
    Saved the cleaned and transformed data into a new CSV file.

#### Step 2: Exploratory Data Analysis (EDA) using SQL
Dataset Overview:

1. Columns: Airline, Month, Number of Departures, Number of Flights Delayed, On-Time Performance (%),Delay Rate.
2. Time Period: January 2024 - September 2024.
3. Data Source: Processed dataset after cleaning and validation.

Example quieres perfomed on the dataset:

    " SELECT
        DATE_FORMAT(month, '%b %Y') AS month_name,
        AVG((flights_delayed / departures) * 100) AS avg_delay_rate
        FROM flight_performance
        GROUP BY month
        ORDER BY month;
    "
    
The outputs of EDA analysis are backed up by the step-3
EDA using SQL provides insights into flight delays across months and airlines. The analysis highlights:

1. Seasonal Trends – Certain months experience higher delays.

2. Airline Performance – Some airlines consistently perform better in punctuality.

3. Operational Insights – Airlines can use this data to improve scheduling and customer service.

#### Step 3: Data Transformation and visualization in Tableau
   ![Average monthly delay 2024](https://github.com/Bindusrinaik04/Flight_operations_analysis_2024/blob/main/Screenshot%20(32).png)

   ![Airline_wise_departure_2024](https://github.com/Bindusrinaik04/Flight_operations_analysis_2024/blob/main/Screenshot%20(33).png)
   
   ![Airline_wise_delay_2024](https://github.com/Bindusrinaik04/Flight_operations_analysis_2024/blob/main/Screenshot%20(34).png)
   
   ![Airline_delay_rate_2024](https://github.com/Bindusrinaik04/Flight_operations_analysis_2024/blob/main/Screenshot%20(35).png)
   
   ![Airline_On_time_performance](https://github.com/Bindusrinaik04/Flight_operations_analysis_2024/blob/main/Screenshot%20(36).png)

#### Step 4: Summary of findings
Summary of Findings:
###### 1️. Monthly Average Delay Trends:

    1. January & July had the highest average delay rates (43.4% & 42.9%), indicating possible seasonal or operational challenges.
    2. March to June showed the lowest delays (27-32%), suggesting smoother operations during these months.
    3. August & September had moderate delays (~39%), possibly due to monsoon-related disruptions.

##### 2 ️. Airline Performance & Delays & Ranking:

    1. Indigo had the most departures but a manageable delay rate (29.3%), showing strong operational efficiency.
    2. SpiceJet & Alliance Air had the highest delay rates (50.6% & 47.0%), indicating severe on-time performance issues.
    3. Air India also faced significant delays (36.5%), despite fewer departures.
    4. Vistara, Akasa Air, and AIX Connect showed relatively better performance, with delay rates around 24-28%.

##### 3.Overall Insights:

    1. Delays peak in winter (January) and monsoon months (July-August), possibly due to weather conditions.
    2. Some airlines struggle with on-time performance more than others, suggesting a need for better scheduling and fleet management.
    3. Further analysis on airport congestion and time-of-day delays could provide deeper insights into delay patterns.
