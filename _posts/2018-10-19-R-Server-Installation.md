---
title: R Server installation
date: 2018-10-19 12:28:12 -0500
categories: [Server]
tags: [r-server]
---

Installing the R Server is motivated by a wechat article [搭建你的免费R云端服务器](https://mp.weixin.qq.com/s/s9m_1wdm2CF6Ct0w-erN8g). It uses the Machine Learning Server which recently becomes free to the public by Microsoft. The installation of Machine Learning Server refers the [official documentation](https://docs.microsoft.com/en-us/machine-learning-server/install/machine-learning-server-linux-install#install-on-ubuntu-). And I install it on my AWS server. Since I only have access to Ubuntu14.04 and Ubuntu18.04, I choose to install it on the 14.04 version.

### Step 1
Launch the instance of Ubuntu 14.04 in AWS account. By the way, students could apply for AWS Educate for computing resources.

### Step 2
Sign in as a Microsoft Developer and thus could have access to dev essential resources. Then follow the instruction on Microsoft Official Doc about Ubuntu:

```
# Install as root
sudo su

# Optionally, if your system does not have the https apt transport option
apt-get install apt-transport-https

  # Add the **azure-cli** repo to your apt sources list
AZ_REPO=$(lsb_release -cs)

echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | sudo tee /etc/apt/sources.list.d/azure-cli.list

# Set the location of the package repo the "prod" directory containing the distribution.
# This example specifies 16.04. Replace with 14.04 if you want that version
wget https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb

# Register the repo
dpkg -i packages-microsoft-prod.deb

# Verify whether the "microsoft-prod.list" configuration file exists
ls -la /etc/apt/sources.list.d/

# Add the Microsoft public signing key for Secure APT
apt-key adv --keyserver packages.microsoft.com --recv-keys 52E16F86FEE04B979B07E28DB02C46DF417A0893

# Update packages on your system
apt-get update

# Install the server
apt-get install microsoft-mlserver-all-9.3.0

# Activate the server
/opt/microsoft/mlserver/9.3.0/bin/R/activate.sh     

# List installed packages as a verification step
apt list --installed | grep microsoft  

# Choose a package name and obtain verbose version information
dpkg --status microsoft-mlserver-packages-r-9.3.0
```

However, error messages come out when installing the server. It could due to the AWS, but I haven't figured that out yet. Then, I tried to install the server on the Red Hat system refering to the [Official Doc](https://docs.microsoft.com/en-us/machine-learning-server/install/machine-learning-server-linux-install#install-on-red-hat-or-centos). But it still failed. The error showed that there was not enough disk memory for it. 
