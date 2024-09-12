# Deploying Static Website using Load Balancer by ARM Template

## Project Overview

**Farmbox-Direct** Farmbox Direct is an e-commerce platform aimed at delivering fresh, organic fruits and vegetables directly to customers' doorsteps. The goal is to make healthy eating accessible and convenient by providing a simple way for users to order high-quality, farm-fresh produce online. 

This project demonstrates the deployment of **Farmbox-Direct** using Azure's ARM templates and load balancing across two Virtual Machines (VMs) in different availability zones for high availability and scalability.

## Problem Statement

In today’s fast-paced world, many people struggle to find time to shop for fresh, healthy produce, leading to poor diet choices and reliance on processed foods. Additionally, many communities have limited access to organic or locally-sourced fruits and vegetables, making it challenging to maintain a healthy lifestyle. After building the website, the challenge was to deploy it on Azure using a load-balanced architecture for efficient traffic distribution.

## Project Goals

- Deploy the ** Farmbox-Direct ** website on Azure using ARM templates.
- Set up a **Virtual Network (VNet)** with two **Subnets** and a **Network Security Group (NSG)**.
- Use a **Load Balancer** to distribute traffic between two VMs located in different availability zones.
- Host the static website on these VMs and make it accessible via the load balancer's frontend IP.

## Technologies and Azure Services Used

1. **Azure CLI**: Used to create the resource group and Virtual Network.
2. **ARM Templates**: Automated the creation of VNet, subnets, and NSG.
3. **Azure Virtual Machines (VMs)**: Hosted the Sitara-Hotel website.
4. **Azure Load Balancer**: Distributed the traffic between two VMs to ensure high availability.
5. **Nginx**: Used as a web server on both VMs to serve the static content.
6. **Git**: Cloned the website from GitHub onto the VMs using a custom script.
7. **Custom Script Extension**: Used to automatically configure the VMs upon deployment.

## Project Steps

### 1. Website Development
- ** Farmbox-Direct **: A static website allowing users to A hotel room booking website provides a convenient platform for customers to search, reserve, and pay for rooms online.

