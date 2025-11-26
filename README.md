📦 GlobalMart React CI/CD on AWS (CodePipeline + CodeBuild + CodeDeploy + EC2)

This project demonstrates a full CI/CD pipeline for deploying a React application on AWS using:

GitHub (Source)

AWS CodePipeline

AWS CodeBuild

AWS CodeDeploy

Amazon EC2

Node.js runtime

🚀 Architecture Overview
GitHub → CodePipeline → CodeBuild → S3 Artifacts → CodeDeploy → EC2 → Production App

📁 Repository Structure
├── appspec.yml
├── buildspec.yml
├── scripts/
│   └── restart_server.sh
├── public/
├── src/
├── package.json
└── README.md

⚙️ CI/CD Flow
1️⃣ Git Push

Whenever a commit is pushed to main, CodePipeline is triggered automatically.

2️⃣ CodeBuild

Installs Node.js & dependencies

Builds React application using npm run build

Uploads artifacts to S3

3️⃣ CodeDeploy

Copies build output to the EC2 instance

Runs scripts/restart_server.sh to restart the app

4️⃣ Serve React App

Node.js HTTP server serves the production build.

🧪 Testing the App

Once deployed:

http://<EC2-Public-IP>:3000/

🛠️ Key Difficulties Faced & How They Were Solved
✔️ 1. S3 Artifact Access Denied

Error: Insufficient S3 permissions

Fix: Updated CodePipeline IAM role & bucket policy with:

GetObject

PutObject

ListBucket

✔️ 2. CodeDeploy Failing — “appspec.yml not found”

Cause: Wrong file placement in ZIP

Fix: Ensure appspec.yml exists at the root of the repository

✔️ 3. React not loading on EC2

Cause: Using the development server (npm start)

Fix: Use production build + Node static server:

serve -s build


or use Node HTTP server or nginx.

✔️ 4. Port Not Accessible

Cause: EC2 Security group missing inbound rule

Fix: Allowed port 3000 in SG.

🧾 Deployment Scripts
appspec.yml

Used by CodeDeploy for copying files & running scripts.

restart_server.sh

Starts Node.js server using nohup.

📚 Learning Outcomes

CI/CD automation using AWS developer tools

Debugging real-world CodeBuild + CodeDeploy problems

Setting up a production React environment on EC2

IAM access management

S3 artifact handling

⚡ Final Result

A fully automated AWS CI/CD pipeline deploying a React app to EC2 on every GitHub push.
