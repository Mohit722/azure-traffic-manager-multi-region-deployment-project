 Project Name: Azure Traffic Management and Load Balancing Solution:
—-------------------------------------------------------------------

Project Overview:
-----------------

This project focuses on deploying a highly available and scalable web application architecture using Azure services, particularly leveraging Azure Traffic Manager for DNS-based routing and Application Gateways for load balancing and security.

Key Components:

1. Virtual Machines (VMs): 
   - Four Ubuntu-based VMs are deployed across two Azure regions (East US and West US) to ensure redundancy and minimize latency for users in different geographical locations.
   - Each VM hosts a web application that provides specific functionality, with dedicated scripts (`vm1.sh` and `vm2.sh`) to set up the environment and dependencies automatically.

2. Azure Storage Account:
   - A storage account is created to host static content (like error pages) for the web application. Anonymous access is enabled for easy accessibility.
   - The static website feature is utilized to serve the `error.html` file, which acts as a custom error page for the application.

3. Application Gateways:
   - Two Application Gateways (Ag1 and Ag2) are set up in East US and West US, respectively. These gateways serve as a layer for managing traffic to the VMs, ensuring secure and efficient routing.
   - Custom error handling is implemented, directing traffic to static error pages when issues arise.

4. Azure Traffic Manager:
   - Traffic Manager profiles are configured to manage routing to the application gateways based on performance. This ensures that users are directed to the nearest available endpoint, reducing latency and improving application responsiveness.
   - Two endpoints are added to the Traffic Manager profile, corresponding to the public IP addresses of the Application Gateways, enabling DNS-based load balancing.

5. User Experience:
   - The project includes a demonstration of how the system behaves under various conditions, such as accessing specific paths (like `/upload1`), showcasing how the error handling mechanisms work effectively.
   - The Traffic Manager ensures that requests are distributed appropriately between the East US and West US resources, providing seamless access to users.

 
Interview Explanation Points:

- Architecture: Explain the choice of a multi-region deployment for resilience and improved performance.
- Traffic Management: Highlight the benefits of using Azure Traffic Manager for routing and how it enhances the user experience by directing traffic based on performance metrics.
- Load Balancing: Discuss how Application Gateways manage incoming traffic, ensuring efficient distribution and security (e.g., SSL termination).
- Scalability: Emphasize the ability to scale the solution by adding more VMs and endpoints without significant architectural changes.
- Error Handling: Demonstrate how the custom error pages enhance user experience during failures or issues with the application.



Here are detailed explanations for each of the points, which will help you convey the project's architecture and functionalities effectively:

1. Architecture:
Multi-Region Deployment:
- Resilience: By deploying resources across multiple Azure regions (East US and West US), the application can maintain availability even in the event of regional failures. If one region goes down due to an outage, the other can still serve user requests, ensuring minimal disruption.
- Improved Performance: Users are directed to the nearest region based on their geographical location. This reduces latency, as data doesn't have to travel long distances. For example, a user in the East US will connect to resources in the East US, resulting in faster response times.
- Disaster Recovery: Multi-region deployment facilitates effective disaster recovery strategies. In the case of significant outages or data loss in one region, the system can automatically redirect traffic to the other region, ensuring business continuity.