### 2. Deploying the Website on GitHub
- Frontend of  ** Farmbox-Direct ** was uploaded to a public GitHub repository: [Farmbox-Direct](https://github.com/Chabuksawar-Arun/Farmbox-Direct).

### 3. Azure Deployment Using ARM Templates
- **Resource Group**: Created using Azure CLI to hold all the resources.
- **Virtual Network (VNet)**: Set up using an ARM template, which included two subnets for distributing the VMs.
- **Network Security Group (NSG)**: Applied inbound rules to allow traffic on ports 22 (SSH) and 80 (HTTP).
  
### 4. Virtual Machines Setup
- **VM 1**: Created in Availability Zone 1 using Azure Portal. Configured with:
  - Custom Script Extension to clone the website from GitHub.
  - Networking settings to connect to the VNet and assigned Subnet.
  
 Custom Script:
  ```bash
  #!/bin/bash
  sudo apt update
  sudo apt install nginx git -y
  cd /tmp && git clone https://github.com/Chabuksawar-Arun/Farmbox-Direct
  sudo rm -rf /var/www/html/index.nginx-debian.html
  sudo cp -r /tmp/mysitee/* /var/www/html/
  ```
- **VM 2**: Created in Availability Zone 2 with the same configuration as VM 1.

### 5. Load Balancer Configuration
- **Load Balancer**: Configured to distribute traffic between VM 1 and VM 2.
  - **Frontend IP Configuration**: Assigned a new frontend IP for external access.
  - **Backend Pool**: Added both VMs to the backend pool for traffic distribution.
  - **Load Balancing Rule**: Defined to balance HTTP traffic (port 80) across the VMs.
  - **Health Probe**: Set up to monitor the health of the VMs and ensure traffic is routed only to healthy VMs.

### 6. Testing and Accessing the Website
- After the load balancer deployment, the website became accessible via the frontend IP of the load balancer. Users can interact with **Farmbox-Direct** to generate outfits from their clothing uploads.

## How to Use Farmbox-Direct

1.Open the website and open BookNow Right to top Corner of webpage.
2. Then it take to booking form fill the  and select type of room required.
3. By adding Payment details and confirm your stay.

## Azure Services and Tools Used

- **Azure CLI**: Resource group creation and management.
- **Azure Resource Manager (ARM) Templates**: Infrastructure-as-Code to deploy resources.
- **Virtual Network (VNet)**: Networking and subnetting.
- **Network Security Group (NSG)**: Security rules for VM access.
- **Azure Virtual Machines**: Hosting the website on multiple VMs.
- **Azure Load Balancer**: Load balancing between VMs.
- **Nginx**: Web server for hosting static content.
- **Git**: Version control and cloning the website onto VMs.
- **Custom Script Extension**: Automated configuration of VMs.

## Live Website and Resources

- **Website Link**: [Farmbox-Direct](https://github.com/Chabuksawar-Arun/Farmbox-Direct)
- **Demo Video**: [YouTube Demo](https://youtube.com/example)
- **Screenshots**:
  **Created Resource Group Screenshot**
  - ![ResourceGroup Screenshot](https://github.com/Chabuksawar-Arun/Farmbox-Direct/blob/main/Az%20resource%20group%20create.png)
    
  **ResourceGroup Deployment Output**
  - ![RSG-Deployment-output Screenshot](https://github.com/Chabuksawar-Arun/Farmbox-Direct/blob/main/resource%20group.jpg)

  **VNet Subnets RSG ARM Template Output**
  - ![VNetDeploymentoutputSS Screenshot](https://github.com/Chabuksawar-Arun/Farmbox-Direct/blob/main/Az%20deployment%20of%20Vnet%20(2).png)

   **Created VNet Screenshot** 
  - ![VNetSS Screenshot](https://github.com/Chabuksawar-Arun/Farmbox-Direct/blob/main/Virtual%20Network.png)

  **Created Subnets Screenshot**
  - ![SubnetSS Screenshot](https://github.com/Chabuksawar-Arun/Farmbox-Direct/blob/main/Vnet%20subnets.png)

   **Deployed VM 1 Screenshot**
  - ![VM1SS Screenshot](https://github.com/Chabuksawar-Arun/Farmbox-Direct/blob/main/Virtual%20Machine%201.png)

  **Deployed VM 2 Screenshot**
  - ![VM2SS Screenshot](https://github.com/Chabuksawar-Arun/Farmbox-Direct/blob/main/Virtual%20Machine%202.png)

  **Deployed LoadBalancer Screenshot**
  - ![LoadbalancerSS Screenshot](https://github.com/Chabuksawar-Arun/Farmbox-Direct/blob/main/Load%20Balancer.png )

  **Website Home Page Screenshot**
  - ![Sitara-Hotel Homepage Screenshot](https://github.com/Chabuksawar-Arun/Farmbox-Direct/blob/main/Homepage.png)

  **About page after complete Deployment**
  - ![GenerateOutfitsPage Screenshot](https://github.com/Chabuksawar-Arun/Farmbox-Direct/blob/main/About%20Page.png )

  **Services Page after complete Deployment**
  - ![About hotel Page Screenshot](https://github.com/Chabuksawar-Arun/Farmbox-Direct/blob/main/Services%20Page.png)
    
  **Blog Page after complete Deployment**
  - ![About hotel Page Screenshot](https://github.com/Chabuksawar-Arun/Farmbox-Direct/blob/main/Blog%20Page.png)
 
  **Contact Page after complete Deployment**
  - ![About hotel Page Screenshot](https://github.com/Chabuksawar-Arun/Farmbox-Direct/blob/main/Contact%20Page.png)


## Conclusion

This project showcases the end-to-end process of deploying a static website using Azure's ARM templates and load balancing capabilities. By distributing traffic between two VMs in different availability zones, we ensure high availability and scalability for the **Farmbox-Direct** platform. The integration of Azure's powerful tools and services simplified the deployment and configuration process.

## Author

**Chabuksawar Arun**  
**Sunnapu Shruthi** 
**Pandiri Pavan** 
Deployed by group as part of learning Azure's cloud infrastructure.

