# AWS Backend API Deployment with Managed RDS

A production-ready deployment of a RESTful API on **Amazon EC2**, integrated with a managed **Amazon RDS** (Relational Database Service) instance. This project demonstrates core cloud infrastructure skills including compute management, database integration, and network security.

---

##  Architecture



The architecture follows cloud best practices by decoupling the application logic from the data layer:
1.  **EC2 (Ubuntu):** Hosts the Node.js/Express application.
2.  **RDS (MySQL/PostgreSQL):** A managed database service for automated backups and scaling.
3.  **Security Groups:** Acting as virtual firewalls to control inbound and outbound traffic.

---

##  Tech Stack
* **Cloud Provider:** AWS (EC2, RDS, VPC)
* **Backend:** Node.js, Express.js
* **Database:** Managed MySQL / PostgreSQL
* **Process Management:** PM2 (for logging and uptime)
* **Version Control:** Git

---

##  Key Features

### 1. Secure Database Integration
Implemented the **Principle of Least Privilege**. The RDS instance is placed in a private configuration where it only accepts traffic on Port 3306/5432 from the specific **Security Group ID** of the EC2 instance.

### 2. Environment Variable Management
Sensitive credentials (DB Host, User, Password) are managed using a `.env` file on the server. This ensures that no secrets are hardcoded or pushed to the GitHub repository.

### 3. Health Monitoring & Logging
* **Health Checks:** A dedicated `/health` endpoint to monitor the server status.
* **Logging:** Integrated **PM2** to manage application processes, providing real-time logs and ensuring the API restarts automatically on failure.

### 4. Optimized Security Groups
* **Port 22:** Restricted to specific IP for SSH management.
* **Port 80/3000:** Open for web traffic to the API.
* **Port 3306:** Restricted to internal traffic only.

---

##  Deployment Steps

### Step 1: Database Setup
1. Created an **Amazon RDS** instance (Free Tier).
2. Configured the Security Group to allow inbound traffic from the EC2 Security Group.

### Step 2: Server Setup
1. Launched an **EC2 (t2.micro)** instance with Ubuntu.
2. Installed Node.js and dependencies.
3. Configured environment variables in a `.env` file.

### Step 3: Application Launch
```bash
# Clone the repository
git clone [https://github.com/vishal0078380/your-repo-name.git](https://github.com/vishal0078380/your-repo-name.git)

# Install dependencies
npm install

# Start the application with PM2
pm2 start index.js --name "backend-api"

# Check logs
pm2 logs
