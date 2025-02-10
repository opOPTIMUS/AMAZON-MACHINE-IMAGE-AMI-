# AMAZON-MACHINE-IMAGE-AMI-
To create an Amazon Machine Image (AMI) on AWS and set up simple web hosting with Apache (httpd), follow these step-by-step instructions:

### Step 1: Create an EC2 Instance (Named `amalinux`)

1. **Login to AWS Console:**
   - Go to the [AWS Management Console](https://aws.amazon.com/console/).

2. **Launch an EC2 Instance:**
   - Navigate to **EC2** under the "Compute" section.
   - Click **Launch Instance** to create a new instance.
   - Choose an **Amazon Linux 2 AMI**.
   - Select an **Instance Type** (e.g., `t2.micro` for testing purposes).
   - Configure the **Instance Details** (use defaults or adjust according to your need).
   - Add **Storage** (default is fine for a basic setup).
   - Configure the **Security Group**:
     - Ensure that **HTTP (port 80)** is allowed for public access.
     - Allow **SSH (port 22)** for SSH access.
   - Launch the instance and select or create a **key pair** to use for SSH access.

3. **Get the Public IP:**
   - Once the instance is running, note down the **public IP** of the instance from the EC2 dashboard.

### Step 2: Access the EC2 Instance via SSH Using Termius

1. **Open Termius** (or any SSH client of your choice).
2. **Create a new SSH connection** using the following details:
   - **Host**: Enter the public IP of the EC2 instance.
   - **User**: Use `ec2-user` (for Amazon Linux AMIs).
   - **Private Key**: Use the `.pem` private key you downloaded when creating the instance.
3. **Connect** to the instance.

### Step 3: Set Up a Simple Web Hosting with Apache (`httpd`)

1. Once logged in via SSH, update the instance:
   ```bash
   sudo yum update -y
   ```

2. **Install Apache (`httpd`):**
   ```bash
   sudo yum install -y httpd
   ```

3. **Start Apache service** and enable it to start on boot:
   ```bash
   sudo systemctl start httpd
   sudo systemctl enable httpd
   ```

4. **Verify Apache is running:**
   - Open your browser and enter the **public IP** of your instance.
   - You should see the Apache default web page.

5. **Optional: Create a simple HTML page:**
   - Navigate to the web root directory:
     ```bash
     cd /var/www/html
     ```
   - Create an `index.html` file:
     ```bash
     echo "Hi, I'm Chitti the Robot. Speed 1 terahertz, memory 1 zigabyte" > index.html
     ```

6. **Verify** by refreshing the public IP in your browser again to see your custom page.

### Step 4: Create an AMI from the Running Instance

1. In the **EC2 Console**, go to the **Instances** section.
2. Right-click on the instance you created (named `amalinux`) and choose **Create Image**.
3. Fill in the **AMI name** (e.g., `amalinux-ami-image`) and other options.
4. Click **Create Image**.
   - AWS will create an image of your instance. This process may take several minutes.

### Step 5: Launch a New Instance from the AMI

1. Once the AMI is created, go to the **AMIs** section in the EC2 dashboard.
2. Select the AMI you just created (e.g., `amalinux-ami-image`).
3. Click **Launch** to create a new EC2 instance using this AMI.
   - Follow the same steps as before to configure the instance.
4. **Note** the **public IP** of the new instance (`amalinuxamiimage`).

### Step 6: Verify the Web Hosting on the New Instance

1. Open your browser and enter the **public IP** of the new instance (`amalinuxamiimage`).
2. You should see the same web page (i.e., "Hello from EC2!") that was set up earlier, confirming that the AMI was successfully created and launched.

---

### Summary:
1. Launch EC2 instance (`amalinux`), set up Apache (`httpd`), and create a simple HTML page.
2. Create an AMI from the running instance.
3. Launch a new instance (`amalinuxamiimage`) from the AMI and verify the web hosting by accessing it via the public IP.

This process will confirm that the simple web hosting setup has been successfully replicated on the new instance.
