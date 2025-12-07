## Working with AWS Lambda
# Lab overview

In this lab, you set up a serverless system using AWS Lambda. The Lambda function creates a daily sales report by doing the following:
1. Gets database login details from AWS Systems Manager Parameter Store.
2. Connects to a MySQL database that is running on an EC2 LAMP server.
3. Pulls sales data from the database.
4. Generates a report based on the data.
5. Emails the report automatically every day.

The architecture diagram shows how all these steps happen in order, from storing configuration parameters → running the Lambda function → connecting to the database → sending the email.
<img width="773" height="415" alt="lab-2 (1)" src="https://github.com/user-attachments/assets/ca4e1506-a8ff-477b-aff9-367addb65967" />

Explaining the diagram:

| **Step** | **What Happens**                                                                                                  | **Simple Explanation**                                                           |
| -------- | ----------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| **1**    | A CloudWatch Events rule triggers the salesAnalysisReport Lambda function every day at 8 PM (Monday–Saturday).  | CloudWatch automatically starts the main Lambda function at the scheduled time.  |
| **2**    | The salesAnalysisReport Lambda function calls another Lambda function named salesAnalysisReportDataExtractor. | The main function asks a second function to fetch the data it needs.             |
| **3**    | The salesAnalysisReportDataExtractor function runs an analytical query on the cafe_db database.               | The second function connects to the database and runs a query to get sales data. |
| **4**    | The query results are sent back to the salesAnalysisReport function.                                            | The database results are returned to the main function.                          |
| **5**    | The salesAnalysisReport function formats the report and sends it to the salesAnalysisReportTopic SNS topic.   | The main function creates a readable report and sends it to SNS.                 |
| **6**    | The salesAnalysisReportTopic SNS topic delivers the report by email to the administrator.                       | SNS emails the final report to the admin.                                        |
# Objectives
After completing this lab, I will be able to do the following:
- Recognize necessary AWS Identity and Access Management (IAM) policy permissions to facilitate a Lambda function to other Amazon Web Services (AWS) resources.
- Create a Lambda layer to satisfy an external library dependency.
- Create Lambda functions that extract data from database, and send reports to user.
- Deploy and test a Lambda function that is initiated based on a schedule and that invokes another function.
- Use CloudWatch logs to troubleshoot any issues running a Lambda function.

 # Challanges 
This was by far the biggest and most head-throbbing lab I’ve had to do out of all my labs. My main issue was with testing and saving. At first, I kept getting an “Execution result: failed” error, which, according to the lab, shouldn’t have happened. I had to fix it, and that’s when everything started to feel really messy and frustrating.

I had created multiple Inbound rules for port 3306 as required by the lab, but the tests still kept failing. Finally, I went to the Configuration tab, chose VPC, and checked the Inbound rules of the EC2 security group to ensure that port 3306 was allowed. When I added the missing rule, I returned to the salesAnalysisReportDataExtractor Lambda function, went to the Test tab, and ran the test again.

This time, everything worked, and I saw the green message: “Execution result: succeeded (logs)”, which meant the function ran successfully.
# Task 1: Observing the IAM role settings
     Task 1.1: Observing the salesAnalysisReport IAM role settings
I go to IAM in the AWS Console and open the role called salesAnalysisReportRole.

When I check the Trust relationships, I see that Lambda is trusted.
This means Lambda is allowed to use this role.

In the Permissions tab, I see four policies attached:
- **AmazonSNSFullAccess** – allows me to use SNS completely.
- **AmazonSSMReadOnlyAccess** – allows me to read values from Parameter Store.
- **AWSLambdaBasicRunRole** – allows my Lambda function to write logs to CloudWatch.
- **AWSLambdaRole** – allows one Lambda function to call another.

Later in the lab, I will use this role for the salesAnalysisReport Lambda function.

    Task 1.2: Observing the salesAnalysisReportDERole IAM role settings

I go back to the Roles page in IAM and search for sales again.

From the results, I open the salesAnalysisReportDERole role.

In the Trust relationships tab, I see that lambda.amazonaws.com is trusted, which means Lambda can use this role.

In the Permissions tab, I see two policies:
- **AWSLambdaBasicRunRole** – lets my Lambda function write logs to CloudWatch.
- **AWSLambdaVPCAccessRunRole** – allows my function to create and manage network interfaces so it can connect to a VPC.

This role will be used by the salesAnalysisReportDataExtractor Lambda function that I create next.
# Task 2: Creating a Lambda layer and a data extractor Lambda function
First things first to start this lab you need to dowload the following ZIP folders 
________________________________________________________________
pymysql-v3.zip

salesAnalysisReportDataExtractor-v3.zip
_________________________________________________________________

      Task 2.1: Creating a Lambda Layer

I go to AWS Lambda in the console and open the Layers section.