2. Traffic Management:
Benefits of Azure Traffic Manager:
- Performance-Based Routing: Azure Traffic Manager directs user requests to the endpoint with the lowest latency or best performance. This is crucial for applications with a global user base, as it optimizes response times and provides a seamless experience.
- DNS-Level Load Balancing: Traffic Manager operates at the DNS level, meaning it resolves domain names to the appropriate endpoints based on the routing method chosen (e.g., performance, geographic, etc.). This approach helps distribute traffic intelligently and balances the load across various resources.
- Health Monitoring: Traffic Manager continuously monitors the health of the endpoints. If an endpoint becomes unavailable, Traffic Manager automatically reroutes traffic to healthy endpoints, enhancing availability.
- User Experience: By ensuring that users are connected to the most responsive endpoints, Traffic Manager improves overall user satisfaction and reduces frustration due to slow response times or application unavailability.

 
3. Load Balancing:
Application Gateways:
- Traffic Distribution: Azure Application Gateways intelligently manage incoming traffic by distributing requests across multiple backend instances (e.g., VMs). This ensures that no single instance becomes a bottleneck, leading to improved application performance and responsiveness.
- Security Features: Application Gateways offer built-in security features, such as Web Application Firewall (WAF) capabilities, which help protect against common web vulnerabilities and attacks (e.g., SQL injection, cross-site scripting).
- SSL Termination: Application Gateways can handle SSL termination, meaning they can decrypt incoming SSL traffic before forwarding it to backend instances. This offloads the decryption process from the VMs, reducing their load and simplifying certificate management.
- Custom Error Handling: Gateways can be configured to serve custom error pages (e.g., 404 or 502 error pages), providing users with a more user-friendly experience during issues.

 
4. Scalability:
Scalability of the Solution:
- Adding Resources: The architecture allows for easy scalability by adding more VMs or endpoints to meet increased demand. Azure services can scale up or down based on traffic loads, ensuring optimal performance at all times.
- Load Balancer Configuration: Both Traffic Manager and Application Gateways can dynamically accommodate additional resources without significant changes to the existing architecture. This means as user traffic grows, new VMs can be added to the backend pool, and the gateways can automatically start directing traffic to these new instances.
- Future-Proofing: The architecture is designed to be future-proof, enabling quick adjustments to accommodate emerging technologies or changing user demands. This ensures long-term viability and performance of the application.

 
5. Error Handling:
Custom Error Pages:
- User Experience Enhancement: The use of custom error pages helps guide users when they encounter issues. Instead of showing generic error messages, the application can present user-friendly pages that explain the issue and provide options for next steps (e.g., returning to the homepage or trying again later).
- Static Website Hosting: By hosting error pages in Azure Blob Storage as static websites, the application ensures quick delivery of these error messages without impacting performance. This setup helps users understand what went wrong, reducing frustration and confusion.
- Consistent Branding: Custom error pages allow organizations to maintain consistent branding, even during errors. This professionalism helps reinforce user trust in the application.


----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------



# Overview
As an Azure professional, your task is to implement an architecture for the company's website that balances traffic, manages routing, and provides redundancy across two regions. The architecture includes the following components:

