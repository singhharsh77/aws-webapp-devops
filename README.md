# 🚀 DevOps Project: Deploying a Java Web App on AWS

This is my **first hands-on DevOps project**, where I set up and deployed a simple Java-based web application on **AWS EC2** using **Maven**, **Java (Amazon Corretto 8)**, and **VS Code Remote SSH**.  

The goal was to set up a **CI/CD-ready environment** in the cloud, automate the build using Maven, and confirm successful deployment of a web app.

---

## 🔧 Project Steps

### 1️⃣ AWS IAM User Setup
- Created an IAM user `Harsh-IAM-Admin` with **AdministratorAccess**.
- Downloaded credentials (.csv) and used this user instead of root for security.

### 2️⃣ EC2 Instance Launch
### EC2 Instance Running(![Screenshorts/Screenshot 2025-09-13 at 11.55.10 PM.png](https://github.com/singhharsh77/aws-webapp-devops/blob/main/Screenshorts/Screenshot%202025-09-13%20at%2011.55.10%E2%80%AFPM.png))
![EC2 Instance]
- Region: `ap-south-1 (Mumbai)`
- Instance Type: `t2.nano`
- AMI: **Amazon Linux 2023**
- Created a key pair `work-keypair.pem`
- Updated permissions:  
  ```bash
  chmod 400 work-keypair.pem
  ```
- Connected via SSH:
  ```bash
  ssh -i ~/Desktop/DevOps/work-keypair.pem ec2-user@<public-dns>
  ```

### 3️⃣ Install Dependencies
- Installed **Maven**:
  ```bash
  wget https://archive.apache.org/dist/maven/maven-3/3.5.2/binaries/apache-maven-3.5.2-bin.tar.gz
  sudo tar -xzf apache-maven-3.5.2-bin.tar.gz -C /opt
  echo "export PATH=/opt/apache-maven-3.5.2/bin:$PATH" >> ~/.bashrc
  source ~/.bashrc
  ```
- Installed **Java 8 (Amazon Corretto)**:
  ```bash
  sudo dnf install -y java-1.8.0-amazon-corretto-devel
  export JAVA_HOME=/usr/lib/jvm/java-1.8.0-amazon-corretto.x86_64
  export PATH=$JAVA_HOME/jre/bin:$PATH
  ```

### 4️⃣ Generate Web App with Maven
```bash
mvn archetype:generate \
    -DgroupId=com.nextwork.app \
    -DartifactId=nextwork-web-project \
    -DarchetypeArtifactId=maven-archetype-webapp \
    -DinteractiveMode=false
```
- Verified with `BUILD SUCCESS`.

### 5️⃣ Connect VS Code to EC2
- Installed **Remote - SSH** extension.
- Added SSH config:
  ```txt
  Host ec2-3-6-94-23.ap-south-1.compute.amazonaws.com
    HostName ec2-3-6-94-23.ap-south-1.compute.amazonaws.com
    IdentityFile ~/Desktop/DevOps/nextwork-keypair.pem
    User ec2-user
  ```
- Opened project in VS Code:
  ```
  /home/ec2-user/nextwork-web-project
  ```

### 6️⃣ Edit Web App
- Updated `index.jsp` with:
  ```html
  <html>
    <body>
      <h2>Hello Harsh!</h2>
      <p>This is my Work web application working! You can Edit this according to your needs</p>
    </body>
  </html>
  ```

---

## 📸 Screenshots  

Screenshots of the setup and steps are stored in the [`/screenshots`](./screenshots) folder:

- ✅ EC2 instance running  
- ✅ SSH connection  
- ✅ Maven `BUILD SUCCESS`  
- ✅ VS Code Remote-SSH connected  
- ✅ `pom.xml` setup  
- ✅ Edited `index.jsp`  

---

## 🧹 Cleanup
- Terminated EC2 instance to avoid extra charges.

---

## 🚀 Key Learnings
- Setting up secure access to AWS with **IAM users**.
- Launching and configuring **EC2 instances**.
- Installing and configuring **Java & Maven**.
- Using **Maven archetypes** to bootstrap a project.
- Connecting **VS Code** with remote servers via SSH.
- Deploying and customizing a **Java web app** in the cloud.

---

## 📌 Next Steps
- Containerize the application with **Docker**.
- Automate deployment with **Jenkins / GitHub Actions**.
- Deploy to **Kubernetes** for scaling.