I choose Create layer and fill in the details:
- I name the layer pymysqlLibrary.
- I add the description PyMySQL library modules.
- I upload the pymysql-v3.zip file.
- I select Python 3.9 as the compatible runtime.
  
  <img width="1336" height="498" alt="lab-2 (3)" src="https://github.com/user-attachments/assets/54c56634-9d05-459a-bfd0-4b3654595934" />

- Then I choose Create to finish making the layer.

           Task 2.2: Creating a data extractor Lambda function
  
I go to the Functions page in AWS Lambda and choose Create function.
- I select Author from scratch.
- I name the function salesAnalysisReportDataExtractor.
- I choose Python 3.9 as the runtime.
- In Change default execution role, I select Use an existing role.
- I pick the salesAnalysisReportDERole as the existing role.
<img width="1350" height="513" alt="lab-2 (5)" src="https://github.com/user-attachments/assets/c824dbdf-325e-4f84-b214-94cb91eb6e5f" />

Then I choose Create function.

                Task 2.3: Adding the Lambda layer to the function

In my Lambda function page, I go to the Function overview section and choose Layers.
- At the bottom, I select Add a layer.
- On the Add layer page:
- I choose Custom layers.
- I select pymysqlLibrary.
- I choose Version 1.
  
<img width="1366" height="499" alt="lab-2 (8)" src="https://github.com/user-attachments/assets/d9228758-1162-4706-8b6c-9f53f68eb8fe" />

Then I choose Add to attach the layer to my function.

              Task 2.4: Importing the code for the data extractor Lambda function

I open my salesAnalysisReportDataExtractor Lambda function.
- In Runtime settings, I choose Edit and change the handler to salesAnalysisReportDataExtractor.lambda_handler, then I save it.
- In the Code source section, I choose Upload from, select .zip file, and upload the salesAnalysisReportDataExtractor-v3.zip file I downloaded earlier.
<img width="1326" height="291" alt="lab-2 (12)" src="https://github.com/user-attachments/assets/0bf49991-6cd8-4874-a95b-7665bd888e0f" />
<img width="820" height="378" alt="lab-2 (13)" src="https://github.com/user-attachments/assets/03357b3a-baf9-41d0-a3dc-dff13d675c74" />

  Finally, I choose Save.             

          Task 2.5: Configuring network settings for the function

I go to the Configuration tab of my Lambda function and choose VPC.

Then I select Edit and set the following:
- For VPC, I pick the one named Cafe VPC.

For Subnets, I choose Cafe Public Subnet 1.
(I ignore the warning about needing two subnets.)

For Security groups, I choose CafeSecurityGroup and see its inbound and outbound rules appear.

<img width="1350" height="516" alt="lab-2 (14)" src="https://github.com/user-attachments/assets/327f1ea5-d31d-4da2-b24a-6713dceec258" />

After that, I choose Save.

# Task 3: Testing the data extractor Lambda function
    Task 3.1: Launching a test of the Lambda function

 I open AWS Systems Manager in a new browser tab and go to Parameter Store.

I open each parameter and copy its Value into a text editor:

`/cafe/dbUrl`

`/cafe/dbName`

`/cafe/dbUser`

`/cafe/dbPassword`

Then I return to my salesAnalysisReportDataExtractor Lambda function in the Lambda console and go to the Test tab.

- I select Create new event.

- I name the event SARDETestEvent.

- I choose the hello-world template.

- I replace the JSON in the Event JSON pane with the new JSON object I need for testing.
- I ran the following code for testing
  
 {

  "dbUrl": "<value of /cafe/dbUrl parameter>",
  
  "dbName": "<value of /cafe/dbName parameter>",
  
  "dbUser": "<value of /cafe/dbUser parameter>",
  
  "dbPassword": "<value of /cafe/dbPassword parameter>"
  
}
   
    Task 3.3: Analyzing and correcting the Lambda function

Then i will save and test. After some time the page showed a "Execution result: failed" error i did not give in to much worry to it , i simply went to the Configuration tab and choose VPC to check the Inbound rules of the EC2 security group to see if port 3306 is allowed. If not, I add a rule to allow it. After fixing the security group, I return to the salesAnalysisReportDataExtractor Lambda function, go to the Test tab, and run the test again. If everything is correct, I see a green message: “Execution result: succeeded (logs)”, which means the function ran successfully.

         Task 3.4: Placing an order and testing again
To open the café website, I first find the public IP address of the café EC2 instance. There are two ways to do this:

**Option 1:**
- I go to EC2 in the AWS Console, select CafeInstance, and copy the Public IPv4 address.

- In a new browser tab, I enter http://publicIP/cafe, replacing publicIP with the address I copied, and press Enter to load the website.