```
                     +-----------------------+
                     |  Azure Traffic Manager |
                     +-----------------------+
                        /                  \
                       /                    \
            +-------------------+      +-------------------+
            | Application Gateway 1 |      | Application Gateway 2 |
            |      (Central US)     |      |       (West US)      |
            +-------------------+      +-------------------+
                  /          \                /          \
                 /            \              /            \
            +------+      +------+       +------+      +------+
            |  VM 1 |      |  VM 2 |       |  VM 1 |      |  VM 2 |
            +------+      +------+       +------+      +------+
               |                |               |                |
          +--------------+  +--------------+  +--------------+  +--------------+
          |    Vnet 1    |  |    Vnet 1    |  |    Vnet 2    |  |    Vnet 2    |
          +--------------+  +--------------+  +--------------+  +--------------+




 
Project: Optimized Multi-Region Deployment with Azure Traffic Manager:
-----------------------------------------------------------------------

# Overview
This project aims to implement a multi-region deployment to ensure optimal traffic distribution across Central US and West US. Utilizing Azure Traffic Manager and Application Gateways, this architecture provides a fault-tolerant, scalable solution to manage web traffic efficiently while maintaining high availability.
 
Architecture Components

1. Azure Traffic Manager
   - Purpose: Distributes incoming traffic across different endpoints based on routing policies, such as performance or geographic location.

2. Application Gateways
   - Application Gateway 1 (Central US): Routes traffic to Virtual Machines in Central US.
   - Application Gateway 2 (West US): Routes traffic to Virtual Machines in West US.

3. Virtual Machines (VMs)
   - Central US Region:
     - VM1: Hosts the Upload Page.
     - VM2: Hosts the Home Page.
   - West US Region:
     - VM1: Hosts the Upload Page.
     - VM2: Hosts the Home Page.

4. Virtual Networks (VNets)
   - VNet1 (Central US): Contains VM1 and VM2 for handling regional traffic.
   - VNet2 (West US): Contains VM1 and VM2 in the West US region.
   - Cross-Region Connectivity: VNets in both regions communicate securely, ensuring seamless service operation across regions.

5. Storage Account
   - Static Website Hosting: Hosts the `error.html` file as a static page for error handling.
   - Upload Container: Stores uploaded files required by the application, facilitating centralized data storage.

---

 Web Pages Setup

- Home Page: Deployed on VM2 in both regions, accessed via a specific DNS (`example.com`).
- Upload Page: Deployed on VM1 in both regions, accessible through a separate DNS path (`example.com/upload`).
- Error Page: A static page stored in Azure Storage, which Application Gateways redirect to in case of failures on the primary pages.

---

 
Routing and DNS Configuration

- Home Page: Configured to resolve DNS `example.com` to VM2 instances in either region.
- Upload Page: Configured to resolve DNS `example.com/upload` to VM1 instances in either region.
- Error Page: Application Gateways redirect to the error page (`error.html`) hosted on Azure Storage if any service disruption occurs.

---

 
Implementation Steps

1. Set Up Azure Traffic Manager
   - Create a Traffic Manager profile with endpoints linked to Application Gateway 1 and Application Gateway 2.
   - Configure routing policies to distribute traffic based on performance and regional proximity.

2. Deploy Application Gateways
   - Set up Application Gateway 1 in Central US and Application Gateway 2 in West US.
   - Define routing rules that direct traffic from specific DNS paths to corresponding VM instances.

3. Provision Virtual Machines
   - Deploy VM1 and VM2 within VNet1 (Central US) and VNet2 (West US).
   - Use Azure CLI or the Azure Portal to create and configure VMs for each region.
   - Assign VMs to handle specific web pages (Upload and Home).

4. Configure Error Page on Azure Storage
   - Create a Storage Account and enable static website hosting.
   - Upload the `error.html` file, which serves as the failover page.
   - Integrate the Storage Account with the GitHub repository to enable continuous updates to `error.html` as required.

5. Connect GitHub Repository
   - Link the Azure Storage Account to the GitHub repository where the `error.html` file is stored.
   - Set up automation to update the static website whenever `error.html` is modified in the repository.

---

 
Storage Account Setup

1. Static Website Hosting:
   - Configure `error.html` as a static website hosted in the Storage Account.
   - Direct Application Gateway 403 and 502 errors to this static page.

2. Upload Container:
   - Create an "upload" container in the Storage Account for file storage and application use.
   - This provides a centralized location for handling uploaded data across regions.

---

 
Technical Specifications for Deployment

1. Regional VM Deployments
   - Deploy VMs in both Central US and West US regions for redundancy.
   - Clone the GitHub repository ([https://github.com/azcloudberg/azproject](https://github.com/azcloudberg/azproject)) to each VM and execute deployment scripts for each service.

2. Repository Cloning and Script Execution
   - VM1: Run `vm1.sh` to deploy the Upload Page.
   - VM2: Run `vm2.sh` to deploy the Home Page.

3. Routing Types and Functions
   - Application Gateway: Utilizes path-based routing, directing traffic based on specific URL paths (e.g., `/upload` for Upload Page).
   - Azure Traffic Manager: Manages traffic flow at the DNS level, balancing load across Application Gateways depending on user location and resource availability.



Summary:
 By implementing this architecture, you will achieve a robust, highly available system that supports regional redundancy and efficient traffic distribution. The integration of Azure Traffic Manager, Application Gateways, and Storage Accounts ensures that users experience minimal downtime, as the architecture automatically fails over to available resources and displays error pages when necessary. This approach provides a reliable, scalable foundation for deploying web services across multiple regions, ensuring optimal performance and user satisfaction.



--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------



# Step-by-Step Guide for Setting Up Capstone Project:
-----------------------------------------------------

1. Create a Resource Group
   - Name: Capstone Project
   - Region: Central US
   - Action: Click on Review + Create to finalize.



2. Setting Up Virtual Machine 1 (VM1) - East US
   

 - VNet-to-VNet Peering:
   - Ensure both regions are connected through VNet-to-VNet Peering for seamless communication.

- Traffic Manager Setup
   - Configure Traffic Manager to route traffic between the Application Gateways of both regions.

- Application Gateway and Subnet Configuration
   - Note: The Application Gateway should not be in the same subnet as the VMs.
   - Create a separate subnet specifically for the Application Gateway.


# Main Objective
   - Deploy four VMs and one storage account for the application deployment.


# Creating VM1 East US:
-------------------------

# Portal Configuration for VM1
   - Go to the Azure Portal and start creating VM1 under the Capstone Project resource group.
   - Region: Central US
   - Security Type: Standard
   - Image: Ubuntu Server 20.04
   - VM Size: B1s (Basic)
   - Username: azureuser
   - Password: Sajal@56712378
   - Inbound Ports: HTTP (80), SSH (22)

# Network Section Setup
   - Virtual Network (VNet): Create a new VNet
     - Name: Vnet1
     - Subnet Name: subnet1
     - Address Range: 10.0.0.0/24
   - Create an additional subnet for the Application Gateway:
     - Subnet Name: subnet1_ag1
     - Address Range: 10.0.1.0/24 
     - Note: Ensure the subnet address range is different from the VM subnet to avoid overlap and ensure compatibility.

# Public IP Configuration
   - Change the name of the Public IP to ip1 for easier identification.

# Final Steps
   - Review all settings, then click on Review + Create to deploy the VM and network configurations.



# Step-by-Step Guide for Setting Up Additional VMs

3. Creating VM2 - East US:
------------------------------

   - Azure Portal Configuration:
     - Go to the Azure Portal and start creating VM2 within the Capstone Project resource group.
     - Region: Central US
     - Security Type: Standard
     - Image: Ubuntu Server 20.04
     - VM Size: B1s (Basic)
     - Username: azureuser
     - Password: Sajal@56712378
     - Inbound Ports: HTTP (80), SSH (22)
   
   - Network Section:
     - VNet: Select Vnet1
     - Subnet: Select subnet1 (created for VM1)
   
   - Click on Review + Create to proceed.


# Creating a New Virtual Network for Future Use:
   - VNet Name: Vnet2
   - Subnet Name: subnet2
   - Address Range: 10.0.0.0/24

# Creating an Additional Subnet for the Application Gateway:
   - Subnet Name: subnet_ag2
   - Address Range: 10.0.1.0/24 (Ensuring a unique range for compatibility with the Application Gateway)
   
   - Public IP: Rename the Public IP for VM2 to ip3.

   - Click Review + Create to finalize VM2 configuration.

---

4. Creating VM1 - West US

   - Azure Portal Configuration:
     - Go to the Azure Portal and start creating VM1WUS within the Capstone Project resource group.
     - Region: West US 2
     - Security Type: Standard
     - Image: Ubuntu Server 20.04
     - VM Size: B1s (Basic)
     - Username: azureuser
     - Password: Sajal@56712378
     - Inbound Ports: HTTP (80), SSH (22)

   - Network Section:
     - Create a new VNet:
       - Name: Vnet2
       - Subnet Name: subnet2
       - Address Range: 10.0.0.0/24
     - Public IP: Rename the Public IP for VM1WUS to ip3.

   - Click Review + Create to complete the setup for VM1 - West US.

---

5. Creating VM2 - West US

   - Azure Portal Configuration:
     - Go to the Azure Portal and start creating VM2WUS within the Capstone Project resource group.
     - Region: West US 2
     - Security Type: Standard
     - Image: Ubuntu Server 20.04
     - VM Size: B1s (Basic)
     - Username: azureuser
     - Password: Sajal@56712378
     - Inbound Ports: HTTP (80), SSH (22)
   
   - Network Section:
     - Select Vnet2
     - Subnet: Choose subnet2
   
   - Public IP: Rename the Public IP for VM2WUS to ip4.

   - Click Review + Create to finalize the configuration for VM2 - West US.

--- 
With these steps, both Central US and West US regions now have 2-2 VMs each, ready for deployment and configuration within the Azure network structure.






# Step-by-Step Guide for Setting Up the Storage Account and Static Website Hosting:
-------------------------------------------------------------------------------------

1. Creating the Storage Account

   - Azure Portal Configuration:
     - Go to the Azure Portal and start creating a Storage Account.
     - Name: Choose a unique name for your storage account.
   
   - Advanced Settings:
     - Enable anonymous access on individual containers.
   
   - Click on Review + Create to finalize the setup of the storage account.


2. Creating a Container and Uploading the Error Page

   - Once the storage account is created, navigate to Resource.
   - Go to the Containers section to create a new container.
   
   - Container Configuration:
     - Name: upload
     - Anonymous Access Level: Containers (allowing anonymous read access for containers and blobs)
   
   - Click Create to set up the container.

   - Uploading the Error Page:
     - Open the upload container.
     - Upload your `error.html` page inside this container.


3. Enabling Static Website Hosting

   - In the left-side menu, search for Static Website.
   - Enable Static Website hosting.
   - Error Document Path: Set it to `error.html`.
   - Click Save to apply the settings.
   
   - Upon saving, you'll receive Primary Endpoint and Secondary Endpoint URLs, which are used to access the static website.


4. Pointing Application Gateway to Static Website URL

   - When configuring the Application Gateway, set it to redirect error pages to the `error.html` page.
   - Use the Primary Endpoint URL from the Static Website settings as the redirection URL.
   
   - Ensure the `error.html` file is accessible publicly, as it will be referenced in the Application Gateway's error handling configuration.


Following these steps will set up the storage account with static website hosting, enabling the `error.html` page to handle error responses via the Application Gateway.





# Step-by-Step Guide for Setting Up Application Gateway1 for East US:
------------------------------------------------------------------------

1. Creating the Application Gateway

   - Azure Portal Configuration:
     - Go to the Azure Portal and search for Application Gateway.
     - Select Create Application Gateway.
     - Resource Group: Choose Capstone Project.
     - Application Gateway Name: Ag1
     - Region: East US
     - Instance Count: Set the minimum to 1 and the maximum to 5.
     - Virtual Network: Select Vnet1. 
       - Note: Application Gateway and VM should reside in the same virtual network but must be in different subnets.

   - Subnet: Select the subnet designated for the Application Gateway, not the one used by the VM.


2. Configuring the Frontend IP

   - In the Frontends section:
     - Create a new IP:
       - Name: ag1_ip1
     - Click OK to finalize.


3. Adding Backend Pools

   - Go to the Backends section and Add Backend Pool:
     - Pool 1:
       - Name: pool1
       - Target Type: Virtual Machine
       - Target VM: Select VM1 (select created in East US)
       - Click Add
   
     - Pool 2:
       - Name: pool2
       - Target Type: Virtual Machine
       - Target VM: Select VM2(select created in East US)
       - Click Add
   
   - Both backend pools (pool1 and pool2) should now be added.


4. Configuring Routing Rules

   - In the Configuration section, Add a Routing Rule:
     - Rule Name: rule1
     - Priority: 1
     - Listener Name: Provide a name.
     - Custom Error Pages:
       - Bad Gateway (502): Enter the URL of the `error.html` file hosted as a static website in the storage account.
       - Forbidden (403): Use the same URL.
     - Example URL for custom error pages:  
       - Bad Gateway (502): `https://capstoneproject1610.z19.web.core.windows.net/error.html`
       - Forbidden (403): `https://capstoneproject1610.z19.web.core.windows.net/error.html`

   - In the Backend Targets section of the rule:
     - Backend Target: Select pool2
       - Reason: This directs traffic to the home VM (VM2), which is the intended target for general website traffic, like a home page.

   - Backend Settings:
     - Default


