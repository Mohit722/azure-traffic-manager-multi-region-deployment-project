# Project Setup Instructions

# Welcome to the Azure Traffic Manager Multi-Region Deployment project! 

Follow these step-by-step instructions to set up and deploy the project across Central US and West US regions.

 
Prerequisites
1. Ensure you have access to an Azure account with permissions to create resources.
2. Set up four Virtual Machines (VMs) – two in each region (Central US and West US).

Step-by-Step Guide

1. Follow the Project Documentation:
   - Clone this repository to access all necessary files.
   - Refer to the `project-documents/installation-guide.md` (or other relevant file) for detailed instructions on setting up Azure Traffic Manager, Application Gateways, Virtual Networks, and VMs.

2. Deploy the Required Files to Each VM:
   - File List: Make sure the following files are accessible on all four VMs, which you will set up:
     - `.github/workflows`
     - `templates`
     - `README.md`
     - `app.py`
     - `config.py`
     - `error.html`
     - `index.html`
     - `vm1.sh`
     - `vm2.sh`

   - Clone this Repository:
     - On each VM, clone the repository using:
       ```bash
       git clone https://github.com/azcloudberg/azproject.git
       ```
     - Navigate to the project directory:
       ```bash
       cd azproject
       ```

3. Configure and Run VM-Specific Scripts:
   - On VM 1 in each region, run:
     ```bash
     bash vm1.sh
     ```
   - On VM 2 in each region, run:
     ```bash
     bash vm2.sh
     ```
   These scripts will set up the Upload Page on VM 1 and the Home Page on VM 2, respectively.

4. Deploy Static Website for Error Handling:
   - Upload `error.html` to your Azure Storage Account and enable static website hosting to ensure proper error handling across the application.

5. Finalize Configuration:
   - Follow the remaining steps in the project documentation to configure DNS settings, connect the Azure Traffic Manager, and test your deployment.

By following these instructions and using the provided scripts, you will set up a multi-region architecture with robust traffic management and error handling features.


