# Installing Jenkins
Prerequisites 
Java should be installed 
```
https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-on-ubuntu-20-04#installing-specific-versions-of-openjdk
```
Add the repository key to the system:

```
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian/jenkins.io-2023.key
```
After the key is added the system will return with OK.
Next, let’s append the Debian package repository address to the server’s **sources.list:**
```
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
```

After both commands have been entered, we’ll run update so that apt will use the new repository.
```
sudo apt-get update
```

Finally, we’ll install Jenkins and its dependencies.
```
sudo apt-get install jenkins
```   
Now that Jenkins and its dependencies are in place, we’ll start the Jenkins server.

## Starting Jenkins
Let’s start Jenkins by using **systemctl:**
```
sudo systemctl start jenkins
```
Since systemctl doesn’t display status output, we’ll use the status command to verify that Jenkins started successfully:
```
sudo systemctl status jenkins
```

If everything went well, the beginning of the status output shows that the service is active and configured to start at boot:
```
Output
● jenkins.service - LSB: Start Jenkins at boot time
   Loaded: loaded (/etc/init.d/jenkins; generated)
   Active: active (exited) since Fri 2020-06-05 21:21:46 UTC; 45s ago
     Docs: man:systemd-sysv-generator(8)
    Tasks: 0 (limit: 1137)
   CGroup: /system.slice/jenkins.service
```
Now that Jenkins is up and running, let’s adjust our firewall rules so that we can reach it from a web browser to complete the initial setup.
Step 3 — Opening the Firewall
To set up a UFW firewall, visit Initial Server Setup with Ubuntu 20.04, Step 4- Setting up a Basic Firewall. By default, Jenkins runs on port 8080. We’ll open that port using ufw:
```
sudo ufw allow 8080
```
Note: If the firewall is inactive, the following commands will allow OpenSSH and enable the firewall:
```
sudo ufw allow OpenSSH
sudo ufw enable
```
Check ufw’s status to confirm the new rules:
```
sudo ufw status
```

You’ll notice that traffic is allowed to port 8080 from anywhere:
```
Output
Status: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere
8080                       ALLOW       Anywhere
OpenSSH (v6)               ALLOW       Anywhere (v6)
8080 (v6)                  ALLOW       Anywhere (v6)

```
With Jenkins installed and our firewall configured, we can complete the installation stage and dive into Jenkins setup.

## Setting Up Jenkins
To set up your installation, visit Jenkins on its default port, 8080, using your server domain name or IP address: http://your_server_ip_or_domain:8080
(If you are using EC2 machine copy the public ip of EC2 IP ex--http://172.96.35.23:8080)
You should receive the Unlock Jenkins screen, which displays the location of the initial password:

![image](https://github.com/siddeshpm1/Jenkins/assets/109099693/0e00d18f-e6a9-4388-8c75-0fd2350728a0)

In the terminal window, use the cat command to display the password:
```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```	
## initializing Jenkins
Copy the 32-character alphanumeric password from the terminal and paste it into the Administrator password field, then click Continue.
The next screen presents the option of installing suggested plugins or selecting specific plugins:

![image](https://github.com/siddeshpm1/Jenkins/assets/109099693/63174b88-fb53-46c4-93ec-517381e6a242)

We’ll click the Install suggested plugins option, which will immediately begin the installation process.

![image](https://github.com/siddeshpm1/Jenkins/assets/109099693/6b1b6b4c-934b-4376-85a9-a93267fd39c4)

When the installation is complete, you’ll be prompted to set up the first administrative user. It’s possible to skip this step and continue as admin using the initial password we used above, but we’ll take a moment to create the user.

![image](https://github.com/siddeshpm1/Jenkins/assets/109099693/31c258f1-2033-4709-aa20-f613a5610ed0)

Enter the name and password for your user:

![image](https://github.com/siddeshpm1/Jenkins/assets/109099693/ed5a8abd-c430-434e-ae7a-6ddba2168391)

You’ll receive an Instance Configuration page that will ask you to confirm the preferred URL for your Jenkins instance. Confirm either the domain name for your server or your server’s IP address:

![image](https://github.com/siddeshpm1/Jenkins/assets/109099693/3c131519-c4ed-4f50-98c2-d99473839bca)

After confirming the appropriate information, click Save and Finish. You’ll receive a confirmation page confirming that “Jenkins is Ready!”:

![image](https://github.com/siddeshpm1/Jenkins/assets/109099693/0873dd07-f887-405d-8916-874dee77b4bb)

Click Start using Jenkins to visit the main Jenkins dashboard:

![Uploading image.png…]()

At this point, you have completed a successful installation of Jenkins.
Conclusion

In this tutorial, you installed Jenkins using the project-provided packages, started the server, opened the firewall, and created an administrative user. At this point, you can start exploring Jenkins.