5. Adding a Path-Based Rule for Uploads

   - Path: /upload (path for the upload section)
   - Target Name: upload (the container name in the storage account)
   - Backend Setting: Default
   - Backend Target: Select pool1

   - Click Add to finalize the path-based rule.


6. Final Steps
   - Review the configurations and select Review + Create to deploy Application Gateway1 with the specified settings.

This setup will configure Application Gateway1 for optimal traffic distribution, with custom error pages and path-based rules for directing traffic to specific resources.





# Step-by-Step Guide for Setting Up Application Gateway2 for West US:
------------------------------------------------------------------------

1. Creating the Application Gateway

   - Azure Portal Configuration:
     - Go to the Azure Portal and search for Application Gateway.
     - Select Create Application Gateway.
     - Application Gateway Name: Ag2
     - Region: West US2
     - Instance Count: Set the minimum to 1 and the maximum to 5.
     - Virtual Network: Select Vnet2. 
       - Note: Application Gateway and VM should reside in the same virtual network but must be in different subnets.

   - Subnet: Select the subnet designated for the Application Gateway, not the one used by the VM.


2. Configuring the Frontend IP

   - In the Frontends section:
     - Create a new IP:
       - Name: ag2_ip2
     - Click OK to finalize.


3. Adding Backend Pools

   - Go to the Backends section and Add Backend Pool:
     - Pool 1:
       - Name: pool1
       - Target Type: Virtual Machine
       - Target VM: Select VM1 (created in West US)
       - Click Add
   
     - Pool 2:
       - Name: pool2
       - Target Type: Virtual Machine
       - Target VM: Select VM2 (created in West US)
       - Click Add
   
   - Both backend pools (pool1 and pool2) should now be added.


