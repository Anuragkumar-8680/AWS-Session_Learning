# AWS EC2 Deployment — Kubesimplify Live Workshop

> ⚠️ This is a forked repository from Kubesimplify.
> Original project & application code credit goes to 
> Kunal Verma & the Kubesimplify team.
> I did NOT build the application — I deployed it.
> 🔗 Workshop: https://www.youtube.com/watch?v=NLmF64KdLN0

## 📌 About
This project was completed as part of the **Kubesimplify Live Workshop**
on deploying and exposing a Node.js app to AWS EC2.
I followed along with the workshop to get real hands-on experience
with cloud deployment — not just theory.

> The website, application code, and original README
> were built by Kunal Verma (@verma-kunal).
> My contribution was purely the deployment process.

## 🛠 What I Did (Deployment Steps)

### 1. AWS Setup
- Created an **IAM user** with admin permissions
- Launched an **EC2 instance** (Ubuntu, t2.micro)
- Created and downloaded a new **.pem key pair**
- Configured **security group inbound rules** to allow traffic on port 3000

### 2. SSH into EC2
Connected to the remote EC2 instance using Git Bash on Windows:
ssh -i "D:\Devops\EC2_Project.pem" ubuntu@<EC2-PUBLIC-IP>

### 3. Configuring Ubuntu on EC2
Updated packages and installed dependencies:
sudo apt update
- Installed **Git** on the remote VM
- Configured **Node.js and npm** on the remote VM

### 4. Editing Files on EC2
Used **nano** (via Git Bash terminal) to edit files directly on the EC2 instance:
nano .env
nano server.js

### 5. Environment Variables Setup
Created a `.env` file on the EC2 instance:
DOMAIN="http://<EC2-PUBLIC-IP>:3000"
PORT=3000
STATIC_DIR="./client"
PUBLISHABLE_KEY=""
SECRET_KEY=""

### 6. Code Fix — server.js
Modified `server.js` to bind the server to `0.0.0.0`
so the app is accessible via EC2 public IP:

Before:
app.listen(port, () => {
After:
app.listen(port, '0.0.0.0', () => {
> Without this fix the app only runs on localhost
> and is NOT accessible from the public internet
> even with correct inbound rules.

### 7. Deploying the Project
git clone https://github.com/verma-kunal/AWS-Session.git
npm install
npm run start

### 8. Fixing npm Vulnerabilities
Resolved 3 high severity vulnerabilities in nodemon:
npm install nodemon@latest --save-dev
Result: 0 vulnerabilities ✅

## 💻 Tech Stack Used
- AWS EC2 (Ubuntu)
- Node.js & Express
- Stripe Payment Gateway
- dotenv
- nodemon
- Git Bash (Windows SSH & file editing)
- nano (file editing on EC2)

## 🔧 How to Run Locally
1. Clone the repo
git clone https://github.com/Anuragkumar-8680/AWS-Sesssion_Learning.git
2. Install dependencies
npm install
3. Create a `.env` file
DOMAIN="http://localhost:3000"
PORT=3000
STATIC_DIR="./client"
PUBLISHABLE_KEY=your_stripe_publishable_key
SECRET_KEY=your_stripe_secret_key
4. Start the server
npm run start
5. Open in browser
http://localhost:3000

## 🎓 Credit
- Original application & code by **Kunal Verma**
- GitHub: https://github.com/verma-kunal/AWS-Session
- Workshop by **Kubesimplify**
- YouTube: https://www.youtube.com/watch?v=NLmF64KdLN0
- Channel: https://www.youtube.com/@kubesimplify
