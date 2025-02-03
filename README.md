# Los Angeles Wildfire (2025) Tableau Visualization Project with AWS Pipeline 🔥  

📅 Date: January, 2025  
👤 Author: Nirmalkumar Thirupallikrishnan Kesavan  
🛠️ Tech Stack: AWS (S3, Lambda, Glue Crawler, Athena, EventBridge), Web Scraping, Tableau, Python, Data Visualization  

## 📌 Overview
This project is a 🌎 dynamic and automated Tableau dashboard that visualizes real-time wildfire incidents in Los Angeles. The visualization updates every three hours using an AWS-based data pipeline, ensuring that insights remain fresh and relevant. 🔥

## 📹 [Project Video Demo](https://github.com/NirmalKumar31/Realtime-LA-wildfire-tableau-visualization-with-AWS-pipeline/blob/573b16ec3e2b313bc13d7fafad397332afe689cd/LA_wildfire_tableau_viz_project_demo.mp4)

## 🚀 Workflow & Architecture
### **1. Web Scraping & Data Storage (AWS S3) 🏗️**
- Since there is no single dataset available for wildfires, we scrape data from a [Wildfire Monitoring Website](https://www.fire.ca.gov/) 🌐
- A Lambda function _(DailyLAfiredata)_ runs the scraping script and stores the extracted data in an AWS S3 bucket _(lafiredata)_ in CSV format. 💾

### **2. AWS Athena - Transforming Data for Tableau 📊**
- The scraped data is stored in S3 but requires transformation.
- An Athena table _(fire_data)_ is created to structure and clean the dataset.
- A second table _(updated_fire_data)_ (a transformed view of `fire_data`) is created to ensure proper formatting (especially date-time adjustments) before connecting to Tableau. 🛠️

### **3. AWS Glue Crawler - Schema Update Automation 🔄**
- A Glue Crawler _(athena fire_data schedule)_ is scheduled to run on demand.
- The Glue Crawler scans new data in S3 and refreshes the Athena tables.
- To run the Glue Crawler, we have created another Lambda function called _(gluecrawlertrigger)_.  
- When this Lambda function is triggered, it initiates the Glue Crawler, which in turn refreshes the Athena tables. 🔄


### **4. Automating the Pipeline with AWS EventBridge ⏳**
- **Triggering Data Updates:**
  - The main Lambda function _(DailyLAfiredata)_ scrapes data and stores it in S3 bucket. 🔥
  - An EventBridge notification is enabled on the S3 bucket to detect new data uploads.
  - This triggers another Lambda function _(gluecrawlertrigger)_ that initiates the Glue Crawler.
  - Once the Glue Crawler is executed, Athena updates its tables with the latest wildfire data.
- **Final Tableau Connection:**
  - The transformed Athena table is linked to Tableau, ensuring real-time updates in the visualization. 📈

## 📊 Tableau Dashboard
- The Tableau dashboard visualizes wildfire incidents, showing active fires, affected areas, and other critical insights. 🌋
- Since the data pipeline updates every 3 hours, users always see the latest wildfire data. 🔥

## 🎯 Key Features
✅ **End-to-End AWS Data Pipeline** – Web scraping, S3 storage, Athena transformation, Glue Crawler automation, EventBridge orchestration.  
✅ **Real-Time Data Updates** – Automated refresh every 3 hours. 🔄  
✅ **Seamless Tableau Integration** – Live visual representation of wildfires. 🎥  
✅ **AWS Serverless Architecture** – Cost-effective and scalable solution using Lambda & Athena. ☁️  

## ⭐ Contribute & Connect
💡 If you find this useful, star ⭐ this repo!  

🔗 LinkedIn: [Nirmalkumar Thirupallikrishnan Kesavan](https://www.linkedin.com/in/nirmalkumartk/)  
🔗 GitHub: [NirmalKumar31](https://github.com/NirmalKumar31)  

