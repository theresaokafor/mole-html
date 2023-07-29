# Task 1: Hosting HTML Website on EC2 Instance

This README file provides step-by-step instructions for hosting an HTML website on an EC2 instance using the provided script and resources.

## Steps to Host the Website (Task 1)

1. **Download Web File**: First, download the web file from the provided link:
   - [Download Web File](https://drive.google.com/file/d/15ql0ixVoZ0nILDAXYrodPpTKiHZRpK7U/view?usp=sharing)

2. **Create S3 Bucket**: Go to the AWS Management Console and create an S3 bucket with the name `tess-assigment1`.

3. **Upload Web File to S3 Bucket**: Upload the downloaded web file into the S3 bucket `tess-assigment1` that you created in the previous step.

4. **Create Script to Host the Website on EC2**:

   Create a script (e.g., `host_website.sh`) with the following content:

   ```bash
   #!/bin/bash
   sudo su
   yum update -y
   yum install -y httpd
   cd /var/www/html
   aws s3 ls
   aws s3 ls s3://tess-assigment1
   aws s3 cp s3://tess-assigment1/mole.zip .
   unzip mole.zip
   cp -r mole-main/* /var/www/html/
   rm -rf mole-main mole.zip
   systemctl enable httpd
   systemctl start httpd
   ```

   Save the script and make it executable: `chmod +x host_website.sh`.

5. **Create Security Group for the EC2 Instance**:

   In the AWS Management Console, navigate to the EC2 dashboard, and create a new security group. Allow inbound traffic for ports 22 (SSH) and 80 (HTTP).

6. **Create a Key Pair**:

   In the EC2 dashboard, create a new key pair. This will be used to connect to the EC2 instance securely.

7. **Create a Role using IAM**:

   In the IAM (Identity and Access Management) console, create a new IAM role. Attach the AmazonS3FullAccess policy to the role. This will allow the EC2 instance to access the S3 bucket.

8. **Launch an EC2 Instance**:

   - In the EC2 dashboard, click on "Launch Instance."
   - Choose an Amazon Machine Image (AMI) with your preferred operating system.
   - Select an instance type (e.g., t2.micro).
   - Configure the instance details using the default VPC.
   - In the "Add User Data" section, paste the contents of the script `host_website.sh` created earlier.
   - Choose the security group created in Step 5.
   - Select the key pair created in Step 6.
   - In the "Configure Instance Details," add the IAM role created in Step 7 to the instance.
   - Launch the instance.

9. **Copy Public IPv4 DNS**:

   Once the instance is up and running, go to the EC2 dashboard, find your instance, and copy its public IPv4 DNS. Paste the DNS into your web browser to check that the website is hosted successfully.

**Note**: Ensure that the appropriate AWS CLI and SDK configurations are set up on the EC2 instance to access the S3 bucket.

## Conclusion

Following the above steps, you should have successfully hosted the HTML website on an EC2 instance using the provided script and resources. If you encounter any issues, please review the steps or refer to the AWS documentation for further assistance.

Please feel free to reach out if you have any questions or need further support. Happy hosting!




# Task 2: Hosting HTML Website on EC2 Instance from GitHub

This README file provides step-by-step instructions for hosting an HTML website on an EC2 instance using a script and GitHub repository.

## Steps to Host the Website (Task 2)

1. **Download Web File**: First, download the web file from the provided link.

2. **Create a Public GitHub Repo**:

   - Go to GitHub (https://github.com) and create a new public repository with an appropriate name (e.g., "mole-html").
   - Leave the repository empty for now, as we will upload the web file from your local project repository.

3. **Upload Web File to GitHub Repo**:

   Open your terminal or command prompt and navigate to your local project repository ("assignment1") that contains the web file to be uploaded. Use the following commands:

   ```bash
   cd assignment1
   git init
   git add .
   git status
   git commit -m "first commit"
   git remote add origin https://github.com/theresaokafor/mole-html.git
   git push -u origin master
   ```

   This will initialize your local repository, add the files, commit the changes, and push them to the GitHub repository you created in Step 2.

4. **Create Script to Host the Website on EC2**:

   Create a script (e.g., `host_website.sh`) with the following content:

   ```bash
   #!/bin/bash
   sudo su
   yum update -y
   yum install -y httpd
   cd /var/www/html
   wget https://github.com/theresaokafor/mole-html/archive/refs/heads/master.zip
   unzip master.zip
   cd mole-html-master/
   unzip mole.zip
   cp -r mole-main/* /var/www/html/
   rm -rf mole-html-master master.zip
   systemctl enable httpd
   systemctl start httpd
   ```

   Save the script and make it executable: `chmod +x host_website.sh`.

5. **Create Security Group for the EC2 Instance**:

   In the AWS Management Console, navigate to the EC2 dashboard, and create a new security group. Allow inbound traffic for ports 22 (SSH) and 80 (HTTP).

6. **Create a Key Pair**:

   In the EC2 dashboard, create a new key pair. This will be used to connect to the EC2 instance securely.

7. **Launch an EC2 Instance**:

   - In the EC2 dashboard, click on "Launch Instance."
   - Choose an Amazon Machine Image (AMI) with your preferred operating system.
   - Select an instance type (e.g., t2.micro).
   - Configure the instance details using the default VPC.
   - In the "Add User Data" section, paste the contents of the script `host_website.sh` created earlier.
   - Choose the security group created in Step 5.
   - Select the key pair created in Step 6.
   - Launch the instance.

8. **Copy Public IPv4 DNS**:

   Once the instance is up and running, go to the EC2 dashboard, find your instance, and copy its public IPv4 DNS. Paste the DNS into your web browser to check that the website is hosted successfully.

**Note**: Ensure that the appropriate AWS CLI and SDK configurations are set up on the EC2 instance to access the GitHub repository.

## Conclusion

Following the above steps, you should have successfully hosted the HTML website on an EC2 instance using the provided script and GitHub repository. If you encounter any issues, please review the steps or refer to the AWS documentation for further assistance.

Please feel free to reach out if you have any questions or need further support. Happy hosting!
