# Python Application Deployment using CI/CD
### Project Overview

This project demonstrates deployment of a Python application using a CI/CD pipeline with Jenkins on AWS.
Whenever code is pushed to the GitHub repository, the pipeline automatically builds, tests, and deploys the application.

### Architecture

This Python CI/CD pipeline demonstrates automated deployment of a Python application on an AWS EC2 instance using Jenkins, GitHub

### Technologies & Platforms

1. AWS EC2 – Hosting Python application and Jenkins
2. GitHub – Source code version control
3. Jenkins – CI/CD automation
4. Python 3.10+ – Application runtime
5. Ubuntu – Server OS

### Steps 
### Step 1: Launch EC2 Instances
1.  Launch 2 Ubuntu EC2 instances:

 * Jenkins Server – for CI/CD
 * Python Application Server – to host your app

2. Configure Security Groups:

 * SSH (22)
 * HTTP (80) / Python app port (5000 or custom)
 * Jenkins port (8080)
 ### Step 2: Create & Clone GitHub Repository

1. Create a new repository: Python-app-deployment-using-CICD-pipeline

2. Clone repository on local machine:
   1. git clone https://github.com/<username>/Python-app-deployment-using-CICD-pipeline.git
   2. cd Python-app-deployment-using-CICD-pipeline

### Step 3: Create Application & Jenkins Configuration Files

#### 1 app.py
```
from flask import Flask
import os
app = Flask(__name__)

@app.route('/')
def hello_geek():
    return 'successfully deployed python application through jenkins!!!!!!!!!, added webhook'
@app.route('/hi')
def hell():
    return '<h1>Hiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiii from Flask & Docker</h1>'

if __name__ == "__main__":
    port = int(os.environ.get('PORT', 5000))
    app.run(debug=True, host='0.0.0.0', port=port)

```
#### 2. requirements.txt
```
click==8.0.3
colorama==0.4.4
Flask==2.0.2
itsdangerous==2.0.1
Jinja2==3.0.3
MarkupSafe==2.0.1
Werkzeug==2.0.2
gunicorn==20.1.0

```
#### 3. Jenkinsfile

#### 4. Commit & Push:
1. git add .
2. git commit -m "Added Python app and Jenkinsfile"
3. git push -u origin main

#### Step 4: Install Required Jenkins Plugins

1. SSH Agent
2. Git
3. Pipeline

#### Step 5: Create Jenkins Credentials

1. Go to Manage Jenkins → Credentials → Global → Add Credentials

2. Add SSH key for EC2:

   1. Kind: SSH Username with private key
   2. Username: ubuntu
   3. Private Key: paste key or choose file
   4. ID: python-app-key

 #### Step 6: Create Jenkins Job

 1. New Item → Pipeline → Name: Python-CICD-Pipeline
 2. Pipeline Definition → Pipeline script from SCM → Git
 3. Repository URL, branch, and credentials (python-app-key)
 4. Save & Build Now

 #### Step 7: Test Deployment

1. Trigger Build Now in Jenkins
2. Check Console Output
3. Access app in browser:http://<EC2-PUBLIC-IP:5000

#### Your Python app is now deployed and running using Jenkins CI/CD Pipeline on AWS EC2!