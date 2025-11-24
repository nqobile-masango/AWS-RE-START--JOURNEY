
### Introduction to an Amazon Linux Amazon Machine Image (AMI)
- This lab is designed to reinforce your knowledge of the basic command line interface functionality and provide a solid foundation from which you can continue to learn about new commands and capabilities within the Linux shell. 

### Scenario
- In this lab, you use Secure Shell (SSH) to access an Amazon Linux Amazon Machine Image (AMI) within Vocareum labs.
- Next you use the man command to access the man pages.

### Objectives
- After completing this lab, you will be able to:

- Use SSH to access an Amazon Linux AMI within Vocareum labs.
- Understand the purpose of the man command.
- Demonstrate the search feature of the man pages.
- Examine man page headers.
  
### The following components are created for you as a part of the lab environment:

### Amazon EC2 - Command Host (in the public subnet):
- You log in to this instance to use the commands listed within this lab.

### Public subnet
Amazon Virtual Private Cloud (Amazon VPC)

### Accessing the AWS Management Console
### 1. Click “Start Lab”.
- At the top of your lab page.
 ### 2. Wait for “Lab status: ready.
- The system needs a few seconds to create your temporary environment.
  ### 3. Open the AWS Console
- At the top of the instructions, click the AWS button.
- A new browser tab will open automatically.
### 4. Arrange your windows
- To make the lab easier:
- Keep the instructions open on one side.
- Keep the AWS Console open on the other.
- This makes it easy to follow each step without switching tabs repeatedly.

### Task 1: Use SSH to connect to an Amazon Linux EC2 instance.
### WINDOWS USERS
1. Open the **Details** panel and **download the `.ppk` key file**.
2. **Note the EC2 Public IP address**.
3. Install and open **PuTTY**.
4. In PuTTY, enter `ec2-user@<Public-IP>` and load the **.ppk key** under *SSH → Auth*.
5. Click **Open** to connect to the Amazon Linux EC2 instance.
### MAC'OS  and LINUX  USERS
- Mac/Linux Users – SSH to EC2 Instance:
1. Open Terminal on your Mac or Linux system.
2. Download the private key file .(`labuser.pem`)
3. Change file permission (to secure the key):
- `chmod 400 labuser.pem`
4. Get the EC2 public IP address from the lab/console.
5. SSH into the instance using:
-` ssh -i labuser.pem ec2-user@<public-ip-address>`
5. Replace `<public-ip-address>` with the actual IP.
- This authenticates you as ec2-user using the provided key file.
- Type `yes` when prompted to allow the first connection to this remote SSH server.
Because you are using a key pair for authentication.

### Task 2: Exercise - Explore the Linux Man Pages
### 1. Open the Manual Pages:
- In your PuTTY terminal window, type the following command and press Enter:Code `man` `man`
### 2. Viewing the Man Page:
-The terminal will display the man page for the man command. This page contains useful information about how to use man, including its options and functionalities.
### 3.Identify Major Sections:
- As you scroll through the man page, look for the following important headers:
- NAME: The name of the command and a brief description.
- SYNOPSIS: A summary of how to use the command, including syntax.
 - DESCRIPTION: A detailed explanation of what the command does.
- OVERVIEW: General information about the command.
- EXAMPLES: Practical examples of how to use the command.
- FILES: Information about files associated with the command.
- OPTIONS: A list of command-line options you can use with the command.
- SEE ALSO: References to related commands or documentation.
### 4. Navigation:
- Move through the man page using the ↑ (up) and ↓ (down) arrow keys.
- If you need to scroll faster, you can use Page Up and Page Down keys.
### 5. Examining the DESCRIPTION Header:
- Pay particular attention to the DESCRIPTION section, which provides an overview of the man command and outlines its functionality. 
- Look for section numbers, which indicate where you can find specific information about the command.
### . Exiting the Man Pages:
- To exit the man page and return to the command prompt, simply press the q key.
- ### SCREENSHOTS
- <img width="580" height="522" alt="Screenshot 2025-11-22 140620 111" src="https://github.com/user-attachments/assets/978c8c83-fbfe-4a31-8317-33fbea090de2" />

- <img width="567" height="546" alt="Screenshot 2025-11-22 135105" src="https://github.com/user-attachments/assets/298fc38b-459b-44a1-bf7e-7fa09855426f" />

<img width="739" height="590" alt="Screenshot 2025-11-22 135453" src="https://github.com/user-attachments/assets/2d2002df-4a35-4c4f-9f3b-93267b13ddf1" />

<img width="612" height="673" alt="Screenshot 2025-11-22 135729 2" src="https://github.com/user-attachments/assets/1ed82757-c005-4a0e-ad04-411762af2a0e" />