4. Configuring Routing Rules

   - In the Configuration section, Add a Routing Rule:
     - Rule Name: rule2
     - Priority: 1
     - Listener Name: Provide a name.
     - Custom Error Pages:
       - Bad Gateway (502): Enter the URL of the `error.html` file hosted as a static website in the storage account.
       - Forbidden (403): Use the same URL.
     - Example URL for custom error pages:  
       - Bad Gateway (502): `https://capstoneproject1610.z19.web.core.windows.net/error.html`
       - Forbidden (403): `https://capstoneproject1610.z19.web.core.windows.net/error.html`

   - In the Backend Targets section of the rule:
     - Backend Target: Select pool2
       - Reason: This directs traffic to the home VM (VM2), which is the intended target for general website traffic, like a home page.

   - Backend Settings:
     - Default


5. Adding a Path-Based Rule for Uploads

   - Path: /upload (path for the upload section)
   - Target Name: upload (the container name in the storage account)
   - Backend Setting: Default
   - Backend Target: Select pool1

   - Click Add to finalize the path-based rule.


6. Final Steps
   - Review the configurations and select Review + Create to deploy Application Gateway2 with the specified settings.
 
This setup completes the configuration for Application Gateway2 in the West US, providing traffic distribution, custom error pages, and path-based rules for directing traffic as needed.





