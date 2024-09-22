# <h1> SPLUNK DASHBOARD AND VISUALIZATION SETUP </h1>
# Project Overview
This project provides a step-by-step guide for visualizing and monitoring web traffic data using Splunk. The data in question is focused on `POST` events, and through various visualization tools like **radial gauges**, **pie charts**, and **geographic maps**, you’ll gain insights into server request patterns and create dashboards to consolidate and monitor these metrics. Each visualization is saved as a report, which is then assembled into a Splunk dashboard for monitoring and alerting.

# Detail Steps
# Upload the radialgauge.csv file to your Splunk environment:
Navigate to splunk/logs/Week-2-Day-1-Logs and upload the radialgauge.csv file.

![2](https://github.com/user-attachments/assets/07170b15-afcc-46a9-83ae-a9bb154d5c4a)

Select all default options during the upload.

![3](https://github.com/user-attachments/assets/854f0e92-669a-4596-b703-c3f1302f6abc)

## Single-Value Visualization (Radial Gauge)
In this exercise, I created a radial gauge to monitor the number of "POST" requests per hour.
Search: Use the following SPL query to count the number of POST events:
Query: source="radialgauge.csv" http_method=POST | stats count as total

![4](https://github.com/user-attachments/assets/ba922081-fe5b-4eab-bf3d-7624fc3b26a6)

Create the Visualization:
Go to Visualization > Radial Gauge.
Set the ranges under Format > Color Ranges > Manual. For example:
Green: 0–400
Yellow: 400–1000
Red: 1000–2000
Save the visualization as "Radial Gauge – POST request monitor".
Alert Setup:

Create an alert that triggers when the count reaches the red range (e.g., 1200+ POST requests/hour).




