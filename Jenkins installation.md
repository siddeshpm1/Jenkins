Step 1 — Installing Jenkins
The version of Jenkins included with the default Ubuntu packages is often behind the latest available version from the project itself. To ensure you have the latest fixes and features, use the project-maintained packages to install Jenkins.
First, add the repository key to the system:
1.	wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
2.	
Copy
After the key is added the system will return with OK.
Next, let’s append the Debian package repository address to the server’s sources.list:
1.	sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
2.	
Copy
After both commands have been entered, we’ll run update so that apt will use the new repository.
1.	sudo apt update
2.	
Copy
Finally, we’ll install Jenkins and its dependencies.
1.	sudo apt install jenkins
2.	
Copy
Now that Jenkins and its dependencies are in place, we’ll start the Jenkins server.
Step 2 — Starting Jenkins
Let’s start Jenkins by using systemctl:
sudo systemctl start jenkins
Since systemctl doesn’t display status output, we’ll use the status command to verify that Jenkins started successfully:
1.	sudo systemctl status jenkins
2.	
Copy
If everything went well, the beginning of the status output shows that the service is active and configured to start at boot:
Output
● jenkins.service - LSB: Start Jenkins at boot time
   Loaded: loaded (/etc/init.d/jenkins; generated)
   Active: active (exited) since Fri 2020-06-05 21:21:46 UTC; 45s ago
     Docs: man:systemd-sysv-generator(8)
    Tasks: 0 (limit: 1137)
   CGroup: /system.slice/jenkins.service
Now that Jenkins is up and running, let’s adjust our firewall rules so that we can reach it from a web browser to complete the initial setup.
Step 3 — Opening the Firewall
To set up a UFW firewall, visit Initial Server Setup with Ubuntu 20.04, Step 4- Setting up a Basic Firewall. By default, Jenkins runs on port 8080. We’ll open that port using ufw:
1.	sudo ufw allow 8080
2.	
Copy
Note: If the firewall is inactive, the following commands will allow OpenSSH and enable the firewall:
1.	sudo ufw allow OpenSSH
2.	
3.	sudo ufw enable
4.	
Copy
Check ufw’s status to confirm the new rules:
1.	sudo ufw status
2.	
Copy
You’ll notice that traffic is allowed to port 8080 from anywhere:
Output
Status: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere
8080                       ALLOW       Anywhere
OpenSSH (v6)               ALLOW       Anywhere (v6)
8080 (v6)                  ALLOW       Anywhere (v6)
With Jenkins installed and our firewall configured, we can complete the installation stage and dive into Jenkins setup.
Step 4 — Setting Up Jenkins
To set up your installation, visit Jenkins on its default port, 8080, using your server domain name or IP address: http://your_server_ip_or_domain:8080
You should receive the Unlock Jenkins screen, which displays the location of the initial password:

In the terminal window, use the cat command to display the password:
1.	sudo cat /var/lib/jenkins/secrets/initialAdminPassword
2.	
Copy
Copy the 32-character alphanumeric password from the terminal and paste it into the Administrator password field, then click Continue.
The next screen presents the option of installing suggested plugins or selecting specific plugins:

We’ll click the Install suggested plugins option, which will immediately begin the installation process.

When the installation is complete, you’ll be prompted to set up the first administrative user. It’s possible to skip this step and continue as admin using the initial password we used above, but we’ll take a moment to create the user.
Note: The default Jenkins server is NOT encrypted, so the data submitted with this form is not protected. Refer to How to Configure Jenkins with SSL Using an Nginx Reverse Proxy on Ubuntu 20.04 to protect user credentials and information about builds that are transmitted via the web interface.

Enter the name and password for your user:

You’ll receive an Instance Configuration page that will ask you to confirm the preferred URL for your Jenkins instance. Confirm either the domain name for your server or your server’s IP address:

After confirming the appropriate information, click Save and Finish. You’ll receive a confirmation page confirming that “Jenkins is Ready!”:

Click Start using Jenkins to visit the main Jenkins dashboard:

At this point, you have completed a successful installation of Jenkins.
Conclusion
In this tutorial, you installed Jenkins using the project-provided packages, started the server, opened the firewall, and created an administrative user. At this point, you can start exploring Jenkins.
When you’ve completed your exploration, follow the guide How to Configure Jenkins with SSL Using an Nginx Reverse Proxy on Ubuntu 20.04 to protect your passwords, as well as any sensitive system or product information that will be sent between your machine and the server in plain text to continue using Jenkins.
To learn more about what you can do using Jenkins, check out other tutorials on the subject:
•	How to Build Android Apps with Jenkins
•	How To Set Up Continuous Integration Pipelines in Jenkins on Ubuntu 16.04

![image](https://github.com/siddeshpm1/Jenkins/assets/109099693/87a88c85-82a5-4a9c-b612-62f4e0566239)