# Step-by-Step Guide for Cloning Repository and Running Scripts on VMs:
-------------------------------------------------------------------------

1. Cloning the GitHub Repository

   - Clone Repository:
     - Clone the GitHub repository:  
       `https://github.com/azcloudberg/azproject`
     
   - Using PuTTY to Connect:
     - Copy the IP address of VM1 (East US) and paste it into PuTTY to connect.
     - Copy the IP address of VM2 (East US) and paste it into PuTTY to connect in parallel.
     - Next, copy the IP address of VM1 (West US) and open it in PuTTY.
     - Finally, copy the IP address of VM2 (West US) and paste it into PuTTY to connect.

   - Connections: 
     - Now you are connected to all four VMs.


2. Running Scripts on the VMs

   - On VM1 (East US):
     - Run the following commands to update and clone the repository:
       ```bash
       sudo apt-get update
       git clone https://github.com/azcloudberg/azproject
       cd azproject
       ./vm1.sh
       ```

   - On VM2 (East US):
     - Run the following commands:
       ```bash
       sudo apt-get update
       git clone https://github.com/azcloudberg/azproject
       cd azproject
       ./vm2.sh
       ```

   - On VM1 (West US):
     - Repeat the commands to clone the repository and run the script:
       ```bash
       sudo apt-get update
       git clone https://github.com/azcloudberg/azproject
       cd azproject
       ./vm1.sh
       ```

   - On VM2 (West US):
     - Repeat the commands for VM2:
       ```bash
       sudo apt-get update
       git clone https://github.com/azcloudberg/azproject
       cd azproject
       ./vm2.sh
       ```


