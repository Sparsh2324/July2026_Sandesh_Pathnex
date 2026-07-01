#   Day-01  Basic Coding practic

##  Ansible Task - Nginx installation

---

-   name:   Install Nginx
    hosts:   all
    become: yes

    task:
    -   name:   Install Nginx
        yum:
            name:   nginx
            state:  present


##  Terraform task  -   create EC2 instance

---

provider "aws" {
    region = "ap-south-1"
}

resource "aws_instance" "PathnexEC2" {
    ami     =   "ami-0abcd1234abcd1234"
    instance_type   =   "t3.micro"

    tags    = {
        Name    =   "PathNexEC2"
    }
}



##  K8s task    -   create nginx POD

---

apiVersion: v1
kind:   Pod
metadata:
    name:   Pathnex-nginx

spec:
    containers:
        -   name:   web
            image:  nginx:latest
            ports:
                -   containerPort:  80

##  SHELL script task   -   Print Date & Hostname

#!/bin/bash
echo "Date: $(date)"
echo "Hostname: $(HOSTNAME)"

---

#   Git Integration
##  Jenkins pipeline    -   git checkout

---

Pipeline    {
    agent   any
    stages  {
        stage ("git_checkout") {
            steps {
                git branch: "main", url: "https://github.com/Sparsh2324/July2026_Sandesh_Pathnex.git"
            }
        }
        stage ("list the files") {
            steps {
                sh '''
                cd July2026_Sandesh_Pathnex
                ls -la
                '''
            }
        }
    }
}

##  GitLab CI   -   Checkout Git

---

stages: 
    -   checkout


git-checkout:
    stage: checkout
    script:
        -   git clone "https://github.com/Sparsh2324/July2026_Sandesh_Pathnex.git"
        -   cd July2026_Sandesh_pathnex
        -   ls -la