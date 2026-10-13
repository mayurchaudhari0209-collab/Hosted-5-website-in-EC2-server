# Hosted 5 Websites on a Single EC2 Instance Using Nginx

## 📌 Project Overview

This project demonstrates how to host **5 different websites on a single Amazon EC2 instance** using the Nginx web server.

Each website uses a different port number, allowing multiple websites to run on one server.

## 🎯 Project Objectives

- Launch an Amazon EC2 instance.
- Install and configure Nginx.
- Create separate directories for five websites.
- Configure Nginx to host multiple websites using different ports.
- Access all five websites through a web browser.

## 🛠️ AWS Services and Technologies

- **Amazon EC2** – Virtual server to host websites.
- **Nginx** – Web server.
- **Amazon Linux / Ubuntu** – Operating system.
- **HTML and CSS** – Website content.
- **Security Groups** – Control inbound traffic.
- **SSH** – Connect to the EC2 instance.

## 🏗️ Architecture

```text
                 Users / Web Browser
                         |
                  Internet Gateway
                         |
                  Amazon EC2 Instance
                         |
                       Nginx
                         |
          +--------------+--------------+
          |              |              |
       Port 8081      Port 8082      Port 8083
          |              |              |
       Website 1      Website 2      Website 3

          +--------------+--------------+
          |                             |
       Port 8084                     Port 8085
          |                             |
       Website 4                    Website 5
```

## ⚙️ Implementation Steps

### Step 1: Launch an EC2 Instance

1. Open the AWS Management Console.
2. Navigate to Amazon EC2.
3. Launch an Amazon Linux or Ubuntu instance.
4. Configure the key pair and network settings.
5. Allow SSH traffic on port 22 from your IP address.
6. Connect to the instance using SSH.

### Step 2: Install Nginx

For Amazon Linux 2023:

```bash
sudo dnf update -y
sudo dnf install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx
```

### Step 3: Create Five Website Directories

```bash
sudo mkdir -p /var/www/site1
sudo mkdir -p /var/www/site2
sudo mkdir -p /var/www/site3
sudo mkdir -p /var/www/site4
sudo mkdir -p /var/www/site5
```

### Step 4: Create Website Pages

```bash
echo "<h1>Welcome to Website 1</h1>" | sudo tee /var/www/site1/index.html
echo "<h1>Welcome to Website 2</h1>" | sudo tee /var/www/site2/index.html
echo "<h1>Welcome to Website 3</h1>" | sudo tee /var/www/site3/index.html
echo "<h1>Welcome to Website 4</h1>" | sudo tee /var/www/site4/index.html
echo "<h1>Welcome to Website 5</h1>" | sudo tee /var/www/site5/index.html
```

### Step 5: Configure Nginx

Create a configuration file:

```bash
sudo vi /etc/nginx/conf.d/multi-sites.conf
```

Add the following configuration:

```nginx
server {
    listen 8081;
    root /var/www/site1;
    index index.html;
}

server {
    listen 8082;
    root /var/www/site2;
    index index.html;
}

server {
    listen 8083;
    root /var/www/site3;
    index index.html;
}

server {
    listen 8084;
    root /var/www/site4;
    index index.html;
}

server {
    listen 8085;
    root /var/www/site5;
    index index.html;
}
```

Save the file and exit the editor.

### Step 6: Test and Restart Nginx

```bash
sudo nginx -t
sudo systemctl restart nginx
sudo systemctl status nginx
```

### Step 7: Configure the EC2 Security Group

Add these inbound rules for testing:

| Type | Port | Source |
|---|---:|---|
| SSH | 22 | My IP |
| Custom TCP | 8081 | Your IP |
| Custom TCP | 8082 | Your IP |
| Custom TCP | 8083 | Your IP |
| Custom TCP | 8084 | Your IP |
| Custom TCP | 8085 | Your IP |

For production, restrict access to the required users or place the websites behind an appropriate load balancer or reverse proxy.

### Step 8: Access the Websites

Replace `EC2-PUBLIC-IP` with your instance's public IPv4 address.

```text
http://EC2-PUBLIC-IP:8081
http://EC2-PUBLIC-IP:8082
http://EC2-PUBLIC-IP:8083
http://EC2-PUBLIC-IP:8084
http://EC2-PUBLIC-IP:8085
```

Each URL should display a different website.

## ✅ Expected Results

- Website 1 runs on port 8081.
- Website 2 runs on port 8082.
- Website 3 runs on port 8083.
- Website 4 runs on port 8084.
- Website 5 runs on port 8085.

All five websites are hosted on a single EC2 instance using Nginx.

## 📚 Key Learnings

- Launching and managing Amazon EC2 instances.
- Installing and configuring Nginx.
- Hosting multiple websites on one server.
- Configuring Nginx server blocks and ports.
- Managing AWS Security Group inbound rules.
- Troubleshooting website connectivity.

## 👨‍💻 Author

**Mayur Chaudhari**

GitHub Repository: [Hosted 5 Websites on 1 EC2 Server](https://github.com/mayurchaudhari0209-collab/Hosted-5-website-in-EC2-server)

## 🚀 Future Improvements

- Configure domain names for the websites.
- Enable HTTPS using SSL/TLS certificates.
- Host production-ready HTML and CSS websites.
- Configure monitoring and logging.
- Improve availability and security.
