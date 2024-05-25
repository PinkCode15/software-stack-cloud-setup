# LEMP Stack Setup on AWS EC2 Instance

This guide walks through the process of setting up a LEMP (Linux, Apache, MySQL, PHP) stack on an Amazon EC2 instance running Ubuntu Linux.

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Step 1: Launch EC2 Instance](#step-1-launch-ec2-instance)
3. [Step 2: Connect to Instance](#step-2-connect-to-instance)
4. [Step 3: Install Components](#step-3-install-components)
5. [Step 4: Start Services](#step-4-start-services)
6. [Step 5: Test LEMP Stack](#step-5-test-lemp-stack)

## Prerequisites

- An AWS account with permissions to create EC2 instances.
- Basic familiarity with the AWS Management Console.
- SSH client installed on your local machine.

## Step 1: Launch EC2 Instance

1. Log in to the AWS Management Console.
2. Navigate to the EC2 service.
3. Click on "Launch Instance" and select "Ubuntu Server" as the Amazon Machine Image (AMI).
4. Choose an instance type, configure instance details, add storage, configure security groups, and review and launch the instance. Ensure that the security group allows inbound traffic on ports 22 (SSH) and 80 (HTTP) at least.


## Step 2: Connect to Instance

1. Once the instance is launched, note down its public IP address or DNS name.
2. Open a terminal on your local machine.
3. Use SSH to connect to the EC2 instance using the following command:
   
   ```bash
   ssh -i your_key.pem ubuntu@your_ec2_public_ip

## Step 3: Install Components

1. Update the package index on your EC2 instance by running:

    ```bash
    sudo apt update

2. Install Nginx, MySQL, and PHP packages by running the following command:

    ```bash
    sudo apt install nginx mysql-server php php-fpm php-mysql

## Step 4: Configure Nginx for PHP

1. Find the php version installed

    ```bash
    php -v

2. Open the default Nginx server block configuration file in a text editor:

    ```bash
    sudo nano /etc/nginx/sites-available/default

3. Find the block that starts with location ~ \.php$ { and uncomment and modify it as follows:

    ```bash
    location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass unix:/var/run/php/php8.3-fpm.sock;
    }

    If you are using a different version of PHP, adjust the version number accordingly.
    Save and close the file

## Step 5: Start Services

1. Enable Apache web server to start on boot by running:

    ```bash
    sudo systemctl enable nginx

2. Enable MySQL service to start on boot by running:

    ```bash
    sudo systemctl enable mysql

## Step 6: Test LEMP Stack

1. Create a PHP info file in the web server's root directory:

    ```bash
    sudo nano /var/www/html/info.php

2. Add the content of the file of the file:
  
    ```bash
    <?php
    //output basic PHP infomation
    phpinfo();
    ?>

3. Open a web browser and navigate to your EC2 instance's public IP address or DNS name. You should see the Nginx default page indicating that Nginx is installed.

4. To test PHP, append "/info.php" to the end of the URL (e.g., http://your_ec2_public_ip/info.php). You should see a PHP information page displaying PHP version, configuration settings, etc.










