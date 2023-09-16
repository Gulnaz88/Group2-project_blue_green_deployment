# Task
# Create 3 images with Apache Web server installed. 1st Image should contain “Version 1” in index.hmtl, 
2nd image should contains “Version 2” in index.html and 3rd image should contain “canary” in index.html
Create 2 VMs from each image (total 6)
Create Load Balancer for 6 VMs (create 3 Target Groups for each image)
Perform Blue-Green deployment
Perform Canary deployment

# Create 3 images with Apache Web server installed. 1st Image should contain “Version 1” in index.hmtl, 2nd image should
contains “Version 2” in index.html and 3rd image should contain “canary” in index.html
               Steps: 
Go to the AWS Console and create EC2 instance with the user data : 
#!/bin/bash
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
sudo echo "Version 1" > /var/www/html/index.html

Create the second  EC2 instance with the user data:
#!/bin/bash
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
sudo echo "Version 1" > /var/www/html/index.html

Create the third EC2 instance with the user data:
#!/bin/bash
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
sudo echo "canary" > /var/www/html/index.html

4.  From the each created EC2 instances create Image.
Image 1 is created from the VM1 
Image 2 is created from the VM2
Image 3 is created from the VM3
5. Navigate to the AMIs and validate that 3 Images are created successfully.
                                      Create 2 VMs from each image (total 6) 
While in AMIs page, select the first Image and create 2 EC2 Instances:
Create 2 EC2 instances from the second Image
Create 2 EC2 instances from the third Image

# Create Load Balancer for 6 VMs (create 3 Target Groups for each image) 

Steps:
Create a Target Group. 
a.  Target type: Instances  
b.  Health Check: /index.html 
C. Attach the 2  EC2 instances  from the Image1

Create a Target Group. 
a.  Target type: Instances  
b.  Health Check: /index.html 
C. Attach the 2  EC2 instances  from the Image2

Create a Target Group. 
a.  Target type: Instances  
b.  Health Check: /index.html 
C. Attach the 2  EC2 instances  from the Image3

# 4. Navigate to Load Balancer and create a new Load Balancer
Select the Application Load Balancer
Give a name and select all AZs
Attach Security Group
Under the Listener section select your default Target Group
5. From the Search bar find Route 53 and create a Hosted Zone with the domain name taken from the Load Balancer. Make sure it’s Public
6. Click on created Hosted Zone name  and create a Record
7. Provide the name for Hosted Zone. 
8. Under the Record type drop-down select CNAME
9. Inside of the Value box type in the DNS taken from the Load Balancer and hit Create Record
10. Check the square next to the Record Name and from the right menu copy the Record name
11. Paste the Record name on the Web Browser

# Perform Blue-Green deployment 

Steps:
Go  to the Load Balancer screen and  select the name of the Load Balancer
Find the Protocol HTTP under the Listeners and Rules and click on it
Expand the Actions drop-down and select the Edit Listener
Navigate to the Action Types section and select the Target groups with Version 1 and Version 2
Set the Weight to 50% for both Target Groups and Save
Go back to the Browser and refresh the page
Verify that the web traffic is spread equally between 2 Versions (Version1 and Version 2)

# Perform Canary deployment

Navigate to the Edit Listener Screen and select the Canary version in the drop-down under the Action Types instead of the Version 1
Set the Weight to 20% for Canary and 80% for Version 2
On the Web Browser verify that the  traffic flows accordingly
Repeat steps 2 and 3 but set the Weight to Canary increasingly, but the for Version 2 descendingly until you reach the Weight: Canary 100% and Version 0%
Test on the Browser if the traffic is 100% on the Canary version.
Congratulations! You’ve done your project!
