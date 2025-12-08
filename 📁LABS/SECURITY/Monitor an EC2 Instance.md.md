# Monitor an EC2 Instance
## Lab overview
Logging records system events so you can see detailed activity, while monitoring analyzes that data to track performance and detect issues. In this lab, I create a CloudWatch alarm that triggers when an EC2 instance’s CPU goes above a set level, and I set up an SNS subscription to email me when the alarm activates. I then run a stress test on the instance to push its CPU usage to 100%.
## Challanges
The only challange I encounted was creating a tag for a Restore volume. The tag was succesfully created but it could not be dispalyed and the next step wanted me to implicate an Action to attach a volume. I created 3 tags and still couln`t show even though i reloaded. I went to Instances to check if are they running, when i came back i saw the Restore volume and was able to properly configure the required step.
## Objectives
After completing this lab, you should be able to:
  
  - Create an Amazon SNS notification
  - Configure a CloudWatch alarm
  - Stress test an EC2 instance
  - Confirm that an Amazon SNS email was sent
  - Create a CloudWatch dashboard
 ## Task 1: Configure Amazon SNS
 I search for SNS in the console, open Simple Notification Service, go to Topics, and choose Create topic.

On the Create topic page in the Details section, configure the following options:
- Type: Choose Standard.
- Name: Enter MyCwAlarm 

 The configurations should look like the following image:

<img width="889" height="543" alt="lab-1 (1)" src="https://github.com/user-attachments/assets/4d1055b4-0c80-4354-acb5-0ed4598f6a3a" />
Choose Create topic.

<img width="1046" height="338" alt="lab-1 (2)" src="https://github.com/user-attachments/assets/aaf7bb5b-1425-4918-aabf-74e1d895da55" />

On the MyCwAlarm details page, choose the Subscriptions tab, and then choose Create subscription.

On the Create subscription page in the Details section, configure the following options:
- Topic ARN: Leave the default option selected.
- Protocol: From the dropdown list, choose Email.
- Endpoint: Enter a valid email address that you can access.

  The configurations should look like the following image:
  <img width="1306" height="454" alt="lab-1 (3)" src="https://github.com/user-attachments/assets/08057295-c7e2-4fc2-8166-0c39abe660f5" />
  Choose Create subscription.

I open the SNS confirmation email to confirm the subscription, then return to the console and see that the subscription status has changed from Pending confirmation to Confirmed.

<img width="1070" height="453" alt="lab-1 (4)" src="https://github.com/user-attachments/assets/3ef91b4c-41e8-44ad-a219-603ab9952923" />

<img width="1035" height="452" alt="lab-1 (5)" src="https://github.com/user-attachments/assets/a04f60e5-aa50-4d8a-92ba-2662e672450f" />

## Task 2: Create a CloudWatch alarm
I open CloudWatch, go to All Metrics, wait for EC2 metrics to load, then choose Per-Instance Metrics and select the CPUUtilization metric for the Stress Test EC2 instance.

The following image shows the metrics and instance that you should select.
<img width="1366" height="515" alt="lab-1 (7)" src="https://github.com/user-attachments/assets/88ec4d04-998c-451d-a2bd-60409fcf44ad" />

In the left navigation pane, choose the Alarms dropdown list, and then choose All alarms.

Choose Create alarm.

Choose Select metric, choose EC2, and then choose Per-Instance Metrics.

Select the check box with CPUUtilization as the Metric name for the Stress Test instance name.

Choose Select metric.

On the Specify metric and conditions page, configure the following options:
 
 **Metric**
 
- Metric name: Enter CPUUtilization
- InstanceId: Leave the default option selected.
- Statistic: Enter Average
- Period: From the dropdown list, choose 1 minute.

    The configurations should look like the following image:
<img width="1341" height="526" alt="lab-1 (9)" src="https://github.com/user-attachments/assets/d69f338a-e957-403f-b3b9-a70762856381" />


**Conditions**
  
- Threshold type: Choose Static.
- -Whenever CPUUtilization is...:
- Choose Greater > threshold.
- than... Define the threshold value: Enter 60

<img width="1350" height="558" alt="lab-1 (10)" src="https://github.com/user-attachments/assets/e2d4fe0e-edf5-4c54-b6c5-a86292d647a6" />

Choose Next.

On the Configure actions page, configure the following options:

**Notification**
- Alarm state trigger: Choose In alarm.
- Select an SNS topic: Choose Select an existing SNS topic.
- Send a notification to...: Choose the text box, and then choose MyCwAlarm.
  
  <img width="1017" height="504" alt="lab-1 (11)" src="https://github.com/user-attachments/assets/27a0cdb9-4c74-45ff-ab76-7d4c9e3ebb4b" />

Choose Next, and then configure the following options:
- Name and description
- Alarm name: Enter LabCPUUtilizationAlarm
- Alarm description - optional: Enter CloudWatch alarm for Stress Test EC2 instance CPUUtilization
<img width="1048" height="511" alt="lab-1 (12)" src="https://github.com/user-attachments/assets/b92201fa-fc97-4f59-8950-db1366227dc7" />
Choose Next. Review the Preview and create page, and then choose Create alarm.

<img width="1095" height="273" alt="lab-1 (13)" src="https://github.com/user-attachments/assets/990148cb-07fd-4706-907b-ee4f57e454b7" />

## Task 3: Test the Cloudwatch alarm
Navigate to the Vocareum console page, and choose the  AWS Details button.

Next to EC2InstanceURL, there is a link. Copy and paste this link into a new browser tab.

This link connects you to the Stress Test EC2 instance. 

To manually increase the CPU load of the EC2 instance, run the following command:
- sudo stress --cpu 10 -v --timeout 400s
<img width="1366" height="136" alt="lab-1 (14)" src="https://github.com/user-attachments/assets/bd046b0d-341b-4ceb-bd11-b2d092381d5b" />

The output must be the following:
<img width="1348" height="646" alt="lab-1 (15)" src="https://github.com/user-attachments/assets/60576d34-6f4b-46a4-ae44-c722305caaf7" />

I open Vocareum’s AWS Details and use the EC2InstanceURL to open a second terminal for the Stress Test instance in a new browser tab.
In the new terminal, run the following command: top
<img width="1366" height="136" alt="lab-1 (16)" src="https://github.com/user-attachments/assets/280e628e-8c5f-4101-8644-a43d717ba290" />
The output must be the following:
<img width="1330" height="639" alt="lab-1 (17)" src="https://github.com/user-attachments/assets/40ee8078-2853-45bb-ade0-faaaf75b69e2" />
I return to the CloudWatch alarm, refresh until it goes “In alarm,” see the CPU rise above 60%, and then check my email for the SNS notification.
<img width="1089" height="509" alt="lab-1 (18)" src="https://github.com/user-attachments/assets/6b5b3107-1f07-4b66-80fc-69ad29357d2c" />

## Task 4: Create a CloudWatch dashboard
Go to the CloudWatch section in the AWS console. In the left navigation pane, choose Dashboards.

Choose Create dashboard.

For Dashboard name, enter LabEC2Dashboard and then choose Create dashboard.
<img width="1366" height="650" alt="lab-1 (19)" src="https://github.com/user-attachments/assets/516d2cac-3064-4be2-9629-a848ea61435f" />

Choose Line.

Choose Metrics.

Choose EC2, and then choose Per-Instance Metrics.

Select the check box with Stress Test for the Instance name and CPUUtilization for the Metric name.
<img width="1236" height="618" alt="lab-1 (20)" src="https://github.com/user-attachments/assets/ac7fcbe7-9baa-4d38-b8d8-311b145817ba" />

Choose Create widget.

Choose Save dashboard.
<img width="1366" height="255" alt="lab-1 (21)" src="https://github.com/user-attachments/assets/a1445a4d-8cf3-44f3-9565-dce6cdab2e3a" />


Congratulations you`ve sucessfully completed your lab!!
