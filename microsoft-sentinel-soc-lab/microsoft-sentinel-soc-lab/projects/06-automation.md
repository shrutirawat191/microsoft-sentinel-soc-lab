# 6. Playbooks and Logic Apps in MS Sentinel

## Objective
Document how Sentinel playbooks, Azure Logic Apps, and Workbooks can support incident response and monitoring.

## Workflow
In Microsoft Sentinel, a playbook is an automated response plan for security incidents. It’s built on top of Azure Logic Apps and defines what should happen when a certain alert or
trigger occurs. Logic Apps is the underlying Azure service used to create automated workflows. This is a no-code platform where you can drag and drop connectors, steps, and conditions. Logic apps can be used to automate any workflow, not just for security.
Playbooks are necessary for SOC analysts because they turn manual, repetitive, and timesensitive tasks into fast, consistent, and automated workflows. This reduces human error
and speeds up incident response. 

**Create an Automation Rule**

<img width="975" height="443" alt="image" src="https://github.com/user-attachments/assets/b1dea8ef-cc28-42a5-9932-6086f7043640" />

<img width="975" height="345" alt="image" src="https://github.com/user-attachments/assets/32b47ab1-1016-4435-95df-5303a08ebb04" />

<img width="975" height="402" alt="image" src="https://github.com/user-attachments/assets/5b0efc3d-73bd-4e62-8054-f1e6f54524a5" />

<img width="975" height="496" alt="image" src="https://github.com/user-attachments/assets/048fe6bf-c44a-43d1-9008-59ff16fdf616" />

<img width="975" height="548" alt="image" src="https://github.com/user-attachments/assets/6c62af2a-0f8d-4203-aada-5ddc85608b48" />

<img width="975" height="554" alt="image" src="https://github.com/user-attachments/assets/e32d069e-e40a-4377-8407-c049a8a1037d" />


**Manually brute force the VM and check whether our automation is working properly.**

Before Brute Force Attempt:

<img width="975" height="438" alt="image" src="https://github.com/user-attachments/assets/fe75c017-20f6-4a9d-933b-4a2e7b2e18b1" />

After Brute Force Attempt

<img width="975" height="406" alt="image" src="https://github.com/user-attachments/assets/aedc5527-ae7e-4a37-b257-256b40b4d807" />

Observe the automation rules take action (Incident gets assigned, status changed, new task with investigation instructions)


<img width="975" height="494" alt="image" src="https://github.com/user-attachments/assets/d79ab5d2-d61f-4e7d-a44e-ce4d0a6a5657" />


**Creating a Playbook in MS Sentinel**

Now we will build a basic playbook in MS Sentinel that automatically sends an email notification

<img width="975" height="449" alt="image" src="https://github.com/user-attachments/assets/3e122556-53b9-40bd-92ff-134d552965b5" />

<img width="975" height="605" alt="image" src="https://github.com/user-attachments/assets/d4c1fa11-c7e5-4f22-a5f2-1c6c53fbe6e9" />

<img width="975" height="216" alt="image" src="https://github.com/user-attachments/assets/c1a509c5-04c7-4e3e-8852-1b88b660a6b3" />

<img width="975" height="402" alt="image" src="https://github.com/user-attachments/assets/4d1a5cb1-8b2c-466b-a886-cb41f9e1b4f6" />

Make sure to add Contributor as a role.

<img width="975" height="288" alt="image" src="https://github.com/user-attachments/assets/62e1d279-0407-465a-93a9-bb618df6f7e1" />


<img width="975" height="406" alt="image" src="https://github.com/user-attachments/assets/8fd146ad-894d-4c82-9738-6c30cfc9aef7" />

<img width="975" height="437" alt="image" src="https://github.com/user-attachments/assets/70d718e7-1584-49d5-89ba-740d06a004b1" />

Make sure to save your logic app design

**Test the Playbook**

I will use the previous generated incident to run the playbook manually

<img width="975" height="294" alt="image" src="https://github.com/user-attachments/assets/dcc526b7-94f5-43d6-bf81-ed3d7ec77667" />

We will run into an error, because MS Sentinel doesn’t give access to the resource group for running the playbook by default. So, we need to give access to the resource group for running the playbook.

<img width="975" height="448" alt="image" src="https://github.com/user-attachments/assets/784f9702-e80d-42ae-b197-f668a38f00cd" />

<img width="569" height="889" alt="image" src="https://github.com/user-attachments/assets/b26a5dad-336a-4a04-adf8-0ecd75c4f722" />

Now we can run the playbook without error.

<img width="975" height="471" alt="image" src="https://github.com/user-attachments/assets/ed6d9f08-f6c0-409a-8406-758f7b93c6f4" />

<img width="838" height="569" alt="image" src="https://github.com/user-attachments/assets/ade3a21c-93a9-457e-90af-3a71461eaa07" />

<img width="975" height="247" alt="image" src="https://github.com/user-attachments/assets/f98a35c1-dfe1-4d49-b021-2812df123426" />

