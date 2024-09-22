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
- Search: Use the following SPL query to count the number of POST events:
- Query: source="radialgauge.csv" http_method=POST | stats count as total

![4](https://github.com/user-attachments/assets/ba922081-fe5b-4eab-bf3d-7624fc3b26a6)

# Create the Visualization:
- Go to Visualization > Radial Gauge.
- Set the ranges under Format > Color Ranges > Manual. For example:
- Green: 0–400
- Yellow: 400–1000
- Red: 1000–2000
- Save the visualization as "Radial Gauge – POST request monitor".

![5](https://github.com/user-attachments/assets/8e4b12e5-1610-4488-bd15-f622521ee58c)

# Alert Setup:
Create an alert that triggers when the count reaches the red range (e.g., 1200+ POST requests/hour).

![6](https://github.com/user-attachments/assets/88d443ac-fe41-4171-b44f-f96f13492424)

# Quering Successful Account Logged on Events
Uploading the Source document:
- Locate Source File:Source="demo_winlogs.csv" host="WinsLogs" sourcetype="csv" and injest into Splunk

![7a](https://github.com/user-attachments/assets/7eb73834-c556-4ad8-9855-75ddddfac25e)

Open your Splunk search interface:
- From the left hand menu
- Drill down to subject
- From the pop-up to the left
- Select "An account was successfully logged on"

![8a](https://github.com/user-attachments/assets/600e3f93-f5bc-4fcf-a4b8-a3a2d7cf8bc4)

Use the following Splunk Query Language (SPL) to find events where the subject is "An account was successfully logged on":

- Query: host="WinsLogs" sourcetype="csv" subject="An account was successfully logged on"

![9a](https://github.com/user-attachments/assets/e49f2776-eec7-437f-b06d-fd2731f68d91)

# Create the Visualization:
Once the results are displayed, you can create a visualization by selecting the Visualization tab at the top of the search results.

Choose one of the following chart types depending on how you want to represent the data:
- Bar Chart to show successful logons per user.
- Pie Chart for a proportionate view of logon events by account.
- Column Chart for side-by-side comparison of logon events.

- Graphing the query and also piping the top 20 successful logged on by user on a Bar chart:

![10a](https://github.com/user-attachments/assets/baac88c4-e82a-4f23-bbb2-b28692274e3a)

- Pie Chart for a proportionate view of logon events by account:

![11a](https://github.com/user-attachments/assets/ccbfcda2-c7cc-439f-80ea-1c2ee565ca0f)

# Creating a report for the Pie Chart Logins
- After customizing your visualization, click on Save As and choose Report.
- Give it a meaningful title like "LoginPie Chart" and save the report.

![12a](https://github.com/user-attachments/assets/d1119f23-6b03-4aa0-bb87-d926746a3927)

# Multiple-Value Visualization (Pie Chart and Bar Chart) 
Next, we’ll design a pie chart to display the top 10 URI paths with the most POST requests.
- Search: Use this SPL query to get the top 10 URI paths:
- source="radialgauge.csv" http_method=POST | top limit=10 uri_path

# Create the Visualization:
- Go to Visualization > Pie Chart:

![14a](https://github.com/user-attachments/assets/9a7437e0-18a6-4f96-9ff8-b630a704a426)

- Go to Visualization > Bar Chart:

![13a](https://github.com/user-attachments/assets/085bdc82-496d-4888-8eec-e9fb176b4951)

  
- Save the visualization as "Pie Chart – Top 10 URI_PATH".

![15a](https://github.com/user-attachments/assets/9292f761-2e97-425d-955f-ab64d684514c)

![16a](https://github.com/user-attachments/assets/010f4461-7c98-45e0-a1cb-0c80a818fffe)

# Geographic Map Visualization
In this task, I visualize the locations of source IP addresses making POST requests.

Search: Use the following SPL query:

- Query: source="radialgauge.csv" http_method=POST | iplocation src_ip | geostats count

![20b](https://github.com/user-attachments/assets/242216c0-6d8f-4ad9-a365-9847a4c41b48)

- Zoom! Zoom! by hitting the + sign to the left of the window for clarity

![21b](https://github.com/user-attachments/assets/db058bc9-3f2b-46fa-b1b3-ab2d5d8f074e)

# Modify the search to display the attacked URIs on the same map:

- Query: source="radialgauge.csv" http_method=POST | iplocation src_ip | geostats count by uri_path

![22b](https://github.com/user-attachments/assets/9bb8ad55-8a21-4b4e-b5d2-8e4daca3c396)

# Dashboard Creation
Now, we'll combine all visualizations into a single dashboard.

# Add the Radial Gauge:
- Select the saved radial gauge report:

![24c](https://github.com/user-attachments/assets/c5ec0f82-d956-425f-9375-b4bc4c039eed)

- Add it to a new dashboard titled "Demo Dashboard":

![25c](https://github.com/user-attachments/assets/efc9f4de-d40c-4001-ae25-14088b75a0df)

![26c](https://github.com/user-attachments/assets/6e4a38c9-465a-4975-b902-ae912eeb0078)

- Add Other Visualizations:

- Add the pie chart and geographic map to the same dashboard

![27c](https://github.com/user-attachments/assets/16345c9e-6568-4575-ba75-d2210c5ee13e)

- selecting the Existing Dashboard option

![28c](https://github.com/user-attachments/assets/caf05e03-e67e-48ef-b861-0b489a8064fb)

![29c](https://github.com/user-attachments/assets/f23e3249-8c84-42dd-9ab9-e5384fcac14d)

- Additional Visualization:

![30c](https://github.com/user-attachments/assets/9b1d3ebb-4541-41bf-b9e7-ada5552e2cb0)

- Add a statistical view of the pie chart next to the pie chart in the dashboard.

![31c](https://github.com/user-attachments/assets/2584f04b-f801-4fab-988d-056977c1f836)

# Advanced Dashboard Modifications
Time Range Input:

- Edit the dashboard and add a Time Range input for all panels:

![32c](https://github.com/user-attachments/assets/a74a7457-1b77-4bf8-8bc0-75307a7d245b)

- 1 Minute Window:

![32c](https://github.com/user-attachments/assets/a0346314-808e-4e52-b361-f012e0fca584)

- Year to Date:

![34c](https://github.com/user-attachments/assets/cbf2328e-d774-4285-9b25-348c657b6908)

- All Time:

![35c](https://github.com/user-attachments/assets/81927f4e-efbe-4d53-b545-670153164ea5)

# Drilldown Functionality:

- Adding a drilldown feature to the geographic map panel that links to a new search when clicked.

![36d](https://github.com/user-attachments/assets/e3407fc9-6a30-4028-9b42-8cbaca34e121)

- Adding a click Function to the Dashboard

![37d](https://github.com/user-attachments/assets/9a97b022-7d7d-4583-8c16-c9cb1ec5f187)

- Clicking any user from the Top 10 Users Dashboard will open a drill down in the search window for that user:

![38d](https://github.com/user-attachments/assets/ed4aaea1-ad41-43d6-a03a-de034cb93fd8)

# Conclusion

This Splunk Data Visualization and Dashboard repository provides a comprehensive walkthrough of key Splunk data visualization and dashboard creation exercises for monitoring and analyzing server POST request events. By following the provided steps, users can efficiently generate radial gauges, pie charts, and geographic maps to visualize and track data in real-time, culminating in a consolidated dashboard for web activity monitoring.

This repository not only guides users through essential visualizations but also demonstrates advanced dashboard features, such as time-based inputs and drilldown capabilities. It empowers users to create custom visual reports, monitor server activity, and set up alerts for critical events, thus enhancing their ability to manage and respond to network traffic patterns effectively.

Contributors are welcome to improve or expand upon this guide by following the contribution guidelines. This project stands as a useful resource for anyone looking to learn about or improve their Splunk visualization skills for SIEM monitoring and data analysis.
