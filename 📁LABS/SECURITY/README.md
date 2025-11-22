###  Security Lab: Monitor an EC2 Instance
### Objective
- Create an Amazon SNS notification,
- congifure a cloudwatch alarm, 
- stress test an EC2 instance, 
- confirm that an Amazon SNS email was sent and create cloudwatch dashboard
### Tasks
### Conifgure Amazon SNS
- I created a SNS topic to send alerts and subscribed my email to it.
-  This way if something happens in AWS, the system can send me a message automatically.
### Create cloudwatch alarm 
- I made a CloudWatch alarm to watch the CPU usage of the EC2 instance.
-  If the CPU went above 60%, the alarm would trigger and send an email through the SNS topic.
### Test the cloudwatch alarm
 - I ran a stress on the EC2 to make the CPU go over 60%. I saw the alarm change to "In Alarm" in CLoudWatch and got the email alert.
 - This showed that what I did worked.
### Create a cloudwatch dashboard
- I created a dashboard in CloudWatch to see the CPU usage of the EC2 instance in real time.
-  This makes it easy to monitor the instance without checking manually.
### Challenges
- One challenge was that the CPU took time to go over 60%, so I could not receive the email notification during the test.
  ### Takeaways
- I learned how to set up Amazon SNS for notifications,
- Create and test Cloudwatch alarms
- Build a CloudWatch dashboard to monitor EC2 metrics.

Screenshots