3. Configuring Storage Account Access

   - Access Key:
     - Go to the Storage Account and find the access key.
     
   - Edit `config.py`:
     - Open the terminal on both VM1 (East US) and VM1 (West US):
       ```bash
       sudo nano config.py
       ```
     - Copy the Storage Account Name and replace it in `config.py` on both VMs.
     - Copy the Access Key and replace it in the same file on both VMs.


4. Network Settings Configuration

   - Inbound Rule:
     - Go to Azure VM1 (East US):
       - Network Settings: Add an inbound rule to allow traffic from anywhere to port 5000.

   - Install Flask:
     - Run the following commands on both VM1 (East US) and VM1 (West US):
       ```bash
       sudo pip3 install flask --break-system-packages
       sudo apt update
       sudo apt install python3-flask
       python3 -m flask --version
       sudo pip3 install azure-storage-blob --break-system-packages
       nano app.py  # Replace port: 80 with port: 5000
       python3 app.py
       ```

5. Running the Application

   - Execute the Application:
     - Run the following command on both VMs:
       ```bash
       sudo python3 app.py


6. Final Steps for VM1 (West US)

   - Repeat the same command execution as done for VM1 (East US):
   - Inbound Rule:
       - Go to Azure VM1 (West US):
       - Network Settings: Add an inbound rule to allow traffic from anywhere to port 5000.
    
 ```bash
       sudo pip3 install flask --break-system-packages
       sudo apt update
       sudo apt install python3-flask
       python3 -m flask --version
       sudo pip3 install azure-storage-blob --break-system-packages
       nano app.py  # Replace port: 80 with port: 5000
       python3 app.py
     ```

This guide ensures that the repository is cloned, scripts are executed, and necessary configurations are made on all four virtual machines.





# Step-by-Step Guide for Creating Azure Traffic Manager:
----------------------------------------------------------

1. Create Azure Traffic Manager

   - Search for Traffic Manager:
     - Go to the Azure portal and search for Traffic Manager.

   - Create Traffic Manager Profile:
     - Name: `azuretrafficmanager14`
     - Routing Method: Performance
     - Subscription: (Select your subscription)
     - Resource Group: `CapstoneProject`


2. Configure Endpoints for Application Gateways

   - For Application Gateway 1 (ag1):
     - Go to Application Gateway 1 (ag1).
     - Click on Frontend Public IP.
     - Select Configuration.
     - DNS Name Label: `ag1dnsproject`
     - Click Save.

   - For Application Gateway 2 (ag2):
     - Go to Application Gateway 2 (ag2).
     - Click on Frontend Public IP.
     - Select Configuration.
     - DNS Name Label: `ag2dnsproject`
     - Click Save.


3. Add Endpoints in Traffic Manager

   - Go to Traffic Manager:
     - Navigate to Traffic Manager -> `azuretrafficmanager14` (the one created recently).

   - Add Endpoints:
     - Endpoint 1:
       - Click on Settings -> Endpoints.
       - Add Endpoint:
         - Type: Azure Endpoint
         - Name: `endpoint1`
         - Enable Endpoint: Check
         - Target Resource: Public IP Address
         - Click on the dropdown to select the Public IP address associated with ag1_ip1.
         - Click Add.

     - Endpoint 2:
       - Again, click on Add Endpoint:
         - Type: Azure Endpoint
         - Name: `endpoint2`
         - Enable Endpoint: Check
         - Target Resource: Public IP Address
         - Click on the dropdown to select the Public IP address associated with ag2_ip2.
         - Click Add.


4. Final Steps

   - Refresh Portal:
     - After adding the endpoints, refresh the Azure portal.

   - Copy DNS Name:
     - Go to the Overview section and copy the DNS Name:  
       `http://azuretrafficmanager14.trafficmanager.net`

   - Test the DNS Name:
     - Open a new tab in your browser and run the URL:  
       `http://azuretrafficmanager14.trafficmanager.net`

   - Access Storage Account File:
     - Test accessing the upload file by navigating to:  
       `http://azuretrafficmanager14.trafficmanager.net/upload1`
       - This should display the `error.html` file located in the storage account inside the `upload` container.


This completes the first part of your project with the Azure Traffic Manager setup.