**Option 2:**
- I click Details at the top of the instructions, then Show, and copy CafePublicIP.
- I open a new browser tab, enter http://publicIP/cafe with the copied IP, and press Enter.
- On the café website, I go to Menu and place some orders to add data to the database.
- After populating the database, I return to the salesAnalysisReportDataExtractor Lambda function, go to the Test tab, and run Test again.

Any option work, however i choose Option 2

# Task 4: Configuring notifications
   Task 4.1: Creating an SNS topic

I go to Simple Notification Service (SNS) in the AWS Console and choose Topics, then Create topic.

I select Standard for the type.

I enter salesAnalysisReportTopic as the name.

I enter SARTopic as the display name.

I choose Create topic.

Finally, I copy the ARN of the topic into a text editor for later use.
<img width="1366" height="432" alt="lab-2 (19)" src="https://github.com/user-attachments/assets/d2fd0514-2872-4ba9-a154-6b974f634e47" />
    Task 4.2: Subscribing to the SNS topic

I choose Create subscription in SNS and set the following:

Protocol: Email

Endpoint: My email address

I choose Create subscription. The subscription shows as Pending confirmation.

I check my email inbox and find a message from SARTopic with the subject "AWS Notification - Subscription Confirmation."

I open the email and click Confirm subscription. A new browser tab opens showing "Subscription confirmed!"
<img width="913" height="377" alt="lab-2 (21)" src="https://github.com/user-attachments/assets/e0ea3334-45a1-4438-983f-b6c56d02194b" /> <img width="780" height="288" alt="lab-2 (22)" src="https://github.com/user-attachments/assets/6b6918c3-58c2-4422-80b0-158c7a082c99" /> <img width="791" height="264" alt="lab-2 (23)" src="https://github.com/user-attachments/assets/2c3c1007-c9c5-4404-874a-9fee6b30224c" />

# Task 5: Creating the salesAnalysisReport Lambda function

Here’s a concise, step-by-step summary of all the tasks you described, in **simple English and first person**:

---

### **AWS Lambda Sales Analysis Report Lab – Summary**

1. **Connect to the CLI Host EC2 instance**

   * I select the CLI Host instance and use **EC2 Instance Connect**.

2. **Configure the AWS CLI**
-  I run `aws configure` and enter:
- **AWS Access Key ID** and **Secret Access Key** from the Credentials window.
- **Region:** `us-west-2`
- **Output format:** `json`

3. **Create the salesAnalysisReport Lambda function via CLI**
- I verify that the `salesAnalysisReport-v2.zip` file is on the CLI host.
- I retrieve the **ARN** of the `salesAnalysisReportRole`.
- I run `aws lambda create-function` with the zip file, Python 3.9 runtime, handler, region, and role ARN.

4. **Configure the salesAnalysisReport Lambda function**
- I open the function in the Lambda console.
- I add an **environment variable**:
- **Key:** `topicARN`
- **Value:** ARN of the `salesAnalysisReportTopic` SNS topic

5. **Test the salesAnalysisReport Lambda function**
- I create a **test event** named `SARTestEvent` using the hello-world template.
- I run **Test** and verify the green message: `Execution result: succeeded (logs)`.
- If needed, I adjust the **timeout** in Configuration → General configuration.
- I check my **email inbox** for the report.

6. **Add a trigger for scheduled execution**

I choose **Add trigger → EventBridge (CloudWatch Events)**.
   
I create a new rule:

- **Rule name:** `salesAnalysisReportDailyTrigger`
- **Description:** Initiates report generation daily
- **Schedule expression:** Cron expression for Monday–Saturday at the desired UTC time (e.g., `cron(35 11 ? * MON-SAT *)` for 11:35 UTC).
- I add the trigger and verify that the function runs at the scheduled time.

7. **Check results**
- I confirm that I receive the **daily sales analysis report** by email.
- I can place more orders on the café website to see updates in the report.
<img width="693" height="380" alt="lab-2 (24)" src="https://github.com/user-attachments/assets/cd639412-9e8f-4d6f-8011-06553e4d959b" />
<img width="412" height="54" alt="lab-2 (25)" src="https://github.com/user-attachments/assets/ff571aa8-04b6-481a-bf4f-0369a709ad1b" />
<img width="1360" height="406" alt="lab-2 (26)" src="https://github.com/user-attachments/assets/c1b49ea7-bff4-487a-95d2-4c1b75d4c8bc" />
<img width="1366" height="728" alt="Screenshot 2025-12-03 135234" src="https://github.com/user-attachments/assets/8e2b9adc-cff2-42e8-b7ff-a6512eb2eeb8" />


# **Take aways**

* Learned which **IAM policies** a Lambda function needs to access other AWS resources.
* Created a **Lambda layer** for external library dependencies.
* Built **Lambda functions** to extract data and send reports.
* Scheduled a Lambda function to run automatically using **CloudWatch Events**.
* Used **CloudWatch logs** to troubleshoot and confirm successful execution.
