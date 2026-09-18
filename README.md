```
eksctl create cluster --name mycluster --region us-east-1 --nodegroup-name mynodes --node-type t3.medium --nodes 2 --nodes-min 2 --nodes-max 2 --managed

aws eks update-kubeconfig --name mycluster --region us-east-1

// trivy - security scan 

- vulnerabilities - report 

choco install trivy 

WSL >> 

sudo apt-get install wget gnupg
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg > /dev/null
echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb generic main" | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install trivy

trivy --version 

// keep docker desktop in running state 

docker pull nginx:latest
trivy image nginx:latest
trivy image --severity HIGH,CRITICAL nginx:latest
trivy image --ignore-unfixed nginx:latest

// helloworld.py 

print("hello world")
print("username: admin")

# Basic password comment
# password: admin

# Dummy secrets for Trivy practice ONLY
AWS_ACCESS_KEY_ID = "AKIAIOSFODNN7EXAMPLE"
AWS_SECRET_ACCESS_KEY = "wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY"

GITHUB_TOKEN = "ghp_1234567890abcdefghijklmnopqrstuvwxyz"

DATABASE_URL = "mysql://admin:TestPassword123@database.example.com:3306/mydb"

2. // Create Dockerfile

FROM python:3.12-slim
WORKDIR /app
COPY . .
CMD ["python","helloworld.py"]

3. Image Build 

docker buildx build -t docker.io/atuljkamble/pythonapp --load .

4. scan via trivy

trivy image atuljkamble/pythonapp:latest

5. scan file system

trivy fs secrets.txt
trivy fs .

6. scan manifests 

trivy config deployment.yaml


```
