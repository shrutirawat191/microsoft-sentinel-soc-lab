### Visualizing Security Data in MS Sentinel

### Overview

Visualizing data on a SIEM is important because it transforms raw security logs and events into clear, actionable insights, enabling security teams to quickly understand patterns, trends, and anomalies. Large volumes of data from multiple sources can be overwhelming,
but visualizations like charts, graphs, and dashboards help analysts identify suspicious activity, prioritize threats, and monitor the overall security posture in real time. Effective visualization also supports faster decision-making during incidents, facilitates reporting to
stakeholders, and helps detect patterns that might be missed in textual logs, ultimately enhancing the efficiency and effectiveness of a SOC.

### Creating a Workbook in MS Sentinel

Workbooks are interactive dashboards that allow you to visualize, analyze, and explore security data from multiple sources. They combine charts, tables, and text to present insights from logs and alerts, helping SOC analysts
monitor trends, investigate incidents, and make data-driven decisions in a single, customizable interface.

In this example, we will create a workbook that will help visualize frequently triggered security alerts in the past 30 days.

<img width="975" height="424" alt="image" src="https://github.com/user-attachments/assets/b2285805-84c2-4a19-a613-86c152d77f73" />

<img width="975" height="401" alt="image" src="https://github.com/user-attachments/assets/62cad8c9-add8-4445-a929-4e21e08cb910" />

                                    SecurityAlert
                                    | summarize Alertcount = count() by Alertname
                                    | sort by Alertcount desc

<img width="975" height="208" alt="image" src="https://github.com/user-attachments/assets/86aadd76-6721-4676-8cbe-94cf17f33f38" />

<img width="975" height="420" alt="image" src="https://github.com/user-attachments/assets/7cab04a2-0451-4865-b5a9-5ef7f4ed7622" />

This query will summarize the amount of alerts by alert name and consolidate it in a pie chart.

<img width="402" height="403" alt="image" src="https://github.com/user-attachments/assets/e2c6c38a-0a3c-4b61-a7dd-d62abd729de8" />


**Final Workbook:**

<img width="975" height="410" alt="image" src="https://github.com/user-attachments/assets/4e3fb836-9e6e-4751-bc9e-8b576ad34f14" />

**Create a Workbook For Security Alerts**

Follow the steps from before, and use the following query. This query filters alerts that were generated in the last 30 days and groups them to show the number of alerts per day over the past 30 days.

<img width="968" height="397" alt="image" src="https://github.com/user-attachments/assets/daf3e448-5a0e-44b3-8d6e-331c856ffa69" />

