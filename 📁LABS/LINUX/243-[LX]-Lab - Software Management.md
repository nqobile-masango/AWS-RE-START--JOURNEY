### Software Management

### Objectives
In this lab, you will:
- Update the Linux machine using the package manager
- Roll back or downgrade a previously updated package through the package manager
- Install the AWS Command Line Interface (AWS CLI)
### Accessung the AWS  Management Console
- Click Start Lab to launch the environment.
- Wait until status shows Lab status: ready, then close the panel.
- Click AWS to open the AWS Management Console in a new tab (auto login).
- If blocked, allow pop‑ups in your browser.
- Keep the Console tab side‑by‑side with instructions for easier navigation.

- ### 🪟WINDOWS
- Windows SSH connection steps:  
1. Open `Details → Show` to access credentials.  
2. Download and save the `labsuser.ppk` file (usually in Downloads).  
3. Note the `PublicIP address` shown in the panel.  
4. Close the Details panel (X).  
5. Install and open `PuTTY` if not already installed.  
6. Configure PuTTY using the provided guide to connect to your Linux instance.
### MAC'OS🍏LINUX 🐧USERS
8.  macOS/Linux SSH connection steps:
1. Open Details → Show to access credentials.
2. Download and save the `labsuser.pem` file.
3. Note the `PublicIP address` shown.
4. Close the Details panel (X).
5. In terminal, go to the download directory: `cd ~/Downloads`
6. Set key permissions: chmod 400 labsuser.pem.
7. Connect with SSH: `ssh -i labsuser.pem ec2-user@<public-ip>*` → type yes when prompted (no password needed).'
###  Task 2: Update Linux Machine

1. Check current folder: `pwd`  
2. If not in **companyA**, run: `cd companyA`  
3. Query updates: `sudo yum -y check-update`  
4. Apply security fixes: `sudo yum update --security`  
5. Upgrade all packages: `sudo yum -y upgrade`  
6. System confirms when up to date (still good practice if already current).  
7. Optional: install Apache for practice → `sudo yum install httpd -y`  
8. This also shows update history and installed packages.
### Task 3: Roll back a package
1. Confirm you’re in the **companyA** folder with `pwd`.  
2. View update history: `sudo yum history list` and note the transaction ID.  
3. Check details of that update: `sudo yum history info <ID>`.  
4. Roll back changes: `sudo yum -y history undo <ID>`.  
5. The system reverts to the previous state, showing packages as dep‑install.
### Task 4 (Install AWS CLI on Red Hat Linux)
1. Make sure you have the right permissions (`sudo` if not root).
2. Check Python installation: `python3 --version`.
3. Ensure Python version `≥ 2.6.5 (Py2) or ≥ 3.3 (Py3)`.
4. Verify pip installation: `pip3 --version`.
- `If pip is missing, install it (needed for AWS CLI)`.
5. Download AWS CLI installer:
**bash**
`curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip`
6. Unzip the package: `unzip awscliv2.zip`.
7. Run installer: `sudo ./aws/install`.
Test installation: `aws help` (press `q `to exit).
8. From `Details` → `Show`, copy your AWS credentials (`Access Key` + Secret Key`) for the next task.
### Task 5: Configure AwS CLI
1. Run `aws configure` in your terminal.  
2. Leave `Access Key ID` and `Secret Access Key` blank.  
3. Enter `us-west-2` as the default region.  
4. Enter  `json` as the default output format.  
5. AWS automatically creates credential files.  
6. Open credentials file: `sudo nano ~/.aws/credentials`.  
7. Paste in keys from Task 4 (`aws_access_key_id`, `aws_secret_access_key`, `aws_session_token`).  
8. Save (`ctrl + O`) and exit (`ctrl + X`).  
9. In AWS Console → EC2 → Instances, copy the `Command Host Instance ID`.  
10. Verify connection with:  
 `bash`
`aws ec2 describe-instance-attribute --instance-id <your-id> --attribute instanceType`
   → Output confirms instance type (e.g., `t3.micro`).
### Windows SSH connection 
<img width="452" height="442" alt="Screenshot 2025-11-24 133805" src="https://github.com/user-attachments/assets/6344b501-4a2b-428b-8783-c9f5f47813c2" />

### Update your Linux machine using the yum package manager to update and upgrade the machine including relevant security packages
<img width="1280" height="976" alt="Screenshot 2025-11-24 134410" src="https://github.com/user-attachments/assets/faad4c2d-ff28-431f-a676-b3d675cadd45" />
 This command install httpd will show a listof all previous updates and current packages on the instance.
<img width="1280" height="976" alt="Screenshot 2025-11-24 135734" src="https://github.com/user-attachments/assets/a8723741-e61e-4e7e-83d2-66770c9c3050" />



    
