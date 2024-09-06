<h1> Spunk-Single-Visualization-Config </h1>

Solution Guide:  Single-value Visualizations
In this activity, you were tasked with designing a radial gauge to illustrate the severity of a single value.
![1](https://github.com/user-attachments/assets/254969af-aa31-4da9-8433-33c1f087bec1)

Upload the radialgauge.csv file to your local Splunk system located in the splunk/logs/Week-2-Day-1-Logs directory. Select all defaults during the upload process.

Design a search to view the POST events:

source="radialgauge.csv" http_method=POST |stats  count as total

Design a radial gauge to visualize the data.


Select Visualization > Radial Gauge.


Change the ranges of the radial gauge by selecting Format > Color Ranges > Manual.


The ranges can vary, as long as 1,200 POST requests per hour is in the red range. For example:

Green: 0–400
Yellow: 400–1,000
Red: 1,000–2,000





Save your visualization as a report titled "Radial Gauge – POST request monitor."


Once you save, the radial gauge should display.

Bonus
Design an alert to trigger when the the count reaches the red range.

This will vary from student to student depending on the ranges selected.
The bonus is correct if an alert is designed to trigger when the number of events reaches the lower part of the red range selected in Step 3.
