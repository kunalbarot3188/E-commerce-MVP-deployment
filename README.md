# E-commerce-MVP-deployment


Part 1: E-commerce MVP deployment
Create Magento free account on:
https://marketplace.magento.com/
Create and Save the Public and Private Key from your Magento account
Your User | My Profile | Marketplace | Access Key | Magento 2
Example:
Public Key: b2041f02509880fbbb96312b29995cb6
Private Key: 7be7c69e79bd798a2a8a6b00988a5b72
Install Terraform on AWS Cloud Shell
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo ‘https://rpm.releases.hashicorp.com/AmazonLinux/hashicorp.repo’
sudo yum -y install terraform
Download the Terraform files on AWS Cloud Shell or your EC2 Instance or your local machine.
mkdir final project
cd final project
use terraform files in the repo
Edit Terraform files | variable :
vi main.tf
•	VPC-id: VPC Default
•	SSH Key: sshkey1
•	instance type = "t3a.large"
•	Saving changes: ("Esc" | ":wq")
EC2 pricing:
https://aws.amazon.com/ec2/pricing/on-demand/
Running Terraform to deploy the EC2 VM
terraform init
terraform plan
terraform apply
ls | a new file was created: 'terraform.tfstate'
Part 2: Installing Ansible on EC2 instance
Connect to your EC2 instance via SSH:
ssh -i **sshkey1.pem** ec2-user@**ec2-public-ip**
Installing Ansible
sudo yum-config-manager --enable epel
sudo yum install ansible -y
Download the Ansible playbooks
given in the anisble folder
Edit and save Ansible file parameters
cd ansible-magento2
vi group vars/all.yml
•	magento domain: ec2-public-ip
•	server hostname: ec2-public-ip
•	repo api key: b2041f02509880fbbb96312b29995cb6 (insert your public key)
•	repo secret key: 7be7c69e79bd798a2a8a6b00988a5b72 (insert your private key)
•	Save the file ("Esc" | ":x")
Run Ansible to deploy the stack of tools for the e-commerce
ansible-playbook -i hosts.yml ansible-magento2.yml -k -vvv --become
Testing E-commerce Website:
•	Just copy and paste the EC2 Public IP in the browser.
•	…in some cases, it can take some minutes to get the website available!
Configuring E-commerce:
•	http://EC2 PUBLIC IP/securelocation
User: Admin
Password: Strong123Password#
Download the ecommerce images and personalize the ecommerce website.
given in the images folder
•	Content > Configuration > Default Store View > Edit
•	'HTML Head' | Default page title: The Cloud Bootcamp Store
•	'Header' > Logo image: The Cloud Bootcamp logo from images
•	'Header' > Welcome text: Welcome to The Cloud Bootcamp Store!
•	Save Configuration!
If requested "Refresh no Cache", following these steps:
•	Cache Refresh (Flush it) | Please go to 'Cache Management' and refresh cache types.
Configuration Status: INVALIDATED | Select it and Click on "Flush Magento Cache'
Otherwise, follow these customization e-commerce steps:
•	Catalog > Products > Add product > The Cloud Bootcamp T-Shirt
•	Price: 80
•	Quantity: 100
•	Images And Videos > Add images
•	Save
•	Content > Pages > Home Pages > Select | Edit
•	Click Content > Erase content
•	Insert Widget > Widget type: Catalog New Products List > Insert Widget
Check if the customization is in place:
Click on  Admin | Customer View
E-commerce deployment done successfully!!! 🚀
 
Capture the evidence.
Remove the resources deployed via AWS Cloud Shell
If needed, re-install the Terraform:
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo <https://rpm.releases.hashicorp.com/AmazonLinux/hashicorp.repo>
sudo yum -y install terraform
Destroying resources:
cd ~/projeto final/terraform/

terraform destroy
Links:
Ansible Documentation:
https://docs.ansible.com/ansible-core/devel/user_guide/index.html
